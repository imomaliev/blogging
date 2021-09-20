# Deploy to Github Pages with Github Actions

## Configure github workflow to deploy to github pages

1. Add deploy step for our `build.yml`
    ```diff
    +
    +      - name: Deploy
    +        # deploy only for version 16.x
    +        if: matrix.node-version == '16.x'
    +        uses: JamesIves/github-pages-deploy-action@4.1.4
    +        with:
    +          branch: gh-pages # The branch the action should deploy to.
    +          folder: dist # The folder the action should deploy.
    ```
1. `git add -u`
1. `git commit -m 'Add deploy to github pages step for github workflow'`

## Links

-   https://github.com/marketplace/actions/deploy-to-github-pages
-   https://docs.github.com/en/actions/learn-github-actions/managing-complex-workflows
-   https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

## Project

{% github https://github.com/imomaliev/vue-ts no-readme %}
