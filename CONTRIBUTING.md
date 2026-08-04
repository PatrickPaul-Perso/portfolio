# Contributing

## Workflow

1. Create a focused branch from `main`.
2. Make one logical change at a time.
3. Run `npm run check` and `npm run build`.
4. Review responsive behaviour and accessibility when affected.
5. Use a concise Conventional Commit message.
6. Open a pull request with a clear summary and validation notes.

## Branch naming

Use short, descriptive, English branch names with one of these prefixes:

```text
foundation/
feature/
fix/
docs/
refactor/
chore/
release/
```

Examples:

```text
foundation/milestone-0
feature/homepage-hero
fix/github-pages-routing
docs/branch-conventions
```

Do not rename an active branch without a clear operational reason. Preserve existing pull request history when the current name is already understandable and compliant.

## Commit examples

```text
feat: add project card component
fix: preserve language selection
style: improve mobile navigation spacing
docs: record deployment decision
```

Do not combine unrelated features, broad refactoring, and documentation cleanup in one change.
