# GitHub Action for Hugo

This is a composite action, like described [here](https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/).

It checks out the site (with the private theme submodule), builds it with `hugo --gc --minify` and deploys `public/` with the official GitHub Pages deployment (`actions/upload-pages-artifact` + `actions/deploy-pages`). The repository's Pages source must be "GitHub Actions".

Usage in a site's `.github/workflows/publish-site.yml`:

```yaml
name: Publish site
on:
  push:
    branches:
      - main
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: pages
  cancel-in-progress: false
jobs:
  build:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.publish.outputs.page_url }}
    steps:
    - name: Checkout, build and deploy
      id: publish
      uses: Guite/hugo-action@v4
      with:
        access_token: ${{ secrets.CI_ACCESS_TOKEN }}
```

`v3` and older push to the `gh-pages` branch with a per-site deploy key instead.

Hugo and Dart Sass versions are pinned in `action.yml` and bumped by Renovate (see `renovate.json`). Before releasing a bump to the sites, build all sites with the new version (`hugo-maintenance` skill in `Guite/hugo-theme-guite`).
