# Architecture

## Overview

The portfolio is a statically generated Astro website configured for GitHub Pages and Cloudflare Workers Static Assets.

## Key decisions

- Astro provides static generation with minimal client-side JavaScript.
- GitHub Actions publishes `dist/` to GitHub Pages; Cloudflare Workers Builds publishes the same static output through Wrangler.
- English and French use separate routes.
- Browser language selects the initial route while a visible switcher remains available.
- CSS defines a dark, accessible, responsive design system.
- Generative AI usage is disclosed in the site footer and supporting documentation.

## Constraints

- No paid hosting services.
- No server-side application code.
- No required external database.
- Dependencies must be limited and justified.
