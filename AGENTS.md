# Repository Guidelines

## Project Overview

`anthonny.fyi` is a plain, multi-page personal site. HTML, CSS, and the timeline's small inline script are served directly as static assets. Keep changes minimal and document-like; do not introduce a framework or build system for ordinary content work.

## Architecture & Data Flow

- `index.html` is the navigation hub. Directory routes resolve to their own `index.html`, such as `/about/`, `/timeline/`, and `/work/mchan/`.
- Content is hardcoded in each document. There is no API, backend, database, template engine, shared include system, or generated data.
- Pages repeat the home header and load the shared stylesheet from `css/style.css` or `/css/style.css`.
- `work/index.html` links to project detail pages; each detail page links back to `/work/`.
- `timeline/index.html` contains the only client-side behavior. Its async click handler copies `#timeline.innerText` with the Clipboard API and reports success or failure through the button text.
- There is no dependency injection or application state layer. State is limited to native DOM state such as `<details>` and the timeline button label.

## Key Directories

- `about/`: personal profile page.
- `timeline/`: chronological content and clipboard interaction.
- `work/`: project index and one directory per project.
- `css/`: shared site styling.
- `boilerplates/`: reusable static page starting point.

## Development Commands

No repository-defined scripts, build step, test command, linter, or formatter exist.

```sh
# Preview the repository root as a static site
python3 -m http.server 8000
# Then open http://127.0.0.1:8000/
```

- Build: none; source files are deployable assets.
- Test: none configured; use the browser QA checklist below.
- Lint/format: none configured; preserve existing formatting manually.
- Deploy: no command is documented. `wrangler.jsonc` configures Cloudflare static assets but does not define an invocation workflow.

## Code Conventions & Common Patterns

- Use plain semantic HTML and native browser features. Prefer `main`, headings, paragraphs, lists, links, `details`, and buttons over custom abstractions.
- Use lowercase HTML5 markup, `lang="en"`, UTF-8, viewport metadata, and two-space indentation.
- Routes use directory `index.html` files and slash-terminated root-relative links, for example `/work/moratea/`.
- Nested pages link `/css/style.css`; follow the nearest working page when creating or editing markup.
- Keep headings sparse and content compact. The visual style is intentionally close to browser defaults.
- Put shared visual rules in `css/style.css`; do not add page-specific CSS unless the behavior requires it.
- Keep JavaScript inline and minimal when a native interaction needs it. Follow `timeline/index.html`: query explicit IDs, use `async` only for the asynchronous browser API, and handle failure with `try`/`catch` plus visible text.
- Do not add client state management, dependency injection, modules, or error infrastructure unless the site gains a real need for them.
- Preserve factual project copy. Do not invent features, dates, metrics, technologies, or status claims.

## Important Files

- `index.html`: root entry point and filesystem-style navigation tree.
- `about/index.html`: representative prose-and-list content page.
- `timeline/index.html`: timeline content and the only JavaScript interaction.
- `work/index.html`: project navigation.
- `work/moratea/index.html`, `work/mchan/index.html`, `work/circuit-sim/index.html`: project detail documents.
- `css/style.css`: the only shared stylesheet.
- `boilerplates/page.html`: basic page skeleton; verify its stylesheet path when using it in a nested directory.
- `wrangler.jsonc`: Cloudflare configuration; `assets.directory` is `.` and no Worker entry point is configured.

## Runtime/Tooling Preferences

- Browsers are the application runtime. No Node.js, Bun, package manager, or application runtime is required by the repository.
- No `package.json`, lockfile, CI workflow, Dockerfile, Makefile, or task runner is present.
- Cloudflare Wrangler is the configured hosting tool, but its installation method and deploy command are not repository-defined. Do not add package metadata merely to edit or preview static files.
- Do not commit generated output; there is no generated-output directory or build artifact convention.

## Testing & QA

No automated tests, test framework, coverage tooling, browser runner, or coverage target are configured. For every visible change, preview the actual site in a browser at desktop and mobile widths, then check the affected path directly.

Minimum smoke checks:

- Open `/` and follow `/about/`, `/timeline/`, and `/work/`.
- Expand and collapse the root work `<details>` navigation.
- Follow all project links from `/work/` and each `Back to work` link.
- On `/timeline/`, click `Copy all`; verify the label becomes `Copied` and the clipboard contains the complete 2025 and 2026 timeline. Also preserve the `Copy failed` state for unavailable clipboard access.
- Check for broken internal links, horizontal overflow, unintended heading proliferation, and unsupported factual claims.
