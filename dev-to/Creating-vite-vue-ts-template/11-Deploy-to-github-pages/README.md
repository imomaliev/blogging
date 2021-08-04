# Deploy to Github Pages

## Setup project for Github Pages integration

1. Configure `vite` by setting correct `base` option. Update `vite.config.js`

    > If you are deploying to `https://<USERNAME>.github.io/<REPO>/`, for example your repository is at `https://github.com/<USERNAME>/<REPO>`, then set `base` to `'/<REPO>/'`.

    ```diff
     export default defineConfig({
       plugins: [vue()],
    +  base: '/vue-ts/',
    ```

1. `git add -u`
1. `git commit -m "update vite's 'base' option for github pages"`
1. Prepare our sources `npm run bulid` on `main` branch.
1. Let's setup `gh-pages` branch that will contain our site source. From docs:

    > The default publishing source for project sites is the root of the `gh-pages` branch.

    ```console
    # Create a new branch, with no history or contents, called gh-pages and switches to the gh-pages branc
    $ git checkout --orphan gh-pages
    ```

1. Clear the index and the working tree right after creating the orphan branch.
    ```console
    $ git rm -rf .
    ```
1. Put `dist/` folder contents into root of a project.
    ```console
    mv dist/* . &&  rmdir dist/
    ```
1. `git add assets/ favicon.ico index.html`
1. `git commit -m 'deploy' --no-verify`. We are adding `--no-verify` here to skip pre-commit checks, which will fail because we have deleted `.pre-commit-config.yaml` from this branch.

## Deploy to Github Pages with Github Actions

{% link https://dev.to/imomaliev/creating-vite-vue-ts-template-deploy-to-github-pages-with-github-actions-b7 %}

## Links

-   https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages
-   https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll
-   https://vitejs.dev/guide/static-deploy.html#github-pages
-   https://cli.vuejs.org/guide/deployment.html#github-pages
-   https://pre-commit.com/#temporarily-disabling-hooks

## Project

{% github https://github.com/imomaliev/vue-ts no-readme %}
