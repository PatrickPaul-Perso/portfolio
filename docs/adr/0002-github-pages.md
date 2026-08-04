# ADR 0002: Deploy with GitHub Pages

## Context

The portfolio requires public, reliable hosting without a paid service or server runtime.

## Decision

Build the Astro site with GitHub Actions and publish the generated `dist` directory to GitHub Pages.

## Consequences

Deployment is automatic after changes reach `main`. The website must remain fully static and use the `/portfolio` base path.

## Alternatives considered

- Cloudflare Pages: strong option but adds another service.
- Netlify or Vercel: capable but unnecessary for the current requirements.
- Self-hosting: creates avoidable operational overhead.
