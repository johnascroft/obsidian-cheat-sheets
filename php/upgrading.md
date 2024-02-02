# Upgrading

Add the `ondrej/php` repository which contains the latest php versions. The software-properties-common installation gives a bunch of helpers which means you don’t have to manually edit `/etc/apt/sources.list` and/or any subsidiary files in `/etc/apt/sources.list.d` to manage repos. `apt update` will grab the latest versions of packages from the repos that it knows about.

```bashsudo apt install software-properties-common  
sudo add-apt-repository ppa:ondrej/php  
sudo apt update  
```

Install the version of php that you want:  

```bash
sudo apt install php7.4
```
  
Install the extensions you need for this particular PHP version

```bash
sudo apt install php7.4-extension_name
```

Enable PHP on apache. First you need to disable the php7.0 module, then enable the php7.4 module.

```bash
sudo a2dismod php7.0  
sudo a2enmod php7.4
```
  
Restart [[apache]] for the changes to take effect.

```bash
sudo service apache2 restart
```
