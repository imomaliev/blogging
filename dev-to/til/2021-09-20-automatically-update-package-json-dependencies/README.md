# Automatically update `package.json` dependencies

## How to automatically update npm packages versions

### Question

During chore update of my [vue-ts template](https://github.com/imomaliev/vue-ts) dependencies (to learn more about it, read [here](https://dev.to/imomaliev/series/13845)) I was doing usual npm "upgrade" steps.

1. Run `npm update` to automatically update my packages to the latest versions
   From docs:
    > This command will update all the packages listed to the latest version (specified by the tag config), respecting the semver constraints of both your package and its dependencies (if they also require the same package).
1. Run `npm outdated` - to see what could be still updated.

`npm update` - only updates `package-lock.json` and does not change `package.json`. I started searching for a way to automatically update my dependencies in `package.json` file as well.

### Answer

Quick searching pointed me to [this stackoverflow post](https://stackoverflow.com/questions/16073603/how-to-update-each-dependency-in-package-json-to-the-latest-version), where one of the answers suggested using [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) tool.

1. `npm -g install npm-check-updates`
1. `ncu` to see outdated versions or `ncu --upgrade` to update the `package.json`.

### Links

-   https://github.com/imomaliev/vue-ts
-   https://stackoverflow.com/questions/16073603/how-to-update-each-dependency-in-package-json-to-the-latest-version
-   https://www.npmjs.com/package/npm-check-updates

## Fix `TS2307: Cannot find module 'src' or its corresponding type declarations.`

### Problem

After I updated my `package.json` and installed all dependencies, my `npm run build` started failing with

```console
$ npm run build

> vite-vue-typescript-starter@0.0.0 build
> vue-tsc --noEmit && vite build

node_modules/@vue/test-utils/dist/domWrapper.d.ts:5:28 - error TS2307: Cannot find module 'src' or its corresponding type declarations.

5 import { VueWrapper } from 'src';
                             ~~~~~


Found 1 error.
```

### Solution

This was a tricky one because at a first glance it may seem that I have a typescript problem in project which is technically correct, but actually this is a [bug](https://github.com/vuejs/vue-test-utils-next/issues/936) in `@vue/test-utils-next` library which was introduced in `2.0.0-rc.14` version. Installing `2.0.0-rc.13` or setting `skipLibCheck: true` in `tsconfig.json` solves this. For my case I've chosen the first approach.

### Learned

1. [`skipLibCheck: true`](https://www.typescriptlang.org/tsconfig#skipLibCheck)
    > Skip type checking of declaration files.

### Links

-   https://github.com/vuejs/vue-test-utils-next/issues/936
-   https://www.typescriptlang.org/tsconfig#skipLibCheck
