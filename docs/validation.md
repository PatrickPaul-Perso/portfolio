# Validation Checklist

Before merging a feature or release:

- Install locked dependencies with `docker compose run --rm --user "$(id -u):$(id -g)" app npm ci` when setting up or updating dependencies.
- Run `docker compose run --rm --user "$(id -u):$(id -g)" app npm run check`.
- Run `docker compose run --rm -e ASTRO_SITE_URL=https://patrickpaul-perso.github.io -e ASTRO_BASE_PATH=/portfolio --user "$(id -u):$(id -g)" app npm run build` for GitHub Pages.
- Run `docker compose run --rm --user "$(id -u):$(id -g)" app npm run build` for Cloudflare.
- Start the built-site preview with `docker compose run --rm --service-ports --user "$(id -u):$(id -g)" app npm run preview -- --host 0.0.0.0` and open `http://localhost:4321/`.
- Verify English and French routes.
- Verify keyboard navigation and visible focus.
- Check narrow mobile and wide desktop layouts.
- Check reduced-motion behaviour.
- Confirm internal links work under `/portfolio/` on GitHub Pages and from `/` on Cloudflare.
- Review the generative AI notice when content or process changes.
