# Scoop

## Introduction

[Scoop](https://scoop.sh/) is a command line installer for Windows. I use it to manage my [[php]] installations locally.

PHP configuration file can be found at:

```
C:\Users\jascroft\scoop\persist\php80\cli
```

Make sure to add a `custom.ini` file to the `conf.d` folder and don't update the default configuration.

---

To show all installed packages:

```bash
scoop list
```

To install a package, check the app you need [here](https://scoop.sh/#/apps). You will need to add (or ensure that it's already been added) and then install:

```bash
scoop bucket add versions
scoop install php80
```

Updating Scoop (this will also update buckets):

```bash
scoop update
```

Change CLI PHP version:

```bash
scoop reset php80
```