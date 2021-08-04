# Eslint and vue

## Configure eslint for vue

1. From docs `https://eslint.vuejs.org/user-guide/#how-to-use-a-custom-parser`

    > If you want to use custom parsers such as [babel-eslint](https://www.npmjs.com/package/babel-eslint) or [@typescript-eslint/parser](https://www.npmjs.com/package/@typescript-eslint/parser), you have to use the `parserOptions.parser` option instead of the `parser` option. Because this plugin requires [vue-eslint-parser](https://www.npmjs.com/package/vue-eslint-parser) to parse `.vue` files, this plugin doesn't work if you overwrite the `parser` option.

1. `npm install --save-dev eslint-plugin-vue vue-eslint-parser`
1. Update `.eslintrc.js`
    ```diff
    -  parser: '@typescript-eslint/parser',
    +  parser: "vue-eslint-parser",
    +  // https://github.com/vuejs/vue-eslint-parser#parseroptionsparser
    +  parserOptions: {
    +    parser: "@typescript-eslint/parser",
    +  },
       plugins: ['@typescript-eslint'],
       extends: [
         'eslint:recommended',
         'plugin:@typescript-eslint/recommended',
    +    'plugin:vue/vue3-recommended',
         'prettier',
       ],
     }
    ```
1. Update `package.json`
    ```diff
    -    "lint": "eslint . --ext .js,.jsx,.ts,.tsx"
    +    "lint": "eslint . --ext .js,.jsx,.ts,.tsx,.vue"
    ```
1. Run `npm run lint`
1. Run `npm run format`
1. `git add -u`
1. `git commit -m 'install eslint-plugin-vue and vue-eslint-parser'`

## Links

-   https://eslint.vuejs.org/user-guide/
-   https://eslint.vuejs.org/user-guide/#how-to-use-a-custom-parser
-   https://github.com/vuejs/vue-eslint-parser
-   https://github.com/vuejs/vue-eslint-parser#parseroptionsparser

## Project

{% github https://github.com/imomaliev/vue-ts no-readme %}
