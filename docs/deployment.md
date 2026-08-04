# Deployment

The production site is built and deployed by GitHub Actions after changes reach `main`.

## Expected URL

`https://patrickpaul-perso.github.io/portfolio/`

## Build output

Astro generates the static site in `dist/`. The workflow uploads that directory as the GitHub Pages artifact.

## Repository setting

GitHub Pages must use **GitHub Actions** as its source.
