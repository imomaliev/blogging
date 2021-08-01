# Install instructions and repo configuration

## Add project setup instructions

1. Add `Project Setup` section to our `README.md`

    ````diff
    -# Vue 3 + Typescript + Vite
    +# Vue 3 + Typescript + Vite + Jest

     This template should help get you started developing with Vue 3 and Typescript in Vite.

    +## Project setup
    +
    +Clone project with [`degit`](https://github.com/Rich-Harris/degit)
    +
    +```
    +degit user/repo
    +```
    +
    +### Install dependencies
    +
    +```
    +npm install
    +```
    +
    +### Compiles and hot-reloads for development
    +```
    +npm run dev
    +```
    +
    +### Compiles and minifies for production
    +```
    +npm run build
    +```
    +
    +### Preview build
    +```
    +npm run serve
    +```
    +
    +### Run your unit tests
    +```
    +npm run test
    +```
    +### Lint
    +```
    +npm run lint
    +```
    +### Fix files
    +```
    +npm run format
    +```
    +
     ## Recommended IDE Setup
    ````

1. Add `pre-commit` hooks installation instruction

    ````diff
    +## Install pre-commit hooks
    +```
    +pre-commit install
    +```
    +
    ````

1. `git add -u`
1. `git commit -m 'add install instructions'`

## Setup Depandabot notifications

1. Go to `Security -> Enable Dependabot alerts`
   ![Enable Dependabot alerts](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ngxvg1v48f97cp3qtfjf.png)
1. Enable `Dependabot alerts` and `Dependabot security updates`
   ![Configure security and analysis features](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jz1sctmfbuigyxoag3nw.png)

## Add `LICENSE`

1. In our github repo press `Add file -> Create new file`
   ![Create new file](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tavy58j340f8wjyfcc04.png)
1. Type `LICENSE` into `Name your file...` input.
1. Press appeared `Choose a license template` button.
   ![Choose a license template](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c2ad05wr3h9akk37blkn.png)
1. Select `MIT License` and press `Review and submit`.
1. In appeared commit form choose `Commit directly to the main branch.`
1. Press `Commit new file`

## Links

-   https://pre-commit.com/#3-install-the-git-hook-scripts
-   https://docs.github.com/en/code-security/supply-chain-security/managing-vulnerabilities-in-your-projects-dependencies/configuring-dependabot-security-updates
-   https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-license-to-a-repository

## Project

[vue-ts](https://github.com/imomaliev/vue-ts)
