# Configure Eslint for Jest

## Enable linting for tests

1. Update `.eslintrc.js`
    ```diff
    @@ -16,4 +16,15 @@ module.exports = {
         'plugin:vue/vue3-recommended',
         'prettier',
       ],
    +  overrides: [
    +    {
    +      files: [
    +        '**/__tests__/*.{j,t}s?(x)',
    +        '**/tests/unit/**/*.spec.{j,t}s?(x)',
    +      ],
    +      env: {
    +        jest: true,
    +      },
    +    },
    +  ],
     }
    ```
1. `git add -u`
1. `git commit -m 'enable jest tests linting'`
1. Install `eslint-plugin-jest`
    ```console
    $ npm install --save-dev eslint-plugin-jest
    ```
1. Update `.eslintrc.js`
    ```diff
    -  plugins: ['@typescript-eslint'],
    +  plugins: ['@typescript-eslint', 'jest'],
       extends: [
         'eslint:recommended',
         'plugin:@typescript-eslint/recommended',
         'plugin:vue/vue3-recommended',
    +    'plugin:jest/recommended',
         'prettier',
       ],
       overrides: [
    ```
1. Add `eslint-plugin-jest` to `.pre-commit-config.yaml`
    ```diff
               - vue-eslint-parser@7.9.0
    +          - jest@27.0.6
    +          - eslint-plugin-jest@24.4.0
    ```
1. `git add -u`
1. `git commit -m 'install eslint-plugin-jest'`

## Links

-   https://eslint.org/docs/user-guide/configuring/language-options#specifying-environments
-   https://eslint.org/docs/user-guide/configuring/configuration-files#how-do-overrides-work
-   https://github.com/jest-community/eslint-plugin-jest

## Project

[vue-ts](https://github.com/imomaliev/vue-ts)
