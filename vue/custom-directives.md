# Custom Directives

This is the `<script setup>` method:

```vue
<script setup>
const vTooltip = {
	mounted: (el, binding) => {
		const { value } = binding;

		tippy(el, {
			content: value.content,
			allowHTML: true,
			placement: value.placement || 'top',
			arrow: tippyPlugins.roundArrow,
			maxWidth: 'none',
			interactive: true,
			zIndex: 10003,
			theme: value.theme || 'default',
			animation: 'shift-away',
			appendTo: document.body,
		});
	}
}
</script>

<template>
  <input v-tooltip />
</template>
```

This is the global method using `createApp`:

```js
const app = createApp({})

app.directive('tooltip', {
	mounted(el, binding) {
		const { value } = binding;
		
		tippy(el, {
			content: value.content,
			allowHTML: true,
			placement: value.placement || 'top',
			arrow: tippyPlugins.roundArrow,
			maxWidth: 'none',
			interactive: true,
			zIndex: 10003,
			theme: value.theme || 'default',
			animation: 'shift-away',
			appendTo: document.body,
		});
	}
});
```