# Spec Delta

## Purpose

Defines how the portfolio is delivered to visitors: static files with no build step, published from the repository's main branch to GitHub Pages under the custom domain fabrice-vj.ch.

## ADDED Requirements

### Requirement: Build-free static site
The repository SHALL contain the site as ready-to-serve static files at its root. Publishing SHALL NOT require installing dependencies or running a build step.

#### Scenario: Open locally
- **WHEN** `index.html` from a fresh clone is opened in a browser (or served by any static file server)
- **THEN** the complete site renders without running any install or build command

### Requirement: Publish on push to main
Every push to the `main` branch SHALL automatically publish the site to GitHub Pages without a build step. A manual re-publish SHALL also be possible.

#### Scenario: Content update goes live
- **WHEN** a commit changing `index.html` is pushed to `main`
- **THEN** the updated page is live on GitHub Pages within a few minutes, with no manual step

#### Scenario: Manual re-publish
- **WHEN** the deployment is triggered manually from the repository's Actions tab
- **THEN** the current `main` is published again

### Requirement: Only site files are published
Only the files the page needs (HTML, CSS, `media/`, domain and Pages configuration) SHALL be published. Repository-only files such as planning documents, tool configuration and the README SHALL NOT be reachable on the live site.

#### Scenario: Planning files not public
- **WHEN** a visitor requests `https://fabrice-vj.ch/openspec/` or `https://fabrice-vj.ch/README.md`
- **THEN** the site responds with "not found"

### Requirement: Custom domain
The site SHALL be served at `fabrice-vj.ch`, and the repository SHALL contain a `CNAME` file with that domain so the setting survives every publish.

#### Scenario: Visiting the domain
- **WHEN** a visitor opens `https://fabrice-vj.ch`
- **THEN** the portfolio page is served over HTTPS

#### Scenario: Domain survives a publish
- **WHEN** a new commit is published
- **THEN** the custom domain configuration is still in place
