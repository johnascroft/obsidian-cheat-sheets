# Composer

Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.

- [Composer Docs](https://getcomposer.org/doc/)
- [Packagist](https://packagist.org/) - Main composer repository

## Installation

### [Linux](linux) 20.04

This will uninstall from `apt-get` if needed:

```bash
sudo apt-get remove composer
```

To install, change directory to the user directory and pull down the installer:

```bash
cd ~

curl -sS https://getcomposer.org/installer -o composer-setup.php

sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

To check your installation, run this (**you may need to restart your terminal**):

```bash
composer --version
```

---
## [require](https://getcomposer.org/doc/03-cli.md#require-r)

```bash
composer require "vendor/package:2.*"
```

## [remove](https://getcomposer.org/doc/03-cli.md#remove)

```bash
composer remove vendor/package
```

The `install` command reads the `composer.json` file from the current directory, resolves the dependencies, and installs them into `vendor`:

```bash
composer install
```

## [show / info](https://getcomposer.org/doc/03-cli.md#show-info)

To list all of the available packages, you can use the `show` command:

```bash
composer show
```

To filter the list you can pass a package mask using wildcards:

```bash
composer show "nesbot/*"
```

## [outdated](https://getcomposer.org/doc/03-cli.md#outdated)

Show outdated packages (`--direct` or `-D` will only get direct dependencies from your `composer.json`).

```bash
composer outdated -D
```

## [suggests](https://getcomposer.org/doc/03-cli.md#suggests)

Lists all packages suggested by the currently installed set of packages:

```bash
composer suggests
```

To upgrade composer itself (you can pass the version):

```bash
composer self-update --2
```

## [bump](https://getcomposer.org/doc/03-cli.md#bump)

```bash
composer bump
```