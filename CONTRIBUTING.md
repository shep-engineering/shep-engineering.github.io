# Contributing to David Sheppard's personal portfolio site

This is a small personal site (static HTML / CSS / JavaScript) deployed
via GitHub Pages at https://shep-engineering.github.io. Most of what's
here reflects personal work choices, so the bar for "what belongs" is
narrower than a general-purpose project — but useful contributions are
welcome.

## What contributions make sense

- **Bug fixes** — broken links, layout issues on specific devices,
  accessibility regressions, dead images.
- **Small enhancements** — dark-mode polish, contrast tweaks, subtle
  animation fixes, mobile-layout improvements.
- **Documentation** — fixing typos, clarifying `README.md` or
  `DEPLOYMENT.md`.

## What probably doesn't

- Content rewrites (the "about me" text, project descriptions,
  career-narrative copy) — these are personal and not open to
  outside edits.
- Large structural rewrites of the site scaffold.
- Adding new frameworks, build systems, or tooling — the site is
  intentionally plain static HTML/CSS/JS.

If you're unsure whether something fits, open an issue first.

## How to contribute

1. **Fork** `shep-engineering/shep-engineering.github.io` on GitHub.
2. **Clone your fork** and branch from `main`:
   ```bash
   git clone git@github.com:<your-user>/shep-engineering.github.io.git
   cd shep-engineering.github.io
   git checkout -b fix/short-description
   ```
3. **Make your change.** Keep commits focused — one logical change per PR.
4. **Test locally.** Open `index.html` directly in a browser; verify
   both light and dark themes render correctly, mobile viewport is
   clean, and no console errors appear.
5. **Open a PR** against `main`. A short description of what you
   changed and why is plenty.

## What to expect on merge

- PRs are reviewed against `shep-engineering/shep-engineering.github.io`
  (the repo you forked from).
- This is a mirror of a private-side source repo. When your PR merges,
  the change is reconciled into the private source as well, so your
  contribution persists across future publishes.
- Responses in days-to-a-week range — this is a personal site, not a
  product.
- Attribution in the commit log is preserved; your name stays on your
  change.

## Style

- HTML / CSS / JS without build tooling. No bundlers, no TypeScript,
  no frameworks.
- 2-space indent in HTML/CSS; 4-space indent in JS (matches existing
  code).
- Keep the JavaScript small and dependency-free.

## Commit messages

Short, descriptive imperatives. Conventional-commit prefixes
(`fix:`, `feat:`, `docs:`) are nice but not required.

## License

By submitting a PR, you agree your contribution is licensed under the
[MIT License](./LICENSE) to match the project.
