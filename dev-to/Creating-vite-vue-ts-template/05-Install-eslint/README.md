# Install eslint

## Install eslint and setup default config files

1. Install eslint with typescript
    ```console
    $ npm install --save-dev eslint typescript @typescript-eslint/parser @typescript-eslint/eslint-plugin
    ```
1. Create eslint config file `touch .eslintrc.js`
1. Edit `.eslintrc.js` to look like this

    <!-- prettier-ignore -->
    ```javascript
    module.exports = {
      root: true,
      parser: '@typescript-eslint/parser',
      plugins: [
        '@typescript-eslint',
      ],
      extends: [
        'eslint:recommended',
        'plugin:@typescript-eslint/recommended',
      ],
    }
    ```

1. Create eslint ignore file `touch .eslintignore`
1. Edit `.eslintignore` to look like this
    ```gitignore
    # don't ever lint node_modules
    node_modules
    # don't lint build output (make sure it's set to your correct build folder name)
    dist
    # don't lint nyc coverage output
    coverage
    ```
1. Add `"lint": "eslint . --ext .js,.jsx,.ts,.tsx"` to `"scripts"` section in package.json
    ```json
    {
      ...,
      "scripts": {
        ...,
        "lint": "eslint . --ext .js,.jsx,.ts,.tsx"
      },
      ...
    }
    ```
1. Run `npm run lint`

    ```console
    $ npm run lint

    > vite-vue-typescript-starter@0.0.0 lint
    > eslint . --ext .js,.jsx,.ts,.tsx


    /path/to/project/vue-ts/.eslintrc.js
      1:1  error  'module' is not defined  no-undef

    ✖ 1 problem (1 error, 0 warnings)
    ```

1. First let's commit what we already've done `git add .`
1. `git commit -m 'install eslint with typescript`

### Fix `error 'module' is not defined no-undef`

1. From docs https://eslint.org/docs/rules/no-undef#environments

    > For convenience, ESLint provides shortcuts that pre-define global variables exposed by popular libraries and runtime environments.

1. Fix previous error by editing `.eslintrc.js` to look like this
    ```diff
     module.exports = {
       root: true,
    +  // https://eslint.org/docs/rules/no-undef#nodejs
    +  env: {
    +    node: true,
    +  },
    ```
1. Run `npm run lint`
1. `git add -u`
1. `git commit -m "fix: error 'module' is not defined no-undef"`

## Links

-   https://vueschool.io/articles/vuejs-tutorials/eslint-and-prettier-with-vite-and-vue-js-3/
-   https://eslint.org/docs/user-guide/getting-started
-   https://github.com/typescript-eslint/typescript-eslint/blob/master/docs/getting-started/linting/README.md

### Links for `error 'module' is not defined no-undef`

-   https://eslint.org/docs/user-guide/configuring/language-options#specifying-environments
-   https://eslint.org/docs/rules/no-undef#nodejs
-   https://stackoverflow.com/a/62335842/3627387
-   https://stackoverflow.com/a/63512242/3627387

## Project

[vue-ts](https://github.com/imomaliev/vue-ts)
