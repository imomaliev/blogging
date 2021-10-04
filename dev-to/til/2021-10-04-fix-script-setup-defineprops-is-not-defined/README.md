# Fix `script setup` `defineProps` is not defined

## Fix `defineProps is not defined`

### Problem

In one of my `vue-ts` series' [article](https://dev.to/imomaliev/creating-vite-vue-ts-template-project-configs-improvements-3617), I was asked how to resolve [this](https://dev.to/algil/comment/1igom) issue

> How have you resolve this console warning (on npm run dev)?
>
> [@vue/compiler-sfc]definePropsis a compiler macro and no longer needs to be imported.
>
> But if I don't import defineProps in HelloWorld.vue file, the next line is underline in red:
>
> defineProps<{ msg: string }>()
>
> With this message:
>
> 'defineProps' is not defined.eslint(no-undef)
>
> Thanks!

### Solution

Add `defineProps` to `globals` in `eslint`. From [docs](https://eslint.vuejs.org/user-guide/#compiler-macros-such-as-defineprops-and-defineemits-are-warned-by-no-undef-rule):

```diff
module.exports = {
+   globals: {
+     defineProps: "readonly",
+   }
}
```

Basically in newer vue versions with `script setup` syntax `defineProps` is no longer needs to be imported because it is a `compliler macro` as it states in quote above. So the solution was just to configure `eslint` to not warn about `defineProps`

## Links

-   https://dev.to/algil/comment/1igom
-   https://dev.to/imomaliev/creating-vite-vue-ts-template-project-configs-improvements-3617
-   https://eslint.vuejs.org/user-guide/#compiler-macros-such-as-defineprops-and-defineemits-are-warned-by-no-undef-rule
-   https://dev.to/imomaliev/comment/1ihh5

## Fix `'props' is assigned a value but never used @typescript-eslint/no-unused-vars`

### Problem

This is a continuation of `script setup` syntax usage. `eslint` thinks that variables like `props`, `emits` etc. are not used, but actually they are.

### Solution

Add `vue/script-setup-uses-vars` rule to eslint.

> ESLint no-unused-vars rule does not detect variables in `<script setup>` used in `<template>`. This rule will find variables in `<script setup>` used in `<template>` and mark them as used.

```diff
module.exports = {
  // Use the rule set.
  extends: ['plugin:vue/base'],
  rules: {
    // Enable vue/script-setup-uses-vars rule
+     'vue/script-setup-uses-vars': 'error',
  }
}
```

### Links

-   https://eslint.vuejs.org/rules/script-setup-uses-vars.html
-   https://eslint.vuejs.org/user-guide/#the-variables-used-in-the-template-are-warned-by-no-unused-vars-rule
