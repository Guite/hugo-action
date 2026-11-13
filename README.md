# GitHub Action for Hugo

This is a composite action, like described [here](https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/).

Hugo and Dart Sass versions are pinned in `action.yml` and bumped by Renovate (see `renovate.json`). Before releasing a bump to the sites, build all sites with the new version (`hugo-maintenance` skill in `Guite/hugo-theme-guite`).
