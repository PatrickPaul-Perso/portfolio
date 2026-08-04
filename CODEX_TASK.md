# Codex Implementation Task

## Objective

Complete and validate Milestone 0 so the repository builds successfully, deploys to GitHub Pages, and is ready for Milestone 1.

## Required reading

Before changing files, read:

1. `AGENTS.md`
2. `ENGINEERING_PRINCIPLES.md`
3. `ARCHITECTURE.md`
4. `AI_USAGE.md`
5. all files in `docs/adr/`

## Scope

Work only on the `milestone-0-foundation` branch.

1. Inspect the current Astro project structure.
2. Verify `package.json`, `astro.config.mjs`, `tsconfig.json`, and all source files are internally consistent.
3. Generate and commit `package-lock.json` if it is missing.
4. Run `npm install`, `npm run check`, and `npm run build`.
5. Fix all build, type, routing, and internal-link errors.
6. Confirm the GitHub Pages base path is `/portfolio`.
7. Confirm the default route detects the browser language and still provides a visible manual language switcher.
8. Confirm English and French routes work under `/portfolio/en/` and `/portfolio/fr/`.
9. Confirm the AI disclosure is visible and the AI transparency page is reachable.
10. Confirm the GitHub Actions workflow installs dependencies reproducibly and deploys `dist`.
11. Update documentation only where the implementation changes require it.

## Open-source perspective

Prefer open standards, portable solutions, self-hostable options, and minimal vendor lock-in when choices are otherwise equivalent. Do not remove accurate references to proprietary tools that are part of Patrick Paul's experience. Present Power BI as one applied analytics tool alongside open-source observability and data tools such as Grafana, InfluxDB, and Telegraf. Describe Node-RED, Losant, and Apache NiFi as prototype or exploratory experience unless stronger evidence exists in the repository.

## Change discipline

- Make small, focused commits.
- Use Conventional Commit messages.
- Do not combine unrelated fixes.
- Do not redesign the landing page in this milestone.
- Do not add dependencies unless they are required and documented.
- Do not merge the pull request.

## Definition of done

Milestone 0 is complete when:

- `npm ci` succeeds from a clean checkout.
- `npm run check` succeeds.
- `npm run build` succeeds.
- the generated routes and asset paths are compatible with GitHub Pages under `/portfolio/`.
- English and French content remain synchronized in structure.
- keyboard navigation and visible focus are preserved.
- reduced-motion preferences are respected where motion exists.
- AI transparency remains visible.
- documentation reflects the final implementation.
- the pull request contains a concise validation summary.

## Stop and ask for human input when

- a factual claim about Patrick Paul's experience is missing or ambiguous;
- a new paid service or proprietary dependency appears necessary;
- an architectural change conflicts with an existing ADR;
- a design decision would materially change the approved visual direction;
- credentials, secrets, a custom domain, or personal contact details are required.

## Final report

When finished, report:

- commits created;
- checks run and their results;
- files changed;
- remaining limitations;
- whether the pull request is ready for human approval.
