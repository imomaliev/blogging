# Install TailwindCSS

## Install and setup TailwindCSS

1. Start by following official [Install Tailwind CSS with Vue 3 and Vite](https://tailwindcss.com/docs/guides/vue-3-vite) instructions. Install `tailwindcss`.
    ```console
    $ npm install --save-dev tailwindcss@latest postcss@latest autoprefixer@latest
    ```
1. Create configuration files
    ```console
    $ npx tailwindcss init -p
    ```
1. Configure tree-shaking (removal of unused styles). Update `tailwind.config.js`.
    ```diff
    -  purge: [],
    +  purge: ['./index.html', './src/**/*.{js,jsx,ts,tsx,vue}'],
    ```
1. Create `index.css. `touch src/index.css`.
1. Update `src/index.css`
    ```diff
    +@tailwind base;
    +@tailwind components;
    +@tailwind utilities;
    ```
1. Ensure our css file is imported. Update `src/main.ts`
    ```diff
     import App from '@/App.vue'
    +import '@/index.css'
    ```
1. `git add -u && git add tailwind.config.js postcss.config.js src/index.css`
1. `git commit -m 'install tailwindcss'`

## Links

-   https://tailwindcss.com/docs/guides/vue-3-vite
-   https://postcss.org

## Project

[vue-ts-tailwind](https://github.com/imomaliev/vue-ts-tailwind)
