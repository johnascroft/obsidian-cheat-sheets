# Samba

Create a Linux user

```bash
useradd readonly
```

Add a password for the user

```bash
passwd readonly
[ enter password twice ]
```

Edit the `/etc/samba/smb.conf` file:

```bash
[vhosts-readonly]
path = /var/www/vhosts
available = yes
valid users = root,readonly
read only = yes
browseable = yes
public = yes
writable = no
```

Set the password for the Samba share

```bash
smbpasswd -a readonly
[ enter password entered above twice ]
```

Restart the `smbd` service:

```bash
service smbd restart
```