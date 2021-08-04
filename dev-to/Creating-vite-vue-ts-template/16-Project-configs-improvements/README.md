# Project configs improvements

## Improve configs

1. Update `tsconfig.json`.
    ```diff
         "esModuleInterop": true,
    -    "lib": ["esnext", "dom"]
    +    "lib": ["esnext", "dom"],
    +    "baseUrl": ".",
    +    "paths": {
    +      "@/*": ["src/*"]
    +    }
       },
    -  "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"]
    +  "include": [
    +    "src/**/*.ts",
    +    "src/**/*.d.ts",
    +    "src/**/*.tsx",
    +    "src/**/*.vue",
    +    "tests/**/*.ts",
    +    "tests/**/*.tsx"
    +  ]
     }
    ```
1. Now we can update our code to use `@` as root of a local import path.

    In `src/App.vue`

    ```diff
    -import HelloWorld from './components/HelloWorld.vue'
    +import HelloWorld from '@/components/HelloWorld.vue'
    ```

    In `src/main.ts`

    ```diff
    -import App from './App.vue'
    +import App from '@/App.vue'
    ...
    -  <img alt="Vue logo" src="./assets/logo.png" />
    +  <img alt="Vue logo" src="@/assets/logo.png" />
    ```

1. `git add -u`
1. `git cim 'update tsconfig: add tests to include and use @ as root'`
1. But if we run our dev server we will get this error

    ```console
    $ npm run dev

    > vite-vue-typescript-starter@0.0.0 dev
    > vite

     > html:/path/to/project/vue-ts/src/App.vue:3:23: error: Could not resolve "@/components/HelloWorld.vue" (the plugin "vite:dep-scan" didn't set a resolve directory)
        3 │ import HelloWorld from '@/components/HelloWorld.vue'
          ╵                        ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    error when starting dev server:
    Error: Build failed with 1 error:
    html:/path/to/project/vue-ts/src/App.vue:3:23: error: Could not resolve "@/components/HelloWorld.vue" (the plugin "vite:dep-scan" didn't set a resolve directory)
        at failureErrorWithLog (/path/to/project/vue-ts/node_modules/esbuild/lib/main.js:1449:15)
        at /path/to/project/vue-ts/node_modules/esbuild/lib/main.js:1131:28
        at runOnEndCallbacks (/path/to/project/vue-ts/node_modules/esbuild/lib/main.js:921:63)
        at buildResponseToResult (/path/to/project/vue-ts/node_modules/esbuild/lib/main.js:1129:7)
        at /path/to/project/vue-ts/node_modules/esbuild/lib/main.js:1236:14
        at /path/to/project/vue-ts/node_modules/esbuild/lib/main.js:609:9
        at handleIncomingPacket (/path/to/project/vue-ts/node_modules/esbuild/lib/main.js:706:9)
        at Socket.readFromStdout (/path/to/project/vue-ts/node_modules/esbuild/lib/main.js:576:7)
        at Socket.emit (node:events:394:28)
        at Socket.emit (node:domain:475:12)
    ```

### Fix `error: Could not resolve "@/components/HelloWorld.vue" (the plugin "vite:dep-scan" didn't set a resolve directory)`

1. Add `resolve` config to `vite.config.js`
    ```diff
    +  resolve: {
    +    alias: [{ find: '@', replacement: '/src' }],
    +  },
    ```
1. `git add -u`
1. `git commit -m 'fix: vite not able to resolve @/'`

## Use `base: '/vue-ts/'` only for deployment

1. Delete `base` from `vite.config.js`
    ```diff
       plugins: [vue()],
    -  base: '/vue-ts/',
       resolve: {
         alias: [{ find: '@', replacement: '/src' }],
       },
    ```
1. Add `deploy` script to `package.json`
    ```diff
         "build": "vue-tsc --noEmit && vite build",
    +    "deploy": "vue-tsc --noEmit && vite build --base '/vue-ts/'",
         "serve": "vite preview",
    ```
1. Update github workflow

    ```diff
    @@ -15,7 +15,7 @@ jobs:

         strategy:
           matrix:
    -        node-version: [12.x, 14.x, 16.x]
    +        node-version: [14.x, 16.x]
             # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

         steps:
    @@ -30,6 +30,8 @@ jobs:
           - run: npm run build
           - run: npm run test

    +      - run: npm run deploy
    +        if: matrix.node-version == '16.x'
           - name: Deploy
             # deploy only for version 16.x
             if: matrix.node-version == '16.x'
    ```

1. `git add -u`
1. `git commit -m 'use vite base option only for deployment'`

## Add links to TypeScript and Jest docs

1. Update `src/componments/HelloWorld.vue`
    ```diff
         <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Docs</a>
         |
    -    <a href="https://www.typescriptlang.org/docs/" target="_blank">TypeScript Docs</a>
    +    <a href="https://www.typescriptlang.org/docs/" target="_blank"
    +      >TypeScript Docs</a
    +    >
         |
    -    <a href="https://jestjs.io/docs/getting-started" target="_blank">Jest Docs</a>
    +    <a href="https://jestjs.io/docs/getting-started" target="_blank"
    +      >Jest Docs</a
    +    >
    ```
1. `git add -u`
1. `git commit -m 'add links to typescript and jest docs'`

## Delete unused styles

1. After code review I've found that `vue-ts` template for Vite contains unused styles for `label` tag.
1. Remove unused styles in `src/component/HelloWorld.vue`

    ```diff
    diff --git a/src/components/HelloWorld.vue b/src/components/HelloWorld.vue
    index b09f889..0504d43 100644
    --- a/src/components/HelloWorld.vue
    +++ b/src/components/HelloWorld.vue
    @@ -64,11 +64,6 @@ a {
       color: #42b983;
     }

    -label {
    -  margin: 0 0.5em;
    -  font-weight: bold;
    -}
    -
     code {
       background-color: #eee;
       padding: 2px 4px;
    ```

1. `git add -u`
1. `git commit -m 'delete unused styles for label'`

## Links

-   https://vitejs.dev/config/#resolve-alias

## Project

{% github https://github.com/imomaliev/vue-ts no-readme %}
