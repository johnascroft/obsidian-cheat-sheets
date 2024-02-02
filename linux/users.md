# Users

## sudo (super user do)

```bash
sudo su
```

## su (switch user)

```bash
su -i ironman
```

Who am I?

```bash
whoami
```

Who is logged in now:

```bash
who
```

Tells you who is logged in and what they are currently doing:

```bash
w
```

Encrypted versions of all user passwords:

```bash
sudo less /etc/shadow
```

Gives you a list of last system logins:

```bash
last | less
```

Show all users:

```bash
cat /etc/passwd
```

Show information on a user:

```bash
id www-data
```

## adduser

Adds a user with extra bits such as setting default shell, password, other information.

## useradd

Very basic command for adding a user - it will literally do just that - but will give you more control.

Create a user (passing `-m` will create a home folder in `/home/tstark`).

```bash
sudo useradd -m tstark
```

Shows all the options available for the `usermod` command (shorthand is `-h`):

```bash
usermod --help
```

Change default shell on a user account (shorthand is `-s`):

```bash
sudo usermod ironman --shell /bin/bash
```

Rename a user account from `ironman` to `tonystark`. Shorthand is `-l`.

```bash
sudo usermod --login tonystark ironman
```

Create a password for a user:

```bash
sudo passwd tstark
```

Set the default group for a user (`-g` shorthand):

```bash
sudo usermod --group wheel tstark
```

Add a additional group to a user. When a user is created, it creates a default group with the same name as the user: (`-a` and `-G` shorthand)

```bash
sudo usermod --append --groups superhero cdanvers
```

Lock out a user account (`-L` shorthand):

```bash
sudo usermod --lock dprince
```

Delete a user:

```bash
sudo userdel thor
```