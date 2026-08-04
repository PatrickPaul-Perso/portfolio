# ADR 0004: Use bilingual static routes

## Context

The portfolio must support English and Canadian French on static hosting.

## Decision

Publish separate `/en/` and `/fr/` routes. Use a lightweight browser-language redirect at the project root and retain a visible manual language switcher.

## Consequences

Both languages are indexable and independently shareable. Content synchronization becomes an explicit maintenance responsibility.

## Alternatives considered

- Runtime translation: incompatible with the static, dependency-light approach.
- A single mixed-language page: less usable and less professional.
