# my-website

Personal portfolio and CV of Fabrice von Jüchen, live at **https://fabrice-vj.ch**.

A single static page: plain HTML and CSS, no build step, no dependencies, no JavaScript.

```
index.html          all content
style.css           all styling (design tokens at the top, in :root)
media/icons/        logo + favicons (svg, ico, png, apple-touch-icon)
media/fonts/        self-hosted 0xProto font (SIL OFL 1.1, see OFL.txt)
CNAME               custom domain for GitHub Pages
.nojekyll           tells GitHub Pages to serve files as-is
.github/workflows/  deploy to GitHub Pages on push to main
```

## Preview locally

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## Editing content

Everything lives in `index.html`. Each repeating list has a commented **template** right above it. Copy the
template, paste it into the list and fill it in. The CSS never needs to change.

| To add…               | Section in `index.html` | What to copy                                     |
| --------------------- | ----------------------- | ------------------------------------------------ |
| a profile link        | `HERO` → `ul.links`     | one `<li><a …>Name</a></li>` line                |
| a skill               | `SKILLS`                | one `<li>Skill</li>` in the right group          |
| a skill group         | `SKILLS`                | a whole `<div><dt>…</dt><dd>…</dd></div>` block  |
| a project             | `PROJECTS`              | a whole `<li><article class="card">…</li>` block |
| a job / education     | `CV`                    | a whole `<li class="entry">…</li>` (newest first) |

External links use `target="_blank" rel="noopener noreferrer"`. They get the small ↗ marker automatically.

To change colours, fonts or spacing, edit the variables in `:root` at the top of `style.css`. Keep text colours at a
contrast of at least 4.5:1 against `--bg` and `--surface`.

## Deployment

Every push to `main` runs `.github/workflows/pages.yml`, which publishes the site to GitHub Pages within a minute or two.
There is no build: the workflow copies `index.html`, `style.css`, `CNAME`, `.nojekyll` and `media/` as they are.
Nothing else in the repo (`openspec/`, `.claude/`, this README) goes live. **If you add a new top-level file the page
needs, add it to the "Collect site files" step.** Runs are listed in the *Actions* tab, where you can also re-run a
deploy by hand ("Run workflow").

One-time setup in GitHub → Settings → Pages: Source *GitHub Actions*, custom domain `fabrice-vj.ch`, *Enforce HTTPS* on.

## License

Code: MIT, see `LICENSE`. Font: 0xProto, SIL Open Font License 1.1, see `media/fonts/OFL.txt`.
