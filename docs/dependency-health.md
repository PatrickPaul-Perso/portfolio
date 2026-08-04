# Dependency Health

## Assessment scope

Assessment date: 2026-08-04

Commands:

```bash
npm audit
npm outdated
```

The repository declares `astro`, `@astrojs/check`, and `typescript` under `dependencies`. npm therefore classifies their complete trees as production dependencies. Operationally, they are build-time tools: GitHub Pages receives the generated static HTML, CSS, JavaScript, and assets, not `node_modules` or the Astro development server.

## Vulnerability summary

| npm category | Critical | High | Moderate | Low |
| --- | ---: | ---: | ---: | ---: |
| Production dependencies | 0 | 2 | 0 | 1 |
| Development dependencies | 0 | 0 | 0 | 0 |

The package-level totals above follow npm's audit classification. Individual Astro advisories include high, moderate, and low findings, but npm reports the direct `astro` package once at its highest transitive severity.

## Vulnerable packages

### Astro

- Package: `astro`
- Current version: 5.18.2
- Classification: direct production dependency; used only to build this static site
- npm severity: High
- Ships to GitHub Pages: No; only generated static output ships
- Fix available: Yes, Astro 7.1.6
- Requires major upgrade: Yes
- Estimated implementation risk: High because two framework major versions, build behavior, integrations, generated output, and all localized routes require migration validation
- Rationale for deferring: Astro 5.18.2 is the newest version allowed by the current compatible range. The audit fix is outside the permitted update scope, and forced remediation is prohibited.
- Future remediation strategy: Evaluate Astro 7 in a focused, human-approved migration pull request; review both major-version guides, update the lockfile normally, rerun the full engineering health report, and regression-test static routing, localization, accessibility, and GitHub Pages deployment.

Advisories:

| Advisory | Severity | Affected range | Recommended version |
| --- | --- | --- | --- |
| [GHSA-j687-52p2-xcff](https://github.com/advisories/GHSA-j687-52p2-xcff) — incomplete `</script>` sanitization in `define:vars` | Moderate | `<6.1.6` | Astro 7.1.6 |
| [GHSA-xr5h-phrj-8vxv](https://github.com/advisories/GHSA-xr5h-phrj-8vxv) — server-island parameter replay | Low | `<6.1.10` | Astro 7.1.6 |
| [GHSA-8hv8-536x-4wqp](https://github.com/advisories/GHSA-8hv8-536x-4wqp) — reflected XSS through an unescaped slot name | High | `<6.3.3` | Astro 7.1.6 |
| [GHSA-2pvr-wf23-7pc7](https://github.com/advisories/GHSA-2pvr-wf23-7pc7) — Host-header SSRF in a prerendered error-page fetch | High | `<6.4.6` | Astro 7.1.6 |
| [GHSA-jrpj-wcv7-9fh9](https://github.com/advisories/GHSA-jrpj-wcv7-9fh9) — XSS through unescaped spread-attribute names | Moderate | `<6.4.6` | Astro 7.1.6 |
| [GHSA-4g3v-8h47-v7g6](https://github.com/advisories/GHSA-4g3v-8h47-v7g6) — reflected XSS through View Transition animation properties | Moderate | `>=2.9.0 <=7.0.9` | Astro 7.1.6 |
| [GHSA-f48w-9m4c-m7f5](https://github.com/advisories/GHSA-f48w-9m4c-m7f5) — incomplete spread-attribute XSS fix | Moderate | `<7.0.6` | Astro 7.1.6 |
| [GHSA-7pw4-f3q4-r2p2](https://github.com/advisories/GHSA-7pw4-f3q4-r2p2) — XSS through hydrated-island transition directives | Low | `>=3.10.0 <7.0.4` | Astro 7.1.6 |

The current portfolio uses static generation, repository-controlled content, and no server islands. Those constraints reduce exposure, but they do not remove the need for a future supported-framework upgrade.

### sharp

- Package: `sharp`
- Current version: 0.34.5
- Classification: optional transitive production dependency of Astro; build-time image processing only
- Advisory: [GHSA-f88m-g3jw-g9cj](https://github.com/advisories/GHSA-f88m-g3jw-g9cj) — inherited libvips vulnerabilities
- Severity: High
- Ships to GitHub Pages: No
- Fix available: Yes, sharp 0.35.0; npm recommends resolving it through Astro 7.1.6
- Requires major upgrade: Yes in the current dependency tree because Astro 5 restricts sharp to `^0.34.0`, and pre-1.0 minor releases are semver-breaking
- Estimated implementation risk: High when addressed through the required Astro major migration
- Rationale for deferring: No compatible Astro 5 resolution is available, and adding an override would bypass the framework's tested dependency range.
- Future remediation strategy: Resolve through the focused Astro major migration and validate image generation before and after the upgrade.

The portfolio currently publishes no optimized raster-image pipeline. This lowers immediate exposure, while the vulnerable native package remains installed during builds.

### esbuild

- Package: `esbuild`
- Current version: 0.27.7
- Classification: transitive production dependency of Astro; build and local-development tooling only
- Advisory: [GHSA-g7r4-m6w7-qqqr](https://github.com/advisories/GHSA-g7r4-m6w7-qqqr) — arbitrary file read through the Windows development server
- Severity: Low
- Ships to GitHub Pages: No
- Fix available: Yes, esbuild 0.28.1; npm recommends resolving it through Astro 7.1.6
- Requires major upgrade: Yes in the current dependency tree because Astro 5 restricts esbuild to `^0.27.3`, and pre-1.0 minor releases are semver-breaking
- Estimated implementation risk: High when addressed through the required Astro major migration; immediate deployed-site risk is Low because the development server is not published
- Rationale for deferring: No compatible version satisfies Astro 5's declared range, and forced or override-based remediation is prohibited.
- Future remediation strategy: Upgrade through the focused Astro major migration; until then, bind local preview servers to loopback and avoid exposing development servers to untrusted users.

## Dependency status

- Updated packages: None. `npm outdated` found no patch or compatible minor updates.
- Deferred packages: Astro 7.1.6, sharp 0.35.0, and esbuild 0.28.1 because remediation requires a framework-major migration.
- Outdated packages: Astro 5.18.2 (latest 7.1.6) and TypeScript 5.9.3 (latest 7.0.2). Both available upgrades are major versions and are outside this pull request's scope.
- Current compatible packages: `@astrojs/check` 0.9.10, Astro 5.18.2, and TypeScript 5.9.3.
- Unused dependencies: None identified. Astro powers the development and build scripts, `@astrojs/check` powers the check script, and TypeScript supports Astro's type checking.
- Lockfile: `package-lock.json` is synchronized and reproducible through `npm ci`.

## Risk decision

No dependency update is appropriate in this pull request. The site remains a static GitHub Pages deployment, the affected packages do not ship to visitors, and the available remediation would violate the explicit prohibition on major framework upgrades. Patrick's approval is required before starting the dedicated Astro migration.
