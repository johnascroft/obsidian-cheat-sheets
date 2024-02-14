# npm

## Install

```bash
npm i moment
npm i moment --save-dev
```

Install specific version of a package

```bash
npm i moment@2.24.0

npm i moment@latest
```

## Upgrade

> [!info]
> Upgrades will always work within the version parameters you have set in the `package.json` file.

Upgrade all packages:

```bash
npm upgrade
```

Upgrade specific package:

```bash
npm upgrade moment
```

## Outdated

```bash
npm outdated
```

This will show something similar to the below. You can then see which packages are out of date and upgrade accordingly.

```txt
Package                Current   Wanted   Latest  Location
axios                   0.17.1   0.17.1    1.3.4  global
bootstrap-sass           3.4.1    3.4.3    3.4.3  global
chart.js                 2.9.4    2.9.4    4.2.1  global
cross-env                5.2.1    5.2.1    7.0.3  global
gauge                    2.7.4    2.7.4    5.0.0  global
jquery                   3.5.1    3.6.4    3.6.4  global
```

Prune will remove extraneous packages that in `node_modules` that aren't present in your `package.json` file.

```bash
npm list --depth 0
npm prune
```

## Font Awesome Pro setup

```bash
npm config set "@fortawesome:registry" https://npm.fontawesome.com/
npm config set "//npm.fontawesome.com/:_authToken" BB62B0FA-359F-4B56-910C-8D03AFCD8F2F
```