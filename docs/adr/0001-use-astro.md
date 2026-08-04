# ADR 0001: Use Astro

## Context

The portfolio must be fast, accessible, bilingual, easy to maintain, and deployable without paid hosting.

## Decision

Use Astro with static output and minimal client-side JavaScript.

## Consequences

The site can be hosted directly on GitHub Pages, pages remain lightweight, and interactive features must be deliberately added.

## Alternatives considered

- Plain HTML and CSS: simpler initially but less structured as the portfolio grows.
- Next.js: capable but unnecessarily complex for a static portfolio.
- WordPress: introduces hosting and maintenance requirements.
