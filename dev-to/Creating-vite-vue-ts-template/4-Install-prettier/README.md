# Install prettier

## Install prettier and setup default config files

1. Install prettier `npm install --save-dev prettier`
1. Create prettier config file `touch .prettierrc.js`
1. Edit `.prettierrc.js` to look like this
    ```javascript
    module.exports = {
      semi: false
      singleQuote: true,
      trailingComma: 'es5',
    }
    ```
1. Create prettier ignore file `touch .prettierignore`
1. Edit `.prettierignore` to look like this
    ```gitignore
    # Ignore artifacts:
    dist
    coverage
    ```
1. Add `"format": "prettier --write ."` to `"scripts"` section in package.json
    ```diff
       "scripts": {
         ...,
    -    "serve": "vite preview"
    +    "serve": "vite preview",
    +    "format": "prettier --write ."
       },
    ```
1. Run `npm run format`
1. `git add .`
1. `git commit -m 'install prettier'`

## Links

-   https://prettier.io/docs/en/install.html
-   https://prettier.io/docs/en/configuration.html
-   https://prettier.io/docs/en/ignore.html#ignoring-files-prettierignore
-   https://vueschool.io/articles/vuejs-tutorials/eslint-and-prettier-with-vite-and-vue-js-3/

## Project

[vue-ts](https://github.com/imomaliev/vue-ts)
