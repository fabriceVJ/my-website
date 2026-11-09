# Design

## Context

The working tree has the old placeholder site deleted but not yet committed. That site was one `index.html` with a centred card, a `style.css` (0xProto font, background `#1a1c20`, card `#2a2d33`, greys `#6b717e` / `#9aa0a8` / `#d0d2d6`) and the `media/fvj.svg` favicon. A Bun/TS scaffold (`package.json`, `index.ts`, `tsconfig.json`) was never used by the page. `.github/workflows/deploy.yml` (untracked) runs `bun run build` and publishes `./dist` with `peaceiris/actions-gh-pages`. No such build exists, and the workflow would drop the custom domain because `CNAME` is not in the published output. See proposal.md for the motivation and specs/ for the required behaviour.

## Goals / Non-Goals

**Goals:**
- Two hand-written files (`index.html`, `style.css`) that are easy to edit years from now without tooling.
- A content change (new project, skill, link) is a copy-paste of an existing HTML block, and the CSS never needs touching.
- Responsive with as few media queries as possible.

**Non-Goals:**
- No templating, data file or generator. Content lives directly in the HTML.
- No JavaScript at all, not even for a mobile menu.
- No light theme or theme toggle.

## Decisions

### 1. Plain HTML + CSS at the repo root, no build
Alternatives considered: Astro (data-driven, static output), Vite + TS with client rendering, Angular. Each one adds dependencies, a build that can break, and CI. Client rendering also hurts SEO. One page with roughly 10 projects doesn't need any of that. If the content grows a lot (or a PDF CV is ever wanted), moving the HTML into Astro later is cheap.

### 2. GitHub Pages via the official Actions workflow (no build)
The old Bun/`peaceiris` workflow is replaced by `.github/workflows/pages.yml`. On push to `main` (or a manual run) it copies an explicit allow-list (`index.html`, `style.css`, `CNAME`, `.nojekyll`, `media/`) into `_site/` and publishes that with `actions/configure-pages`, `upload-pages-artifact` and `deploy-pages`. Pages Source must be set to "GitHub Actions".

The original plan was "Deploy from a branch" with no workflow, which was simpler but has a real downside: it publishes the **whole repo root**, so `openspec/`, `.claude/` and `README.md` would be publicly reachable on fabrice-vj.ch. The allow-list avoids that and gives a visible deploy log, at the cost of one small YAML file. A new top-level file the page needs must be added to the copy step, which is noted in the workflow and README. With Actions deploys, the custom domain is stored in the Pages settings. `CNAME` is kept as a harmless record of it, and so the branch-deploy fallback still works. `.nojekyll` stays for the same reason.

### 3. Page skeleton and content blocks
```
<header>   site mark "fvj" + <nav> (about, skills, projects, cv)
<main>
  <section id="hero">      h1 name, role, intro, <ul class="links">
  <section id="about">     h2 + paragraphs
  <section id="skills">    h2 + <dl>: <dt>Backend</dt><dd><ul class="tags">...</ul></dd>
  <section id="projects">  h2 + <ul class="cards"> of <article>
  <section id="cv">        h2 + h3 Experience <ol class="timeline"> + h3 Education <ol class="timeline">
<footer>   (c) year, domain
```
- **Profile links**: one `<li><a href="..." target="_blank" rel="noopener noreferrer">GitHub</a></li>` per link, as **text labels** (with a small "↗" marker) rather than brand icons. This fits the minimal monospace look, needs no SVG assets, and makes adding GitLab literally one line. The same link list is reused in the hero. The nav links only to sections, so it stays short on phones.
- **Experience vs. education**: two `h3` sub-lists inside one "CV" section, which makes the difference explicit (spec: distinguishable) without icons. Entries use `<time>` for the period.
- **Projects**: each card is an `<article>` with `h3`, `p`, a `.tags` list, and an optional links row that is simply omitted when empty.
- Commented-out template blocks at the top of each repeating list show the exact markup to copy.

### 4. Theme via CSS custom properties
All colours, spacing and font sizes are variables on `:root`. Palette (dark only, `color-scheme: dark`):
| token | value | use |
|---|---|---|
| `--bg` | `#1a1c20` | page background |
| `--surface` | `#2a2d33` | cards |
| `--text` | `#d0d2d6` | body text |
| `--muted` | `#9aa0a8` | secondary text, dates |
| `--border` | `#3a3e46` | hairlines |
| `--accent` | `#7fb4ca` (muted cyan, final value tuned in implementation) | links, focus, hover |

The old `#6b717e` grey fails 4.5:1 on `#1a1c20`, so it is only used for borders and decoration, never for text. All text colours are checked against `--bg` and `--surface`.

### 5. Responsive approach: mobile-first, fluid, one breakpoint
- Container `max-width: 70ch`, side padding `clamp(1rem, 5vw, 3rem)`.
- Type sizes use `clamp()` (e.g. the h1 is roughly `clamp(2rem, 6vw, 3.25rem)`).
- Project cards use `grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr))`, so they reflow without a query. The container for projects may be wider than the text column.
- Tags, links and nav use `flex-wrap: wrap` + `gap`.
- One breakpoint (`min-width: 40rem`) puts the skills label beside its tags and timeline dates beside their entries, and makes the header nav sticky.
- `scroll-behavior: smooth` and hover transitions are applied only inside `@media (prefers-reduced-motion: no-preference)`.

### 6. Self-host the 0xProto font
The old page loaded it from `fonts.cdnfonts.com`. Instead, ship `media/fonts/0xProto-Regular.woff2` (and Bold if used) with `@font-face` + `font-display: swap`. 0xProto is SIL OFL 1.1, so redistribution is allowed, and the licence file goes next to the font. This avoids a third-party request (privacy, uptime), and the font stack still falls back to `ui-monospace, SFMono-Regular, Menlo, Consolas, monospace`.

### 7. Logo, favicons and link previews; no web app manifest
The FvJ icon set lives in `media/icons/`. `favicon.svg` is used both as the tab icon and as the header logo (an `<img alt="">` inside the "Back to top" link, replacing the earlier "fvj" text). `favicon.ico` is the fallback and `apple-touch-icon.png` the iOS home-screen icon. Open Graph + `twitter:card=summary` tags use the square `icon-512.png` as preview image. Alternative: a dedicated 1200×630 preview image for LinkedIn's large card layout, deferred until one exists (it's a one-line swap). A `site.webmanifest` was deliberately **not** added: nobody installs a CV page as an app, and Android's "Add to Home screen" already falls back to the apple-touch-icon. `icon-192.png` / `icon-512.png` stay in the repo so a manifest can be added later without regenerating them.

## Risks / Trade-offs

- [Content duplicated in HTML is repetitive to edit] → Template comments in each list. Volume is small, and moving to a generator stays an option.
- [Pages source not switched in repo settings, so the site keeps serving the old gh-pages branch or nothing] → A tasks.md step to switch it manually and verify the live domain afterwards.
- [Removing `CNAME` from the published source could reset the custom domain] → `CNAME` is restored in the same commit that switches deployment.
- [Accent colour fails contrast on `--surface`] → Verify against both backgrounds during implementation and adjust the value.
- [Placeholder content accidentally goes live] → Placeholders are marked `TODO:` and the final task is a grep for `TODO` before pushing.

## Migration Plan

1. Implement on a branch, preview locally (`python3 -m http.server` or just opening the file).
2. Merge to `main` in one commit that removes the Bun files and old workflow and adds the site, `CNAME`, `.nojekyll` and `.github/workflows/pages.yml`.
3. In GitHub → Settings → Pages: Source = "GitHub Actions". Set the custom domain to `fabrice-vj.ch` and turn on "Enforce HTTPS". Check the run in the Actions tab is green.
4. Check https://fabrice-vj.ch.
5. Rollback: revert the commit (the workflow republishes the previous state), or re-run an earlier successful deploy from the Actions tab.

## Open Questions

- The real content (intro, about, skill list, projects, jobs, education, profile URLs) comes from Fabrice. Placeholders are fine until then.
- The exact accent hue is a taste decision that can be tuned once the page is visible.
