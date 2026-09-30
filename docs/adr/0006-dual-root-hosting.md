# ADR 0006: Dual static hosting with host-specific base paths

## Context

ADR 0002 selected GitHub Pages at `https://patrickpaul-perso.github.io/portfolio/`. That URL appears on printed business cards and must keep working. The portfolio also needs a Cloudflare deployment at the root of `portfolio.forgenord.ca`.

## Decision

Keep Astro static output and build the same source for two hosts with different base paths. The GitHub Pages workflow sets `ASTRO_BASE_PATH=/portfolio` and continues to publish to the existing project URL. Cloudflare Workers Builds leaves `ASTRO_BASE_PATH` unset, so Astro uses `/` and Wrangler publishes `dist/` as Workers Static Assets.

This decision extends ADR 0002 with a second host while preserving its GitHub Pages URL. ADR 0002 remains as the record of the original hosting choice.

## Consequences

- GitHub Pages keeps `/portfolio/`, `/portfolio/en/`, and `/portfolio/fr/`; the printed address remains valid.
- Cloudflare serves `/`, `/en/`, and `/fr/` on `portfolio.forgenord.ca` after the Worker and hostname are connected.
- Both deployments retain the same page structure, language redirects, and static assets, generated with the correct base path for each host.
- Cloudflare Workers Builds needs a one-time repository connection and custom hostname setup. The site needs no application server or Astro Cloudflare adapter.

## Alternatives considered

- Rename this repository to the account's `github.io` site: breaks the printed project-site address.
- Use a custom domain for GitHub Pages: changes the published address without solving the need to preserve the printed URL.
- Use one root-path build on both hosts: creates broken absolute links on the GitHub Pages project URL.
