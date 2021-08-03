# Create repo from `vue-ts` template

## Generate repo from template

1. In our previous series [Creating vite vue ts template](https://dev.to/imomaliev/series/13845) we created [`vue-ts`](https://github.com/imomaliev/vue-ts) template. We will use it to create our new `vue-ts-tailwind` template.
1. Start by pressing `+` in github's navbar and select `New repository`.
   ![New repository](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hll0ioxr5yy5tlgmyuh7.png)
1. Select `vue-ts` as `Repository template` and check `Include all branches`.
1. Set `Repository name` to `vue-ts-tailwind` and press `Create repository`.
   ![Create repo from vue-ts template](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/whhkxw8l98sxr56qza6e.png)

## Configure github repository

1. Make this repo a `Template repository` as we did in {% link https://dev.to/imomaliev/github-project-template-1mc3 %}
1. Enable Depandabot alerts {% link https://dev.to/imomaliev/creating-vite-vue-ts-template-install-instructions-and-repo-configuration-779-temp-slug-4634241 %}

## Update project to mention TailwindCSS

1. Update badges and title in `README.md`.

    ```diff
    -[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/imomaliev/vue-ts/main.svg)](https://results.pre-commit.ci/latest/github/imomaliev/vue-ts/main)
    -![ci](https://github.com/imomaliev/vue-ts/actions/workflows/ci.yml/badge.svg)
    +[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/imomaliev/vue-ts-tailwind/main.svg)](https://results.pre-commit.ci/latest/github/imomaliev/vue-ts-tailwind/main)
    +![ci](https://github.com/imomaliev/vue-ts-tailwind/actions/workflows/ci.yml/badge.svg)

    -# Vue 3 + Typescript + Vite + Jest
    +# Vue 3 + Typescript + Vite + Jest + TailwindCSS

    -This template should help get you started developing with Vue 3 and Typescript in Vite.
    +This template should help get you started developing with Vue 3, Typescript and TailwindCSS in Vite.
    ```

1. Update project `name` and `deploy` script in `package.json`

    ```diff
     {
    -  "name": "vite-vue-typescript-starter",
    +  "name": "vite-vue-typescript-tailwind-starter",
       "version": "0.0.0",
       "scripts": {
         "dev": "vite",
         "build": "vue-tsc --noEmit && vite build",
    -    "deploy": "vue-tsc --noEmit && vite build --base '/vue-ts/'",
    +    "deploy": "vue-tsc --noEmit && vite build --base '/vue-ts-tailwind/'",
    ```

1. Add TailwindCSS to components
   In `src/App.vue`

    ```diff
    -  <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" />
    +  <HelloWorld msg="Hello Vue 3 + TypeScript + Vite + Tailwind" />
    ```

    and in `src/components/HelloWorld.vue`

    ```diff
         >
    +    |
    +    <a href="https://tailwindcss.com/docs/installation" target="_blank"
    +      >TailwindCSS Docs</a
    +    >
       </p>
    ```

1. Update `package-lock.json`
    ```console
    $ npm install
    ```
1. `git add -u`
1. `git commit -m 'mention tailwind'`

## Links

-   https://tailwindcss.com/docs
-   https://dev.to/imomaliev/github-project-template-1mc3
-   https://dev.to/imomaliev/creating-vite-vue-ts-template-install-instructions-and-repo-configuration-779-temp-slug-4634241

## Project

[vue-ts-tailwind](https://github.com/imomaliev/vue-ts-tailwind)
