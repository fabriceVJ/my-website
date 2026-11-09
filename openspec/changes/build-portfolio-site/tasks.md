# Tasks

## 1. Repository cleanup

- [x] 1.1 Confirm removal of the Bun/TS scaffold and unused files (`package.json`, `bun.lock`, `tsconfig.json`, `index.ts`, `media/fvj-test.svg`, `.gitignore.txt`, `.github/workflows/deploy.yml`); verify with `git status` that they show as deleted and that the `.github/` directory is gone
- [x] 1.2 Restore `CNAME` (`fabrice-vj.ch`), `LICENSE` and `media/fvj.svg` from `HEAD`; verify `cat CNAME` prints `fabrice-vj.ch` and the favicon file exists
- [x] 1.3 Add an empty `.nojekyll` at the repo root and trim `.gitignore` to entries that still apply (OS/editor files); verify with `git status` that only intended files are listed
- [x] 1.4 Add `.github/workflows/pages.yml` (official Pages actions; on push to `main` + manual; copies only `index.html`, `style.css`, `CNAME`, `.nojekyll`, `media/` into the artifact); verify the YAML parses and a local run of the copy step produces an artifact containing every file the page references and nothing from `openspec/`, `.claude/` or `README.md`

## 2. Theme foundation (style.css)

- [x] 2.1 Download 0xProto Regular (and Bold if used) as woff2 into `media/fonts/` together with its OFL licence file; verify the files exist and the licence text is present
- [x] 2.2 Create `style.css` with a modern reset, `:root` design tokens (colours, spacing, font sizes per design §4), `color-scheme: dark`, `@font-face` with `font-display: swap`, and a monospace fallback stack; verify by opening a test page that the font loads, and that with the font file renamed the text falls back to a system monospace
- [x] 2.3 Add base typography, link and `:focus-visible` styles using the accent colour, with transitions and smooth scrolling only under `prefers-reduced-motion: no-preference`; verify with a contrast checker that `--text`, `--muted` and `--accent` reach ≥ 4.5:1 on both `--bg` and `--surface`, and adjust the values if not

## 3. Page content (index.html)

- [x] 3.1 Create `index.html` with `lang="en"`, charset, viewport, title, meta description, favicon and stylesheet links, plus the skeleton header/nav, main and footer landmarks; verify the page opens locally with no console errors and the tab shows the title and favicon
- [x] 3.2 Build the hero: `h1` name, role, intro, and the profile links list with GitHub and LinkedIn (`target="_blank" rel="noopener noreferrer"`), plus a commented template line for adding e.g. GitLab; verify that the links open in a new tab and that adding a test GitLab line shows it with identical styling
- [x] 3.3 Build the about section (`#about`) with placeholder paragraphs marked `TODO:`; verify the nav link scrolls there and `/#about` deep-links to it
- [x] 3.4 Build the skills section (`#skills`) as labelled groups (Backend: Java, Spring Boot, C#; Frontend: Angular, TypeScript; Tools: placeholder) with a commented group template; verify that adding a skill and a new group needs no CSS changes
- [x] 3.5 Build the projects section (`#projects`) with 2–3 placeholder `article` cards (title, description, tech tags, optional repo/live links; at least one card without links) and a commented card template; verify that a card without links shows no empty link row
- [x] 3.6 Build the CV section (`#cv`) with "Experience" and "Education" sub-lists in reverse chronological order, using `<time>` periods and "present" for ongoing entries, plus commented entry templates; verify that both sub-lists are visually distinct and in correct order
- [x] 3.7 Use the FvJ icon set from `media/icons/` as header logo (inside the "Back to top" link, `alt=""`) and as favicon (SVG + `.ico` fallback + apple-touch-icon); verify the logo shows at 375px and 1280px and the tab shows the icon
- [x] 3.8 Add canonical URL, Open Graph tags (`icon-512.png` as image, with dimensions and alt) and `twitter:card=summary`; verify all tags parse with absolute `https://fabrice-vj.ch/` URLs and `og:description` matches the meta description

## 4. Layout and responsiveness

- [x] 4.1 Style the header/nav, hero, sections and footer mobile-first (single column, `max-width` reading width, fluid `clamp()` spacing and type); verify at 320px and 375px in browser device mode that there's no horizontal scrollbar
- [x] 4.2 Style tags and link lists with `flex-wrap`, and project cards with an `auto-fit`/`minmax` grid and `--surface` background; verify that cards stack on phones and sit side by side at ≥ 1024px, and that a long tag list wraps
- [x] 4.3 Add the single `min-width: 40rem` breakpoint (skills label beside tags, timeline date beside entry, sticky header); verify the layout at 600px, 768px, 1280px and 1920px widths

## 5. Accessibility and quality checks

- [ ] 5.1 Keyboard pass: Tab through the whole page; verify that every link is reachable in reading order with a visible focus ring, and that nav links move focus/scroll to their sections
- [ ] 5.2 Structure pass: verify there is exactly one `h1`, one `h2` per section and `h3` for sub-items, that landmarks are present (e.g. via the browser accessibility tree or a Lighthouse accessibility audit scoring ≥ 95), and that the HTML validates with no errors at validator.w3.org
- [x] 5.3 Preference checks: verify that with the OS set to light mode the page stays dark, that with reduced motion enabled nav jumps aren't animated, and that with JavaScript disabled everything works the same
- [x] 5.4 Rewrite `README.md` to cover what the site is, how to preview it locally, how to add a link/skill/project/CV entry (pointing to the templates), and how deployment works; verify the documented preview command works as written

## 6. Content and go-live

- [ ] 6.1 Replace all placeholders with Fabrice's real content (intro, about, skills, projects, experience, education, GitHub/LinkedIn URLs); verify `grep -n "TODO" index.html` returns nothing
- [ ] 6.2 Commit and push to `main`, then in GitHub Settings → Pages set Source to "GitHub Actions", set the custom domain to `fabrice-vj.ch` and enforce HTTPS; verify the "Deploy to GitHub Pages" run in the Actions tab succeeds, that https://fabrice-vj.ch/openspec/ returns 404, and that https://fabrice-vj.ch serves the new page and http redirects to https
- [ ] 6.3 Final live check on a real phone and a desktop browser; verify that all profile and project links resolve (no 404s) and the favicon and title show correctly
- [ ] 6.4 Check link previews with the LinkedIn Post Inspector (linkedin.com/post-inspector); verify that title, description and the FvJ logo appear

## Workflow follow-up

- Archive the change with `/opsx:archive` once the site is live and verified.
