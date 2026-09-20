# Dependency Health

## Assessment scope

Assessment date: 2026-09-20

Commands:

```bash
npm audit
npm audit fix
npm outdated
npm ci
npm run check
npm run build
```

The repository declares `astro`, `@astrojs/check`, and `typescript` under `dependencies`. npm therefore classifies their complete trees as production dependencies. Operationally, they are build-time tools: GitHub Pages receives generated static HTML, CSS, JavaScript, and assets, not `node_modules` or the Astro development server.

## Vulnerability summary after compatible remediation

| npm category | Critical | High | Moderate | Low |
| --- | ---: | ---: | ---: | ---: |
| Production dependencies | 1 | 1 | 0 | 1 |
| Development dependencies | 0 | 0 | 0 | 0 |

`npm audit fix` safely updated compatible transitive dependencies and reduced the audit from eight vulnerable packages to three. The remaining findings require Astro 7.3.3, a framework-major upgrade that is outside this content-focused change.

## Compatible updates applied

The synchronized lockfile now resolves patched versions of:

- `devalue` 5.9.4
- `fast-uri` 3.1.8
- `js-yaml` 4.3.2
- `nanoid` 3.3.19
- `svgo` 4.1.0
- their compatible transitive selector dependencies

These packages are used during development or static generation and are not shipped as server-side runtime dependencies on GitHub Pages.

## Remaining vulnerable packages

### Astro

- Current version: 5.18.2
- Classification: direct dependency used to build the static site
- npm severity: Critical
- Ships to GitHub Pages: No; only generated static output ships
- Fix available: Astro 7.3.3
- Requires major upgrade: Yes
- Decision: Deferred pending a focused, human-approved framework migration

The audit includes XSS, path handling, host-header, and server-island advisories, plus [GHSA-26w7-cxv4-gfx2](https://github.com/advisories/GHSA-26w7-cxv4-gfx2), a critical AVIF image-optimization issue. This portfolio uses repository-controlled static content, no server islands, and a prebuilt WebP portrait rather than an AVIF optimization pipeline. Those constraints reduce current exposure but do not replace the need for a supported framework upgrade.

### sharp

- Current version: 0.34.5
- Classification: optional transitive dependency of Astro used at build time
- npm severity: High
- Ships to GitHub Pages: No
- Fix available: Through the Astro 7.3.3 migration
- Decision: Deferred with the framework migration

The affected native image-processing library remains installed during builds, but the current site does not invoke an Astro raster-image optimization pipeline.

### esbuild

- Current version: 0.27.7
- Classification: transitive Astro build and local-development tool
- npm severity: Low
- Ships to GitHub Pages: No
- Fix available: Through the Astro 7.3.3 migration
- Decision: Deferred with the framework migration

The advisory applies to the Windows development server. The deployed static site is unaffected.

## Dependency status

- Updated packages: Five vulnerable transitive packages plus compatible selector dependencies through `npm audit fix`.
- Deferred packages: Astro 7.3.3 and its `sharp` and `esbuild` dependency updates.
- Outdated direct packages: Astro 5.18.2 (latest 7.3.3) and TypeScript 5.9.3 (latest 7.0.2).
- Current compatible direct packages: `@astrojs/check` 0.9.10, Astro 5.18.2, and TypeScript 5.9.3.
- Lockfile: Synchronized and reproducible through `npm ci`.

## Validation

- `npm ci`: Passed
- `npm run check`: Passed with zero errors, warnings, or hints
- `npm run build`: Passed; six static routes generated
- GitHub Pages base path: Preserved at `/portfolio`

## Risk decision

No forced or framework-major update is appropriate in this pull request. The site remains a static GitHub Pages deployment, the affected packages do not execute for visitors, and the available complete remediation requires an Astro major migration. Patrick’s approval is required before starting that dedicated migration.
