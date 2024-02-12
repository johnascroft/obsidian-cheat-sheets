# Filters

Filters in Vue 3 are no longer used in the same way that it was in Vue 2. To define a filter globally you would add it to the `createApp` function:

```js
const app = createApp(App);

app.config.globalProperties.$filters = {
    currencyUSD(value) {
        return '$' + value
    }
}
```

This is how you would use it:

```vue
<template>
    <h1>Bank Account Balance</h1>
    <p>{{ $filters.currencyUSD(accountBalance) }}</p>
</template>
```