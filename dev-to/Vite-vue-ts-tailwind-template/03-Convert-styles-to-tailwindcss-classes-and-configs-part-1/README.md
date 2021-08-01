# Convert styles to tailwindcss classes and configs (Part 1)

## Enable `jit` mode

If you haven't heard TailwindCSS 2.1+ has a [`jit`](https://tailwindcss.com/docs/just-in-time-mode) mode. It speeds up build times and allows couple of extra features which take TailwindCSS's utility first approach to next level

Enabling `jit` is pretty [simple](https://tailwindcss.com/docs/just-in-time-mode#enabling-jit-mode)

1. Update `tailwind.config.js`
    ```diff
    +  mode: 'jit',
    ```
1. `git add -u`
1. `git commit -m 'enable tailwindcss jit'`

## Replace existing styles with TailwindCSS classes in `src/App`

### Replace `font-family`

1. Our first CSS property is [`font-family`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family) inside `#app` styles. To set `font-samily` for TailwindCSS project we will use [`fontFamily`](https://tailwindcss.com/docs/font-family#customizing) configuration in our [`theme`](https://tailwindcss.com/docs/configuration#theme) section of `tailwind.config.js`
1. Update our code

    ```diff
    diff --git a/src/App.vue b/src/App.vue
    index 1963bd4..9b68502 100644
    --- a/src/App.vue
    +++ b/src/App.vue
    @@ -17,7 +17,6 @@ export default defineComponent({

     <style>
     #app {
    -  font-family: Avenir, Helvetica, Arial, sans-serif;
       -webkit-font-smoothing: antialiased;
       -moz-osx-font-smoothing: grayscale;
       text-align: center;
    diff --git a/tailwind.config.js b/tailwind.config.js
    index 1858089..4d6d6e7 100644
    --- a/tailwind.config.js
    +++ b/tailwind.config.js
    @@ -2,6 +2,9 @@ module.exports = {
       purge: ['./index.html', './src/**/*.{js,jsx,ts,tsx,vue}'],
       darkMode: false, // or 'media' or 'class'
       theme: {
    +    fontFamily: {
    +      sans: ['Avenir', 'Helvetica', 'Arial', 'sans-serif'],
    +    },
         extend: {},
       },
       variants: {
    ```

1. `git add -u`
1. `git commit -m 'set font as a part of a tailwind theme'`

### Replace `-webkit-font-smoothing` and `-moz-osx-font-smoothing`

1. Next propperties are `-webkit-font-smoothing` and `-moz-osx-font-smoothing`. There is already [utility class](https://tailwindcss.com/docs/font-smoothing) for this properties. So we will use it with [`@apply`](https://tailwindcss.com/docs/functions-and-directives#apply) directive.
1. Update our code

    ```diff
    diff --git a/src/App.vue b/src/App.vue
    index 9b68502..67fbaa8 100644
    --- a/src/App.vue
    +++ b/src/App.vue
    @@ -17,8 +17,6 @@ export default defineComponent({

     <style>
     #app {
    -  -webkit-font-smoothing: antialiased;
    -  -moz-osx-font-smoothing: grayscale;
    +  @apply antialiased;
       text-align: center;
       color: #2c3e50;
       margin-top: 60px;
    ```

1. `git add -u`
1. `git commit -m 'replace -webkit-font-smoothing and -moz-osx-font-smoothing with antialiased utily class'`

### Replace `text-align`

1. `text-align` is pretty stright forward as well. There are [text alignment utilities](https://tailwindcss.com/docs/text-align).
1. Update our code

    ```diff
    diff --git a/src/App.vue b/src/App.vue
    index 67fbaa8..5c978a6 100644
    --- a/src/App.vue
    +++ b/src/App.vue
    @@ -17,7 +17,6 @@ export default defineComponent({

     <style>
     #app {
    -  @apply antialiased;
    -  text-align: center;
    +  @apply antialiased text-center;
       color: #2c3e50;
       margin-top: 60px;
     }
    ```

1. `git add -u`
1. `git commit -m 'replace text-align property with text-center class'`

### Replace `color`

1. General `color` as `font-family` should be set in `tailwind.config.js`. We could use one of jit's features and set color inline with ["Arbitrary value support"](https://tailwindcss.com/docs/just-in-time-mode#arbitrary-value-support) But in this case we will add new color called `default` in [`textColor`](https://tailwindcss.com/docs/text-color#customizing) by `extend`ing our `theme`.
1. Update our code

    ```diff
    diff --git a/src/App.vue b/src/App.vue
    index 5c978a6..08379dd 100644
    --- a/src/App.vue
    +++ b/src/App.vue
    @@ -17,7 +17,6 @@ export default defineComponent({

     <style>
     #app {
    -  @apply antialiased text-center;
    -  color: #2c3e50;
    +  @apply antialiased text-center text-default;
       margin-top: 60px;
     }
     </style>
    diff --git a/tailwind.config.js b/tailwind.config.js
    index c592ea4..8855955 100644
    --- a/tailwind.config.js
    +++ b/tailwind.config.js
    @@ -6,7 +6,11 @@ module.exports = {
         fontFamily: {
           sans: ['Avenir', 'Helvetica', 'Arial', 'sans-serif'],
         },
    -    extend: {},
    +    extend: {
    +      textColor: {
    +        default: '#2c3e50'
    +      }
    +    },
       },
       variants: {
         extend: {},
    ```

1. `git add -u`
1. `git commit -m 'add default color'`

### Replace `margin-top`

1. This is last style in `#app`. TailwindCSS uses `rem`'s for [`margin`](https://tailwindcss.com/docs/margin) classes. We have `margin-top: 60px;` in `rem`'s it would be `3.75`. By default there is no class for this value. We could [add](https://tailwindcss.com/docs/margin#customizing) one, but I prefer just choosing closest one from already preconfigured ones. Which will be `mt-16`.
1. Update our code

    ```diff
    diff --git a/src/App.vue b/src/App.vue
    index 08379dd..93f2f31 100644
    --- a/src/App.vue
    +++ b/src/App.vue
    @@ -14,9 +14,3 @@ export default defineComponent({
       },
     })
     </script>

    <style>
    #app {
    -  @apply antialiased text-center text-default;
    -  margin-top: 60px;
    +  @apply antialiased text-center text-default m-16;
    }
    </style>
    ```

1. `git add -u`
1. `git commit -m 'replace margin-top property with class'`

## Links

-   https://tailwindcss.com/docs/just-in-time-mode
-   https://tailwindcss.com/docs/text-color#text-colors
-   https://developer.mozilla.org/en-US/docs/Web/CSS/font-family
-   https://tailwindcss.com/docs/configuration#theme
-   https://tailwindcss.com/docs/font-family#customizing
-   https://tailwindcss.com/docs/functions-and-directives#apply
-   https://tailwindcss.com/docs/font-smoothing
-   https://tailwindcss.com/docs/customizing-colors#extending-the-defaults
-   https://tailwindcss.com/docs/just-in-time-mode#arbitrary-value-support
-   https://tailwindcss.com/docs/margin
-   https://tailwindcss.com/docs/margin#customizing

## Project

[vue-ts-tailwind](https://github.com/imomaliev/vue-ts-tailwind)
