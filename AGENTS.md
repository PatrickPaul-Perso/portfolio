# AI Agent Guidelines

## Purpose

This repository is both a professional portfolio and a demonstration of disciplined software engineering. Every change should improve the visitor experience, the maintainability of the codebase, or the clarity of the documentation.

## Primary assistant

ChatGPT is the primary generative AI assistant used for this project. Do not add tool-specific instruction files for assistants that are not used.

## Core principles

- Prefer clarity over cleverness.
- Prefer maintainability over novelty.
- Prefer accessibility over visual effects.
- Prefer static generation whenever possible.
- Prefer open-source technologies, open standards, and portable architectures when they satisfy the requirement.
- Avoid unnecessary dependencies and vendor lock-in.
- Keep the site fast on desktop and mobile.
- Keep documentation in English.
- Keep English and French site content synchronized.

## Open-source perspective

The portfolio should consistently reflect practical experience with open and interoperable platforms.

- Present open-source tools as the preferred foundation when they are reliable and appropriate.
- Favour solutions that can be self-hosted, inspected, automated, and migrated.
- Emphasize interoperability, documented interfaces, and standard protocols.
- Do not hide relevant proprietary-platform experience, but describe it in context rather than making it the centre of the technical identity.
- When discussing data visualization and telemetry, include experience with Grafana, InfluxDB, and Telegraf alongside Power BI.
- Describe Node-RED, Losant, and Apache NiFi accurately as tools used in prototype or experimental work unless stronger production evidence is provided.
- Avoid overstating proficiency, production scale, or operational responsibility.

## Change discipline

- Make small, targeted, incremental changes.
- Keep one logical concern per commit.
- Do not mix refactoring with feature work unless required.
- Avoid large rewrites when a focused change is sufficient.
- Every push must leave the repository buildable and coherent.
- Use concise Conventional Commit messages.

## Architecture

- Use Astro with static output.
- Use semantic HTML and modern CSS.
- Use client-side JavaScript only when it adds clear value.
- Keep components focused and easy to review.
- Avoid duplicated content and duplicated CSS.
- Justify every new dependency.

## Accessibility

Target WCAG 2.2 AA.

- Support keyboard navigation.
- Preserve visible focus indicators.
- Maintain sufficient contrast.
- Respect `prefers-reduced-motion`.
- Use meaningful alternative text.
- Preserve a logical heading hierarchy.
- Never communicate meaning with colour alone.

## Performance

- Target Lighthouse scores above 95 where practical.
- Minimize JavaScript.
- Optimize images and reserve their display dimensions.
- Lazy-load non-critical media.
- Avoid layout shifts.
- Prefer SVG for simple icons and decorative graphics.

## Internationalization

- English is the source language for documentation.
- The website supports English and French.
- Browser language may select the initial route.
- A visible language switcher must always remain available.
- Store an explicit user language choice locally.
- Never mix English and French within the same content block.

## Generative AI transparency

- Disclose that generative AI assisted with writing, design exploration, documentation, and software development.
- Require human review before publication.
- Keep technical decisions and factual validation human-owned.
- Do not present generated content as independently verified.

## Validation before commit

Run the applicable checks:

```bash
npm run check
npm run build
```

Also verify responsive behaviour, keyboard navigation, language switching, reduced-motion behaviour, and internal links when affected.
