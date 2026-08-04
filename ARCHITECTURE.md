# Architecture

## Overview

The portfolio is a statically generated Astro website deployed to GitHub Pages.

## Key decisions

- Astro provides static generation with minimal client-side JavaScript.
- GitHub Actions builds and publishes the `dist` directory.
- English and French use separate routes.
- Browser language selects the initial route while a visible switcher remains available.
- CSS defines a dark, accessible, responsive design system.
- Generative AI usage is disclosed in the site footer and supporting documentation.

## Constraints

- No paid hosting services.
- No server-side runtime.
- No required external database.
- Dependencies must be limited and justified.
