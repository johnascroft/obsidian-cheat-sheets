# Replication

All commands on this page assume you are using [[linux]] as a Linux distribution.

## Example Vagrantfile

```ruby
Vagrant.configure("2") do |config|  
  config.vm.define "master" do |master|  
      master.vm.box = "ubuntu/trusty64"  
      master.vm.hostname = "master"  
      master.vm.network :private_network, ip: "10.11.12.50"  
  end  
  
  config.vm.define "slave" do |slave|  
      slave.vm.box = "ubuntu/trusty64"  
      slave.vm.hostname = "slave"  
      slave.vm.network :private_network, ip: "10.11.12.51"  
  end  
end
```

## Master Server Configuration

### Install MySQL Server:

```bash
sudo apt-get install -y mysql-server 
```

Add the following to `/etc/mysql/my.cnf` (could be `/etc/mysql/mysql.conf.d/mysqld.cnf`):

```bash
#bind-address = 10.11.12.50 (not required for replication)  
server-id = 1  
log_bin = /var/log/mysql/mysql-bin.log  
binlog_do_db = portal_admin  
#binlog_ignore_db = include_database_name
```

Restart MySQL:

```bash
sudo service mysql restart
```
  
Create a replication user:  

```bash
mysql -u root  
CREATE USER 'repl_user'@'%' IDENTIFIED BY 'slavepassword';  
GRANT REPLICATION SLAVE ON *.* TO 'repl_user'@'%';  
exit
```

Create a database and some records on master...  

Create a snapshot and copy it to the slave server. Using `--master-data` dumps the log file and position for use on the slave. The final colon at the end of the secure copy (SCP) is important!

All databases

```bash
mysqldump -u root --all-databases --master-data > masterdump.sql
```

One or more specified databases

```bash
mysqldump -u root --databases portal_admin --master-data > masterportaldump.sql
```  

Secure copy the file to the slave server - **the ending colon is important**. If you don’t see transfer info it hasn’t worked (e.g. 100% 2257     2.2KB/s   00:00).

```bash
scp masterdump.sql 10.11.12.51:
```

Example output (password prompt):  

```bash
vagrant@master:~$ scp masterdump.sql 10.11.12.51:  
vagrant@10.11.12.51's password: vagrant
```

## Slave Server Configuration

On the slave, install MySQL Server:  

```bash
sudo apt-get install -y mysql-server  
```

Add the following to /etc/mysql/my.cnf:  

```bash
#bind-address = 10.11.12.51  
server-id = 2  
```

Restart MySQL:  

```bash
sudo service mysql restart
```

Tell the slave what user, password, and host to use for the master server:  

```bash
mysql -u root  
CHANGE MASTER TO MASTER_HOST='10.11.12.50', MASTER_USER='repl_user', MASTER_PASSWORD='slavepassword';  
exit
```

Restore the snapshot:  

```bash
mysql -uroot < masterdump.sql 
``` 

Start the slave:  

```bash
mysql -u root  
start slave;  
show slave status \G;
```

## Check that the Master & Slave are in sync

If you have a table mydb.mytable, run the command against it (on both master and slave):  

```bash
mysql -u root  
checksum table portal_admin.sites;  
```

If the values do not come back the same, then something is out-of-sync!

## Show Slave Hosts (on Master)

```bash
mysql> show slave hosts;  
+-----------+------+------+-----------+  
| Server_id | Host | Port | Master_id |  
+-----------+------+------+-----------+  
|         2 |      | 3306 |         1 |  
+-----------+------+------+-----------+  
1 row in set (0.00 sec)
```

## MySQL Replication out of sync

If you’re running replication and you get something like the below (where one is running and the other is not):  

```bash
mysql> show slave status \G;  
  
Slave_IO_Running: Yes  
Slave_SQL_Running: No
```

One way to do it is to stop the slave and run a fresh snapshot from master. Be sure to include the `--master-data` option as this automatically appends the `CHANGE MASTER TO` statement required on the replica to start the replication process. This command will export all databases, and transfer to the slave server:  

```bash
vagrant@master:~$ mysqldump -uroot --all-databases --master-data > masterdump.sql  
vagrant@master:~$ scp masterdump.sql 10.11.12.51:  
```

This will export a single database:

```bash
vagrant@master:~$ mysqldump -uroot --databases portal_admin --master-data > masterdump.sql  
```

```bash
vagrant@slave:~$ mysql -uroot < masterdump.sql  
vagrant@slave:~$ mysql -uroot  
mysql> start slave; 
```  

Another thing to try is this (I’ve used this if one or a small number of transactions have failed). You will need to run this on the slave server.

```bash
STOP SLAVE;  
SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1;  
START SLAVE;
```