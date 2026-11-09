# Proposal

## Why

fabrice-vj.ch currently shows only an "under construction" placeholder, and the repository is half torn down: the old files are deleted in the working tree, and a deploy workflow calls a build step that does not exist. This change replaces it with a real one-page portfolio and CV that introduces Fabrice, lists his skills, projects, work experience and education, and links to his profiles. The site is published in the simplest way that works on GitHub Pages.

## What Changes

- Add a single static page (`index.html` + `style.css`) with these sections: hero (name, role, short intro, profile links), about, skills (grouped), projects (cards), and a timeline with work experience and education.
- Add profile links for GitHub and LinkedIn, set up so more links (e.g. GitLab, e-mail) can be added with one line each.
- Apply a minimal, dark-only visual design. It keeps the 0xProto monospace font and slate palette from the previous placeholder and adds one accent colour.
- Make the page responsive (mobile-first) so it reads well from ~320px phones up to wide desktop screens.
- **BREAKING (repo/tooling)**: Remove the Bun/TypeScript scaffolding (`package.json`, `bun.lock`, `tsconfig.json`, `index.ts`), the unused `.gitignore.txt`, and the broken Bun-based `.github/workflows/deploy.yml`. Afterwards the site has no build step.
- Publish to GitHub Pages on every push to `main` with a small official Pages workflow (`.github/workflows/pages.yml`) that copies only the site files, so planning and tool files stay private. Restore the `CNAME` file (`fabrice-vj.ch`).
- Restore `README.md` (updated to describe how to edit and deploy the site) and `LICENSE`. Use the FvJ icon set in `media/icons/` as header logo, favicon and link-preview image, and add Open Graph tags so shared links show a preview card.

Explicitly out of scope: a blog, a profile photo, a downloadable PDF CV, a light theme or theme toggle, JavaScript-driven features, and any build tooling or framework.

## Capabilities

### New Capabilities
- `portfolio-content`: What the page presents and how it is structured. This covers the hero, about, skills, projects, experience and education sections, and the extensible list of profile links.
- `site-appearance`: How the page looks and adapts. This covers the dark minimal theme, typography, accessibility basics (contrast, focus, reduced motion) and responsive behaviour across screen sizes.
- `site-hosting`: How the site is served. This covers static, build-free delivery through GitHub Pages on the custom domain fabrice-vj.ch.

### Modified Capabilities
<!-- None: no specs exist yet. -->

## Impact

- **Files added/restored**: `index.html`, `style.css`, `CNAME`, `README.md`, `LICENSE`, `media/icons/` (FvJ logo and favicons), `media/fonts/` (self-hosted 0xProto).
- **Files removed**: `package.json`, `bun.lock`, `tsconfig.json`, `index.ts`, `media/fvj-test.svg`, `.gitignore.txt`, `.github/workflows/deploy.yml` (replaced by `.github/workflows/pages.yml`).
- **Dependencies**: none at runtime or build time, and no third-party requests. The 0xProto font is self-hosted, with a system monospace fallback.
- **External systems**: The GitHub repository's Pages settings must be set to Source "GitHub Actions" with custom domain `fabrice-vj.ch`, and DNS for fabrice-vj.ch must keep pointing at GitHub Pages. This is a manual step in GitHub's UI and can't be done from the repo.
- **Content**: Fabrice has to supply the real text (intro, about, skills, projects, jobs, education, profile URLs). Until then, clearly marked placeholders are used.
