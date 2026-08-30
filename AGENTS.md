# Repository Guidelines

## Project Overview

`anthonny.fyi` is a plain, multi-page personal site. HTML and CSS are served
directly as static assets. Keep changes minimal and document-like; do not
introduce JavaScript behavior, a framework, or a build system.

## Architecture & Data Flow

- `index.html` is the navigation hub. Directory routes resolve to their own
  `index.html`, such as `/about/`, `/timeline/`, and `/work/mchan/`.
- Content is hardcoded in each document. There is no API, backend, database,
  template engine, shared include system, or generated data.
- Every content directory receives an `index.html`. Pages repeat the home
  header, include a `main` region, and load `/css/style.css`.
- Current projects appear in `work/` before archived games in `work/games/` and
  older projects in `work/older/`.
- Every page has a specific description meta tag and a canonical URL on
  `https://anthonny-fyi.pages.dev/`. Internal links are slash-terminated,
  root-relative URLs.

## Key Directories

- `about/`: personal profile page.
- `timeline/`: chronological content.
- `work/`: current project index and detail pages.
- `work/games/`: archived game pages.
- `work/older/`: archived earlier-work pages.
- `css/`: shared site styling.
- `boilerplates/`: reusable static page starting point.

## Development Commands

No repository-defined scripts, build step, test command, linter, or formatter
exist.

```sh
# Preview the repository root as a static site
python3 -m http.server 8000
# Then open http://127.0.0.1:8000/
```

- Build: none; source files are deployable assets.
- Test: none configured.
- Lint/format: none configured; preserve existing formatting manually.
- Deploy: no command is documented. `wrangler.jsonc` configures Cloudflare
  static assets but does not define an invocation workflow.

## Code Conventions & Common Patterns

- Use plain semantic HTML, `lang="en"`, UTF-8, viewport metadata, headings,
  paragraphs, lists, and links.
- Use lowercase HTML5 markup and two-space indentation.
- Use directory `index.html` files and slash-terminated root-relative links.
- Nested pages load `/css/style.css`; follow the nearest working page when
  creating or editing markup.
- Keep headings sparse and content compact. The visual style is intentionally
  close to browser defaults. Do not add page-specific CSS.
- Keep copy factual. Do not invent features, dates, metrics, technologies,
  status claims, or private repository links.

## Important Files

- `index.html`: root entry point and filesystem-style navigation tree.
- `about/index.html`: representative prose-and-list content page.
- `timeline/index.html`: chronological milestone document.
- `work/index.html`: current project navigation.
- `work/games/index.html`: archived game navigation.
- `work/older/index.html`: archived earlier-work navigation.
- `css/style.css`: the only shared stylesheet.
- `boilerplates/page.html`: basic page skeleton.
- `wrangler.jsonc`: Cloudflare configuration; `assets.directory` is `.` and no
  Worker entry point is configured.

## Runtime/Tooling Preferences

- Browsers are the application runtime. No Node.js, Bun, package manager, or
  application runtime is required by the repository.
- No `package.json`, lockfile, CI workflow, Dockerfile, Makefile, or task
  runner is present.
- Cloudflare Wrangler is the configured hosting tool, but its installation
  method and deploy command are not repository-defined. Do not add package
  metadata merely to edit or preview static files.
- Do not commit generated output; there is no generated-output directory or
  build artifact convention.

## Testing & QA

No automated tests, test framework, coverage tooling, or browser runner is
configured. For visible changes, preview the actual site at desktop and mobile
widths and check the affected paths directly.

Minimum smoke checks:

- Open `/` and follow `/about/`, `/timeline/`, `/work/`, `/work/games/`, and
  `/work/older/`.
- Follow project links from each project index and each back link.
- Check for broken internal links, horizontal overflow, unintended heading
  proliferation, valid metadata, and unsupported factual claims.
