# PHP

> [!INFO]
> Note that my local version of PHP running on Windows is managed by [Scoop](scoop).

- [Upgrading](upgrading)
- [Composer](composer)
- [OOP Tips](oop-tips)
- [Guidelines](guidelines)

## Change CLI version

This will bring up a menu showing all installed PHP versions and an option to switch it.    

```bash
sudo update-alternatives --config php
```

If you know the version, you can use this command to switch. This will switch to php8.1:

```bash
sudo update-alternatives --set php /usr/bin/php8.1
sudo update-alternatives --set php-config /usr/bin/php-config8.1
sudo update-alternatives --set phpize /usr/bin/phpize8.1
```

If you want to upgrade the entire PHP version on the server, see [[upgrading]].