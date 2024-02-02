# Deploy

```bash
#!/bin/bash

# Put the application into maintenance mode
php artisan down

# Get the latest tag
TAG=$(git describe --tags $(git rev-list --tags --max-count=1))

git checkout -- .

# Checkout the latest tag
git checkout "$TAG"

# Install Composer dependencies and optimize the autoloader
composer install --optimize-autoloader --no-dev

# Do a clean install of npm (remove node_modules and performs a clean install)
npm ci && npm run production

# Run database migrations (--force to remove any prompts)
php artisan migrate --force

# Clear application cache
php artisan cache:clear

# Cache the config
# Laravel will read all the configuration files in the config/ directory 
# and merge them into a single file. This merged configuration file is then 
# stored in the bootstrap/cache directory as config.php.
php artisan config:cache

# Cache the routes
# It writes the compiled route array to a cache file 
# (bootstrap/cache/routes.php by default).
php artisan route:cache

# Bring the application back online
php artisan up
```