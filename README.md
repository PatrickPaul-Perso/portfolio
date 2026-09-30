# Patrick Paul — Professional Portfolio

A bilingual professional portfolio focused on technical infrastructure, Linux, automation, industrial IoT, edge processing, data sovereignty, and practical delivery for small and mid-sized organizations.

## Repository goals

- Showcase technical expertise through practical projects and engineering outcomes.
- Demonstrate professional, maintainable software engineering practices.
- Demonstrate responsible AI-assisted development with human review and accountability.
- Build an accessible, responsive bilingual portfolio.
- Remain fully deployable on GitHub Pages without paid hosting.
- Prefer open-source technologies, open standards, and portable architectures when practical.

## Technology

- Astro
- TypeScript
- Semantic HTML
- Modern CSS
- GitHub Actions
- GitHub Pages
- Cloudflare Workers Static Assets

## Local development

Docker Compose is the development environment. The Node.js image is pinned in `compose.yaml`, and npm dependencies are locked in `package-lock.json`. Install dependencies and run Node.js, npm, and Astro inside the container; no global or host Node.js installation is needed.

From the repository root:

```bash
docker compose run --rm --user "$(id -u):$(id -g)" app npm ci
docker compose run --rm --service-ports --user "$(id -u):$(id -g)" app
```

Open `http://localhost:4321/`. Stop the development server with Ctrl+C.

## Build and usability checks

Run the project checks and default Cloudflare static build inside the same container. The GitHub Pages `/portfolio/` build command is in the [deployment instructions](./docs/deployment.md):

```bash
docker compose run --rm --user "$(id -u):$(id -g)" app npm run check
docker compose run --rm --user "$(id -u):$(id -g)" app npm run build
```

To inspect the built site in a browser, start Astro's preview server:

```bash
docker compose run --rm --service-ports --user "$(id -u):$(id -g)" app npm run preview -- --host 0.0.0.0
```

Open `http://localhost:4321/` and follow the [validation checklist](./docs/validation.md): check mobile and desktop layouts, English and French pages, language switching, keyboard navigation and visible focus, reduced motion, and internal links from the site root. Stop the preview server with Ctrl+C. After changing dependencies, update `package-lock.json` with npm in the container and repeat `npm ci`, `npm run check`, and `npm run build`.

## Documentation

- [AI agent guidelines](./AGENTS.md)
- [Architecture](./ARCHITECTURE.md)
- [Engineering principles](./ENGINEERING_PRINCIPLES.md)
- [Contributing](./CONTRIBUTING.md)
- [Generative AI usage](./AI_USAGE.md)
- [Dependency health](./docs/dependency-health.md)
- [Roadmap](./ROADMAP.md)
- [Architecture decision records](./docs/adr/)

## Deployment

The site is built from the same source for both hosts. GitHub Actions keeps `https://patrickpaul-perso.github.io/portfolio/` working for existing printed links; Cloudflare Workers Builds will serve `https://portfolio.forgenord.ca/` from the root after its repository connection and custom hostname are configured. The [deployment instructions](./docs/deployment.md) show how to validate both build variants.
