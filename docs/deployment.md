# Deployment

The portfolio is a static Astro site built from the same source for two hosts. GitHub Pages keeps the existing `/portfolio/` project path; Cloudflare Workers Static Assets serves the site from the root of `portfolio.forgenord.ca`. No server-side application code or Astro Cloudflare adapter is used.

## Build and local verification

Install dependencies and validate both output variants with the pinned Node.js container:

```bash
docker compose run --rm --user "$(id -u):$(id -g)" app npm ci
docker compose run --rm --user "$(id -u):$(id -g)" app npm run check
docker compose run --rm -e ASTRO_SITE_URL=https://patrickpaul-perso.github.io -e ASTRO_BASE_PATH=/portfolio --user "$(id -u):$(id -g)" app npm run build
docker compose run --rm --user "$(id -u):$(id -g)" app npm run build
docker compose run --rm --user "$(id -u):$(id -g)" app npx --no-install wrangler deploy --dry-run
```

Each build writes to `dist/`, so the Cloudflare build must run last before the Wrangler dry run. For browser checks, use the preview command in the README after the Cloudflare build. To preview the GitHub Pages build, rebuild with `ASTRO_BASE_PATH=/portfolio`, then run `docker compose run --rm --service-ports -e ASTRO_BASE_PATH=/portfolio --user "$(id -u):$(id -g)" app npm run preview -- --host 0.0.0.0` and open `http://localhost:4321/portfolio/`.

## GitHub Pages

The existing `.github/workflows/deploy.yml` sets `ASTRO_SITE_URL=https://patrickpaul-perso.github.io` and `ASTRO_BASE_PATH=/portfolio` for its build and publishes `dist/` with GitHub Actions. Keep **Settings → Pages → Build and deployment → Source** set to **GitHub Actions**.

The public address remains `https://patrickpaul-perso.github.io/portfolio/`. Verify `/portfolio/`, `/portfolio/en/`, `/portfolio/fr/`, and internal links after deployment. No repository rename or GitHub Pages custom domain is needed.

## Cloudflare Workers

`wrangler.jsonc` publishes `dist/` as Workers Static Assets. Wrangler is a local development dependency and runs inside Docker Compose.

Connect this repository to **Workers Builds** in the Cloudflare dashboard and select `main` as the production branch. Set the build command to `npm run build` and the deploy command to `npx wrangler deploy`; leave `ASTRO_BASE_PATH` unset. Associate `portfolio.forgenord.ca` with the Worker as a Cloudflare Custom Domain. The existing `forgenord.ca` site remains separate.

The Cloudflare repository connection and Worker custom hostname are external account changes and are not created by this repository. Once connected, verify `/`, `/en/`, `/fr/`, `/en/about/`, `/fr/about/`, and `/ai-usage/` on `portfolio.forgenord.ca`, including redirects, assets, and language selection.
