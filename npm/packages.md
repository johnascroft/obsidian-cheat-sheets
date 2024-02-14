# Packages

## Publishing

1. Generate a token from your [GitHub settings](https://github.com/settings/tokens/new) that has access to the following permissions:
    - `write:packages`
    - `read:packages`
    
2. Copy the key that is produced and use it in the next step.

3. Run both of these commands on your machine. It will add lines to the `~/.npmrc` file. This will allow you to publish to the package repository.

```bash
# Set the registry to be GitHub for all packages within the @crown scope
npm config set "@crown:registry" https://npm.pkg.github.com

# Provide the authToken
npm config set "//npm.pkg.github.com/:_authToken" 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
```

3. From your package directory, you can use the `npm publish` command to publish to the GitHub package repository. It will use the config that you set above. Make sure the version of the package is incremented accordingly as it won't let you publish the same version twice.

## Installing

You can install the package using the below syntax. It will use the authentication credentials that you specified in your npm config on your local machine (or server).

```bash
npm install @crown/ui@1.0.0
```


