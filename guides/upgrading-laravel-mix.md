# Upgrading Laravel Mix

Upgrading from v14.15.5 to v18.17.0

> [!NOTE]
> More than likely, `sass` and `sass-loader` will be way out of date. Remove them from the dependencies list and let the `laravel-mix` package pull in the right versions.

```bash
npm install laravel-mix --save
```

When you run `npm run dev` at this point, it will automatically pull in the right versions (it will automatically run this)

```bash
npm install sass-loader@^12.1.0 sass --save-dev --legacy-peer-deps
```