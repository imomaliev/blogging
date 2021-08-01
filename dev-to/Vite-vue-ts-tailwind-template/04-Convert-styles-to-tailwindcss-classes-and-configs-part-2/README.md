# Convert styles to tailwindcss classes and configs (Part 2)

## Replace existing styles with TailwindCSS classes in `src/components/HelloWorld.vue`

### Replace for styles for `a`

1. There is only `color` in `a` selector. Add new `textColor` as we did in previous article.
1. Update our code

    ```diff
    diff --git a/src/components/HelloWorld.vue b/src/components/HelloWorld.vue
    index 7e9abbe..efb4ee8 100644
    --- a/src/components/HelloWorld.vue
    +++ b/src/components/HelloWorld.vue
    @@ -65,7 +65,7 @@ export default defineComponent({

     <style scoped>
     a {
    -  color: #42b983;
    +  @apply text-link;
     }

     label {
    diff --git a/tailwind.config.js b/tailwind.config.js
    index 8855955..eaabfc4 100644
    --- a/tailwind.config.js
    +++ b/tailwind.config.js
    @@ -8,7 +8,8 @@ module.exports = {
         },
         extend: {
           textColor: {
    -        'default': '#2c3e50'
    +        'default': '#2c3e50',
    +        'link': '#42b983'
           }
         },
       },
    ```

1. `git add -u`
1. `git commit -m 'add link color'`

### Replace styles for `code`

1. First replace `background-color`. As with `color` we will add new color called `code` in [`backgroundColor`](https://tailwindcss.com/docs/background-color#customizing) by `extend`ing our `theme`.
1. Then as with `margin` we will replace [`padding`](https://tailwindcss.com/docs/padding). Luckily there are classes that match our values.
1. Finally create new `textColor` called `code`.
1. Our code diff should look like this

    ```diff
    diff --git a/src/components/HelloWorld.vue b/src/components/HelloWorld.vue
    index efb4ee8..c761112 100644
    --- a/src/components/HelloWorld.vue
    +++ b/src/components/HelloWorld.vue
    @@ -68,15 +68,7 @@ a {
       @apply text-link;
     }

     code {
    -  background-color: #eee;
    -  padding: 2px 4px;
    -  border-radius: 4px;
    -  color: #304455;
    +  @apply bg-code py-0.5 px-1 text-code;
     }
     </style>
    diff --git a/tailwind.config.js b/tailwind.config.js
    index eaabfc4..d8ca082 100644
    --- a/tailwind.config.js
    +++ b/tailwind.config.js
    @@ -9,7 +9,11 @@ module.exports = {
         extend: {
           textColor: {
             'default': '#2c3e50',
    -        'link': '#42b983'
    +        'link': '#42b983',
    +        'code': '#304455',
    +      },
    +      backgroundColor: {
    +        'code': '#eeeeee',
           }
         },
       },
    ```

1. `git add -u`
1. `git commit -m 'replace code styles'`

## Links

-   https://tailwindcss.com/docs/text-color#text-colors
-   https://tailwindcss.com/docs/configuration#theme
-   https://tailwindcss.com/docs/customizing-colors#extending-the-defaults
-   https://tailwindcss.com/docs/margin
-   https://tailwindcss.com/docs/margin#customizing
-   https://tailwindcss.com/docs/background-color#customizing
-   https://tailwindcss.com/docs/padding

## Project

[vue-ts-tailwind](https://github.com/imomaliev/vue-ts-tailwind)
