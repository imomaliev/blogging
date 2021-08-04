# Make eslint and prettier play nice together

## Install eslint-config-prettier

1. `npm install --save-dev eslint-config-prettier`
1. Add `'prettier'` to `.eslintrc.js`

    ```diff
    module.exports = {
      ...
      extends: [
        'eslint:recommended',
        'plugin:@typescript-eslint/recommended',
    +    'prettier',

      ],
    }
    ```

1. Run `npm run lint`
1. Run `npm run format`
1. `git add -u`
1. `git commit -m 'install eslint-config-prettier'`

## Links

-   https://github.com/prettier/eslint-config-prettier#installation
-   https://vueschool.io/articles/vuejs-tutorials/eslint-and-prettier-with-vite-and-vue-js-3/

## Project

{% github https://github.com/imomaliev/vue-ts no-readme %}
