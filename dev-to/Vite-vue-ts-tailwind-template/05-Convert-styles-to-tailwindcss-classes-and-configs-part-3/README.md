# Convert styles to TailwindCSS classes and configs (Part 3)

## Preflight

TailwindCSS built on top of [modern-normalize](https://github.com/sindresorhus/modern-normalize) and has set of opinionated base styles.
From [docs](https://tailwindcss.com/docs/preflight):

> Preflight is a set of base styles for Tailwind projects that are designed to smooth over cross-browser inconsistencies and make it easier for you to work within the constraints of your design system.
> Because of that our project looks like this ![Missing styles](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pchiaz7afmbjjhauubcs.png)
> instead of looking like this
> ![Expected look](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nnuwxul9k6siadshi8g6.png)
> We could [disable preflight](https://tailwindcss.com/docs/preflight#disabling-preflight). But a better way would be explictly styling our code. This will ensure that our template looks same in all browsers.

## Fix missing styles

### Center `img`

1. We start with image not being centered. `img` tag has `display: block` in TailwindCSS instead of `display: inline` which is default. From [docs](https://tailwindcss.com/docs/preflight#images-are-block-level)

    > Images and other replaced elements (like svg, video, canvas, and others) are display: block by default.

1. Fix this by setting [left and right margins to `auto`](https://stackoverflow.com/questions/11856150/center-an-image-horizontally-using-css) with `mx-auto` class.

```diff
  -  <img alt="Vue logo" src="./assets/logo.png" />
  +  <img class="mx-auto" alt="Vue logo" src="./assets/logo.png" />
```

### Add `h1` text styles

1. Next our `h1`. From [docs](https://tailwindcss.com/docs/preflight#headings-are-unstyled)
    > All heading elements are completely unstyled by default, and have the same font-size and font-weight as normal text.
1. We can set headers styling as a part of our [base styles](https://tailwindcss.com/docs/adding-base-styles). But in this case we would add classes inline.
1. Add `text-4xl font-bold` to our `h1` tag in `src/components/HelloWorld.vue`
    ```diff
    -  <h1>{{ msg }}</h1>
    +  <h1 class="text-4xl font-bold">{{ msg }}</h1>
    ```

### Set margins

1. TailwindCSS has no default margins as well. From [docs](https://tailwindcss.com/docs/preflight#default-margins-are-removed)
    > Preflight removes all of the default margins from elements like headings, blockquotes, paragraphs, etc.
1. Add `my-6` to our `h1` to our `src/components/HelloWorld.vue`
    ```diff
    -  <h1 class="text-4xl font-bold">{{ msg }}</h1>
    +  <h1 class="text-4xl font-bold my-6">{{ msg }}</h1>
    ```
1. Create css selector for `p` with `my-4` class in `style` part of our `src/components/HelloWorld.vue` SFC.
    ```diff
     <style scoped>
    +p {
    +  @apply my-4;
    +}
    +
    ```

### Update `code` text styles

1. If we compare how our `code` tags look to `vue-ts` template we will see that text a little bigger.
1. Fix that by adding [`text-sm`](https://tailwindcss.com/docs/font-size#class-reference) class to our `code` styles.
    ```diff
     code {
    -  @apply bg-code py-0.5 px-1 text-code;
    +  @apply bg-code py-0.5 px-1 text-code text-sm;
     }
    ```

### Style `button`

1. In addition boarder styles are reset too. From [docs](https://tailwindcss.com/docs/preflight#border-styles-are-reset-globally)
    > In order to make it easy to add a border by simply adding the border class, Tailwind overrides the default border styles for all elements with the following rules:
1. So we have to manually set our `button` styling

```diff
-  <button type="button" @click="count++">count is: {{ count }}</button>
+  <button
+    class="
+      bg-white
+      hover:bg-gray-50
+      py-2
+      px-4
+      border border-gray-200
+      rounded
+      shadow-sm
+    "
+    type="button"
+    @click="count++"
+  >
+    count is: {{ count }}
+  </button>
```

### Commit all the changes above

1. `git add -u`
1. `git commit -m 'fix styles missing because of preflight'`

## Links

-   https://github.com/sindresorhus/modern-normalize
-   https://tailwindcss.com/docs/preflight
-   https://tailwindcss.com/docs/preflight#images-are-block-level
-   https://stackoverflow.com/questions/11856150/center-an-image-horizontally-using-css
-   https://tailwindcss.com/docs/preflight#headings-are-unstyled
-   https://tailwindcss.com/docs/adding-base-styles
-   https://tailwindcss.com/docs/preflight#default-margins-are-removed
-   https://tailwindcss.com/docs/margin
-   https://tailwindcss.com/docs/margin#customizing
-   https://tailwindcss.com/docs/padding
-   https://tailwindcss.com/docs/preflight#border-styles-are-reset-globally
-   https://tailwindcss.com/docs/preflight#buttons-have-a-default-outline

## Project

{% github https://github.com/imomaliev/vue-ts-tailwind no-readme %}
