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

## Definition of ready

A change is ready for implementation when:

- the intended outcome is clear;
- the scope is limited to one coherent concern;
- required content and factual claims are available;
- no unresolved user decision blocks implementation;
- the change does not conflict with an accepted ADR;
- validation criteria are identified;
- affected English and French content is identified.

Stop and ask for clarification when these conditions are not met.

## Change discipline

- Make small, targeted, incremental changes.
- Keep one logical concern per commit.
- Do not mix refactoring with feature work unless required.
- Avoid large rewrites when a focused change is sufficient.
- Every push must leave the repository buildable and coherent.
- Every pull request should leave the repository in a slightly better state than it was found.
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

## Definition of done

A change is complete when:

- the requested outcome is implemented without unrelated changes;
- applicable checks pass;
- responsive and keyboard behaviour are preserved;
- accessibility and reduced-motion requirements are preserved;
- internal links and GitHub Pages base paths remain valid;
- English and French structures remain synchronized;
- documentation and ADRs are updated when required;
- the pull request includes the Standard Engineering Health Report defined below;
- the pull request includes a `Suggested AGENTS.md improvements` section that proposes repeatable improvements or explicitly states `None.`;
- every dependency update leaves the repository deployable and has been validated with `npm ci`, `npm run check`, and `npm run build`.

## Validation before commit

Run the applicable checks:

```bash
npm run check
npm run build
```

Also verify responsive behaviour, keyboard navigation, language switching, reduced-motion behaviour, and internal links when affected.

## Pull Request Requirements

Every pull request must:

- remain focused on one coherent objective;
- explain the completed implementation and current pull request status;
- identify known limitations, remaining risks, and decisions that require Patrick's approval;
- preserve a buildable, deployable state after every commit;
- include the Standard Engineering Health Report as part of the Definition of Done;
- include a section named `Suggested AGENTS.md improvements` that either proposes repeatable project practices or explicitly states `None.`;
- remain unmerged until the required human approval has been provided.

## Standard Engineering Health Report

Every pull request must include the following report, using these section names and covering every listed item.

### Summary

- objective
- implementation completed
- pull request status

### Validation

Always report:

- `npm ci`
- `npm run check`
- `npm run build`

Also summarize:

- responsive verification
- localization verification
- accessibility verification
- internal-link verification

### Engineering Health

#### Dependency vulnerabilities

Separate production dependencies from development dependencies. For each category report:

- Critical
- High
- Moderate
- Low

#### Dependency status

Report:

- updated packages
- deferred packages
- outdated packages

#### Build quality

Report:

- build status
- check status
- generated routes
- GitHub Pages compatibility

### Accessibility

Summarize:

- keyboard navigation
- visible focus
- semantic landmarks
- reduced motion
- colour contrast

### Performance

Summarize:

- JavaScript footprint
- bundle-size impact
- image optimization
- Lighthouse regressions when results are available

### Technical debt

List all remaining technical debt, including:

- deferred dependency upgrades
- pending framework upgrades
- framework limitations
- future refactoring opportunities

### Documentation

List every documentation file updated.

### Risks

List any remaining risks.

### Human approval required

Explicitly list every decision requiring Patrick's approval.

### Recommendation

Finish with exactly one of:

- `READY FOR REVIEW`
- `READY TO MERGE`
- `HUMAN DECISION REQUIRED`
- `NOT READY`

## Dependency maintenance policy

- Run `npm audit` and `npm outdated` when assessing dependency health or changing dependencies.
- Classify each vulnerability as production or development, state whether the affected code ships to GitHub Pages, and record severity, fix availability, major-version requirements, and implementation risk.
- Apply patch and compatible minor updates when validation shows they are safe.
- Do not apply framework or build-tool major upgrades without explicit human approval and a focused migration plan.
- Never use `npm audit fix --force`.
- Do not add overrides solely to hide or bypass an advisory.
- After every dependency update, run `npm ci`, `npm run check`, and `npm run build` before committing.
- Keep `package-lock.json` synchronized and document deferred vulnerabilities in `docs/dependency-health.md`.
- Confirm that declared dependencies are used and that generated files are not accidentally committed.

## Documentation expectations

- Update only documentation affected by the change.
- Keep `CHANGELOG.md` focused on user-visible or engineering-significant changes.
- Use `docs/devlog.md` to record implementation context and validation outcomes.
- Maintain `docs/dependency-health.md` whenever known vulnerabilities remain.
- Update ADRs only for durable architecture decisions; do not use them as routine change logs.
- Keep technical documentation in English and ensure it remains consistent with the implementation.

## Pull request quality expectations

- Make the report evidence-based: distinguish completed validation from assumptions and unavailable measurements.
- Report zero-count vulnerability categories instead of omitting them.
- Distinguish packages installed for the build from assets actually published to the static site.
- State deferred work explicitly instead of implying that it was fixed.
- Keep the pull request description synchronized with the latest commit and validation results.

## Continuous improvement expectations

Recurring engineering practices should automatically be incorporated into `AGENTS.md` when they become repeatable project practices.

Automatic changes must not modify the following without explicit human approval:

- project vision;
- engineering principles;
- architecture rules;
- accessibility requirements;
- security requirements;
- localization strategy;
- Git workflow.
