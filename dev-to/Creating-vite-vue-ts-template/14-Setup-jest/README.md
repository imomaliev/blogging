# Setup Jest

## Install and configure jest

1. We are using `typescript` in our project. To properly setup `jest` we would need to install [`ts-jest`](https://kulshekhar.github.io/ts-jest/) package as well.
    ```console
    $ npm install --save-dev jest ts-jest @types/jest
    ```
1. `git add -u`
1. `git commit -m 'install jest'`
1. Initialize our `ts-jest` config.
    ```console
    $ npx ts-jest config:init
    ```
1. Add `test` script in `package.json`
    ```diff
     "format": "prettier --write .",
    -    "lint": "eslint . --ext .js,.jsx,.ts,.tsx,.vue"
    +    "lint": "eslint . --ext .js,.jsx,.ts,.tsx,.vue",
    +    "test": "jest"
    ```
1. `git add package.json jest.config.js`
1. `git commit -m 'add jest config'`

## Configure jest for vue

1. To make jest and `vue` work together we will need `vue-jest` package. Recently it was split into `vue2-jest` and [`vue3-jest`](https://www.npmjs.com/package/vue3-jest) (we will use this one), which are currently in alfa. But we still going to use it because this is the only version that supports `jest >= 27.x`. Also for better testing experience with `vue` we will install [`@vue/test-utils`](https://github.com/vuejs/vue-test-utils-next) -

    > official testing utility library for Vue.js

    ```console
    $ npm install --save-dev vue3-jest@27.0.0-alpha.2 @vue/test-utils@next
    ```

1. Update `jest.config.js`
    ```diff
       testEnvironment: 'node',
    +  transform: {
    +    '^.+\\.vue$': 'vue3-jest',
    +  },
    +  moduleFileExtensions: ['json', 'js', 'jsx', 'ts', 'tsx', 'vue']
    ```
1. `git add -u`
1. `git commit -m 'install vue-jest and @vue/test-utils'`

## Add tests

1. `mkdir -p tests/unit`
1. `touch tests/unit/HelloWorld.spec.ts`
1. Add our test in `tests/unit/HelloWorld.spec.ts`
    ```diff
    +import { shallowMount } from '@vue/test-utils'
    +import HelloWorld from '@/components/HelloWorld.vue'
    +
    +describe('HelloWorld.vue', () => {
    +  it('renders props.msg when passed', () => {
    +    const msg = 'new message'
    +    const wrapper = shallowMount(HelloWorld, {
    +      props: { msg },
    +    })
    +    expect(wrapper.text()).toMatch(msg)
    +  })
    +})
    ```
1. `git add -u`
1. `git commit -m 'add test'`
1. Run test.
    ```console
    $ npm run test
    ```

### Fix `error TS7016: Could not find a declaration file for module '@vue/test-utils'`

1. If running tests causes this

    ```console
    $ npm run test

    > vite-vue-typescript-starter@0.0.0 test
    > jest

     FAIL  tests/unit/HelloWorld.spec.ts
      ● Test suite failed to run

        tests/unit/HelloWorld.spec.ts:1:30 - error TS7016: Could not find a declaration file for module '@vue/test-utils'. '/path/to/project/vue-ts/node_modules/@vue/test-utils/dist/vue-test-utils.cjs.js' implicitly has an 'any' type.
          Try `npm i --save-dev @types/vue__test-utils` if it exists or add a new declaration (.d.ts) file containing `declare module '@vue/test-utils';`

        1 import { shallowMount } from '@vue/test-utils'
                                       ~~~~~~~~~~~~~~~~~

    Test Suites: 1 failed, 1 total
    Tests:       0 total
    Snapshots:   0 total
    Time:        3.376 s
    Ran all test suites.
    ```

1. This is due a bug in version `2.0.0-rc.11` which was fixed in `2.0.0-rc.12`.
    - https://github.com/vuejs/vue-test-utils-next/releases/tag/v2.0.0-rc.12
    - https://github.com/vuejs/vue-test-utils-next/issues/799
    - https://github.com/vuejs/vue-test-utils-next/pull/800
1. Update to newer version of `@vue/test-utils`.
    ```console
    $ npm install --save-dev @vue/test-utils@2.0.0-rc.12
    ```
1. `git add -u`
1. `git commit -m 'fix: TS7016 missing declaration file for @vue/test-utils by updating it to 2.0.0-rc.12'`

### Fix `Cannot find module '@/components/HelloWorld.vue' from 'tests/unit/HelloWorld.spec.ts'`

1. If running tests causes

    ```console
    $ npm run test

    > vite-vue-typescript-starter@0.0.0 test
    > jest

     FAIL  tests/unit/HelloWorld.spec.ts
      ● Test suite failed to run

        Cannot find module '@/components/HelloWorld.vue' from 'tests/unit/HelloWorld.spec.ts'

          1 | import { shallowMount } from '@vue/test-utils'
        > 2 | import HelloWorld from '@/components/HelloWorld.vue'
            | ^
          3 |
          4 | describe('HelloWorld.vue', () => {
          5 |   it('renders props.msg when passed', () => {

          at Resolver.resolveModule (node_modules/jest-resolve/build/resolver.js:311:11)
          at Object.<anonymous> (tests/unit/HelloWorld.spec.ts:2:1)

    Test Suites: 1 failed, 1 total
    Tests:       0 total
    Snapshots:   0 total
    Time:        2.735 s
    Ran all test suites.
    ```

1. This issue occurs because `jest` cannot resolve `@/` path.
    - https://kulshekhar.github.io/ts-jest/docs/getting-started/paths-mapping
    - https://jestjs.io/docs/configuration#modulenamemapper-objectstring-string--arraystring
1. Update `jest.config.js` to fix this.
    ```diff
    +  moduleNameMapper: {
    +    '^@/(.*)$': '<rootDir>/src/$1',
    +  },
    ```
1. `git add -u`
1. `git commit -m "fix: jest can't find @/ path"`

### Fix `ReferenceError: document is not defined`

1. If running tests causes

    ```console
    $ npm run test

    > vite-vue-typescript-starter@0.0.0 test
    > jest

     FAIL  tests/unit/HelloWorld.spec.ts
      HelloWorld.vue
        ✕ renders props.msg when passed (2 ms)

      ● HelloWorld.vue › renders props.msg when passed

        The error below may be caused by using the wrong test environment, see https://jestjs.io/docs/configuration#testenvironment-string.
        Consider using the "jsdom" test environment.

        ReferenceError: document is not defined

           5 |   it('renders props.msg when passed', () => {
           6 |     const msg = 'new message'
        >  7 |     const wrapper = shallowMount(HelloWorld, {
             |                     ^
           8 |       props: { msg },
           9 |     })
          10 |     expect(wrapper.text()).toMatch(msg)

          at mount (node_modules/@vue/test-utils/dist/vue-test-utils.cjs.js:7640:14)
          at Object.shallowMount (node_modules/@vue/test-utils/dist/vue-test-utils.cjs.js:7852:12)
          at Object.<anonymous> (tests/unit/HelloWorld.spec.ts:7:21)

    Test Suites: 1 failed, 1 total
    Tests:       1 failed, 1 total
    Snapshots:   0 total
    Time:        4.061 s
    Ran all test suites.
    ```

1. As error message suggests we could fix this error by updating `jest.config.js`
    ```diff
    -  testEnvironment: 'node',
    +  testEnvironment: 'jsdom',
    ```
1. `git add -u`
1. `git commit -m 'fix: using wrong env for jest'`

## Run tests in Github Actions

1. Rename `bulid.yml` to `ci.yml` to be more general on contents of this workflow.
    ```console
    $ git mv .github/workflows/{build,ci}.yml
    ```
1. Update `.github/workflow/ci.yml`

    ```diff
    -name: Node.js CI
    +name: CI

     on:
       push:
    @@ -28,6 +28,7 @@ jobs:
               cache: 'npm'
           - run: npm ci
           - run: npm run build
    +      - run: npm run test
    ```

1. Update badge in `README.md`
    ```diff
    -![build](https://github.com/imomaliev/vue-ts/actions/workflows/build.yml/badge.svg)
    +![ci](https://github.com/imomaliev/vue-ts/actions/workflows/ci.yml/badge.svg)
    ```
1. `git add -u`
1. `git commit -m 'setup github workflow to run tests'`

## Links

-   https://jestjs.io
-   https://kulshekhar.github.io/ts-jest/
-   https://github.com/vuejs/vue-jest
-   https://www.npmjs.com/package/vue3-jest
-   https://next.vue-test-utils.vuejs.org/installation/
-   https://github.com/lmiller1990/vtu-next-demo

## Project

{% github https://github.com/imomaliev/vue-ts no-readme %}
