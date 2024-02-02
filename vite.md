# Vite

You must ensure that Node.js (16+) and [[npm]] are installed before running Vite.

Default Vite config for Laravel:

```js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
 
export default defineConfig({
    plugins: [
        laravel([
            'resources/js/app.js',
        ]),
    ],
});
```