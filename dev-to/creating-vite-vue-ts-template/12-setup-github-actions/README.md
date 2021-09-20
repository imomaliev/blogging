# Setup Github Actions

## Configure Github Actions for `bulid`

1. Let start by setting up `Node.js` workflow.
1. Go to `Actions` tab in your project and find `Node.js` workflow.
   ![Node.js workflow](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yzjisuy78qq5cglbqi1u.png)

    (it may be hidden under ` More continuous integration workflows...`)
    ![More continuous integration workflows](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rz0adjloi6zy5wi022lk.png)
    and press `Set up this workflow` button.

1. Rename `node.js.yml` to `build.yml`. Commit `build.yml` with `Start commit` button. Add `Create .github/workflows/build.yml` commit message.
   ![Commit build.yml](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cp3vel0ny4un0fy1ka7m.png)

### On commit `pre-commit.ci` may fail because of `prettier` formatting.

1. `git pull`
1. `pre-commit run --all-files`
1. `git add -u`
1. `git commit -m 'fix: prettier formating'`

### Update `.github/workflows/build.yml`

1. We do not have tests yet and `build` is present in `package.json`
    ```diff
           - run: npm ci
    -      - run: npm run build --if-present
    -      - run: npm test
    +      - run: npm run build
    ```
1. `git add -u`
1. `git commit -m 'do not run npm test for build workflow'`

### Add badge

1. Add `![build](https://github.com/<OWNER>/<REPOSITORY>/actions/workflows/build.yml/badge.svg)` to README.md. From docs

    > You reference the workflow by the name of your workflow file.
    >
    > ```markdown
    > ![example workflow](https://github.com/<OWNER>/<REPOSITORY>/actions/workflows/<WORKFLOW_FILE>/badge.svg)
    > ```

1. `git add -u`
1. `git commit -m 'add build workflow badge'`

## Links

-   https://docs.github.com/en/actions
-   https://docs.github.com/en/actions/guides/setting-up-continuous-integration-using-workflow-templates
-   https://github.com/actions/setup-node
-   https://github.com/actions/starter-workflows/blob/main/ci/node.js.yml

## Project

{% github https://github.com/imomaliev/vue-ts no-readme %}
