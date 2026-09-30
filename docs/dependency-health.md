# Dependency Health

## Assessment scope

Assessment date: 2026-09-30

Commands:

```bash
docker compose run --rm --user "$(id -u):$(id -g)" app npm audit
docker compose run --rm --user "$(id -u):$(id -g)" app npm outdated
docker compose run --rm --user "$(id -u):$(id -g)" app npm ci
docker compose run --rm --user "$(id -u):$(id -g)" app npm run check
docker compose run --rm -e ASTRO_SITE_URL=https://patrickpaul-perso.github.io -e ASTRO_BASE_PATH=/portfolio --user "$(id -u):$(id -g)" app npm run build
docker compose run --rm --user "$(id -u):$(id -g)" app npm run build
docker compose run --rm --user "$(id -u):$(id -g)" app npx --no-install wrangler deploy --dry-run
```

The repository declares `astro`, `@astrojs/check`, and `typescript` under `dependencies`. npm therefore classifies their complete trees as production dependencies. Operationally, they are build-time tools: both hosts receive generated static HTML, CSS, JavaScript, and assets, not `node_modules` or the Astro development server. Wrangler 4.145.0 is a development dependency used only for Cloudflare deployment.

## Vulnerability summary after compatible remediation

| npm category | Critical | High | Moderate | Low |
| --- | ---: | ---: | ---: | ---: |
| Production dependencies | 1 | 1 | 0 | 1 |
| Development dependencies | 0 | 0 | 0 | 0 |

A previous compatible remediation reduced the audit from eight vulnerable packages to three. The 2026-09-30 audit after adding Wrangler still reports the same three packages: one critical, one high, and one low. The complete fix requires Astro 7.3.5, a framework-major upgrade that remains deferred.

## Compatible updates applied

The synchronized lockfile now resolves patched versions of:

- `devalue` 5.9.4
- `fast-uri` 3.1.8
- `js-yaml` 4.3.2
- `nanoid` 3.3.19
- `svgo` 4.1.0
- their compatible transitive selector dependencies

These packages are used during development or static generation and are not shipped as server-side runtime dependencies on either host.

## Remaining vulnerable packages

### Astro

- Current version: 5.18.2
- Classification: direct dependency used to build the static site
- npm severity: Critical
- Ships to either host: No; only generated static output ships
- Fix available: Astro 7.3.5
- Requires major upgrade: Yes
- Decision: Deferred pending a focused, human-approved framework migration

The audit includes XSS, path handling, host-header, and server-island advisories, plus [GHSA-26w7-cxv4-gfx2](https://github.com/advisories/GHSA-26w7-cxv4-gfx2), a critical AVIF image-optimization issue. This portfolio uses repository-controlled static content, no server islands, and a prebuilt WebP portrait rather than an AVIF optimization pipeline. Those constraints reduce current exposure but do not replace the need for a supported framework upgrade.

### sharp

- Current version: 0.34.5
- Classification: optional transitive dependency of Astro used at build time
- npm severity: High
- Ships to either host: No
- Fix available: Through the Astro 7.3.5 migration
- Decision: Deferred with the framework migration

The affected native image-processing library remains installed during builds, but the current site does not invoke an Astro raster-image optimization pipeline.

### esbuild

- Current version: 0.27.7
- Classification: transitive Astro build and local-development tool
- npm severity: Low
- Ships to either host: No
- Fix available: Through the Astro 7.3.5 migration
- Decision: Deferred with the framework migration

The advisory applies to the Windows development server. The deployed static site is unaffected.

## Dependency status

- Updated packages: Added Wrangler 4.145.0 as a local development dependency for Cloudflare deployment. The previously updated transitive packages remain in the lockfile.
- Deferred packages: Astro 7.3.5 and its `sharp` and `esbuild` dependency updates.
- Outdated direct packages: Astro 5.18.2 (latest 7.3.3) and TypeScript 5.9.3 (latest 7.0.2).
- Current compatible direct packages: `@astrojs/check` 0.9.10, Astro 5.18.2, TypeScript 5.9.3, and Wrangler 4.145.0.
- Lockfile: Synchronized and reproducible through `npm ci`.

## Validation

- `npm ci`: Passed
- `npm run check`: Passed with zero errors, warnings, or hints
- `npm run build`: Passed for both `/portfolio/` and `/`; ten static routes generated per build
- `wrangler deploy --dry-run`: Passed; 28 files read from `dist/`
- Hosting: GitHub Pages retains `/portfolio/`; Cloudflare uses `/` after its Worker and hostname are connected

## Risk decision

No forced or framework-major update is appropriate in this pull request. The site remains static on GitHub Pages and Cloudflare Workers, the affected packages do not execute for visitors, and the available complete remediation requires an Astro major migration. Patrick’s approval is required before starting that dedicated migration.
