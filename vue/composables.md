# Composables

If you find yourself writing Vue components in the "options API style" but just in composition API you may need to look at re-organising stuff. It's not good practice to organise components in the same way you do with options API.

E.g. don't write data first, then computed, then methods, then maybe watchers.

```js
// Data items
const message = ref('Hello');
const isVisible = ref(false);

// Computed
const reversedMessage = computed(() => {
    return message.value.split('').reverse().join('');
});

// Methods				
// Watchers
```

You should first organise them into common elements and then consider extracting them into [Composables](https://vuejs.org/guide/reusability/composables.html#composables) for re-usability.

```js
import { useMessage } from './useMessage';

const originalMessage = ref('Hello World');
const { toggleReverse, message } from useMessage(originalMessage);
```

The `useMessage.js` composable would look like this:

```js
import { ref, computed, watch, toRef } from 'vue';

export function useMessage(text) {
    const originalMessage = toRef(text);
    const isReversed = ref(false);
    function toggleReverse() {
        isReversed.value = !isReversed.value;
    }
    const message = computed(() => {
        if (isReversed.value) {
            return reversedMessage.value;
        }
        return originalMessage.value;
    });
    
    return {
        toggleReverse,
        message
    }
}
```

## "Inline" Composables

It might be that the composables aren't used anywhere else so it might be that it's just neater to create an "inline" composable where all the functionality is contained within your component.

https://gist.github.com/yyx990803/8854f8f6a97631576c14b63c8acd8f2e

```js
const { showHiddenFolders } = useHiddenFolders()

function useHiddenFolders () {
    const showHiddenFolders = ref(localStorage.getItem(SHOW_HIDDEN) === 'true')
    watch(showHiddenFolders, value => {
        if (value) {
            localStorage.setItem(SHOW_HIDDEN, 'true')
        } else {
            localStorage.removeItem(SHOW_HIDDEN)
        }
    }, { lazy: true })
    return {
        showHiddenFolders
    }
}
```