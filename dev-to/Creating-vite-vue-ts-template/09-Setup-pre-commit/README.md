# Setup pre-commit

## Create pre-commit configuration

1. `pre-commit sample-config > .pre-commit-config.yaml`
1. Add prettier hook to `.pre-commit-config.yaml`
    ```diff
    +-   repo: https://github.com/pre-commit/mirrors-prettier
    +    rev: ''  # Use the sha / tag you want to point at
    +    hooks:
    +    -   id: prettier
    ```
1. Add eslint hook to `.pre-commit-config.yaml`
    ```diff
    +-   repo: https://github.com/pre-commit/mirrors-eslint
    +    rev: ''  # Use the sha / tag you want to point at
    +    hooks:
    +    -   id: eslint
    +        additional_dependencies:
    +        -   eslint@7.31.0
    +        -   typescript@4.3.5
    +        -   "@typescript-eslint/eslint-plugin@4.28.5"
    +        -   "@typescript-eslint/parser@4.28.5"
    +        -   eslint-plugin-vue@7.14.0
    +        -   vue-eslint-parser@7.9.0
    +        -   eslint-config-prettier@8.3.0
    ```
1. Update eslint hook to run for `*.js, *.jsx, *.ts, *.tsx and *.vue`

    > By default only \*.js files are taken into consideration. If you want to use eslint on TypeScript codebases you need to start from this template

    ```diff
         hooks:
         -   id: eslint
    +        files: \.([jt]sx?|vue)$  # *.js, *.jsx, *.ts, *.tsx and *.vue
    +        types: [file]
    ```

1. `git add .pre-commit-config.yaml`
1. `pre-commit autoupdate`
1. `pre-commit run --all-files`
1. `git add -u`
1. `git commit -m 'setup pre-commit'`

## Links

-   https://pre-commit.com
-   https://github.com/pre-commit/mirrors-prettier
-   https://github.com/pre-commit/mirrors-eslint

## Project

[vue-ts](https://github.com/imomaliev/vue-ts)
