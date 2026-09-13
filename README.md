# Natural Philosophy

*The study of things as they are.*

A static philosophical journal built with Jekyll and hosted on GitHub Pages. Essays are Markdown files with a small YAML front matter block — no HTML editing, no database, no CMS.

## Publishing a New Essay

1. Add a file to `_posts/` named `YYYY-MM-DD-your-title.md`.
2. Give it this front matter:

   ```yaml
   ---
   layout: post
   title: "Your Essay Title"
   date: 2026-09-14
   description: "One sentence, shown wherever the essay is listed."
   ---
   ```

3. Write the essay in Markdown below it.
4. Commit and push to `main`.

That's it. The homepage, the archive, and the essay's own page are all generated automatically — there's nothing else to update.

For images, math, or linking to other essays, see **Writing an Essay** below.

## What This Is

A minimal, text-first publishing setup: write an essay in Markdown, push, it's live. No JavaScript framework, no build step you need to think about beyond Jekyll itself. Three example essays ship with the project to show the format working end to end (including one that links to the other two) — delete or replace them whenever you like.

## Project Structure

```
_config.yml              Site title, tagline, and deployment settings
_posts/                  One Markdown file per essay — this is what you edit
about.md                 The About page (same format as an essay)
index.html               Homepage
archive.html             Full archive, grouped by year
_layouts/                Page templates (see "Layouts and Includes" below)
_includes/               Shared template snippets
assets/css/style.css     All site styling
assets/images/           Images referenced from essays
.github/workflows/       The GitHub Actions deployment workflow
```

## Writing an Essay

**Standard Markdown** works throughout: headings, paragraphs, lists, `> ` blockquotes, `[links](url)`, and fenced code blocks.

**Images** — place the file under `assets/images/` and reference it without a leading slash:

```markdown
![Alt text](assets/images/your-image.svg)
```

**Math** — wrap LaTeX in double dollar signs. On its own line, it's a displayed equation; inline in a sentence, it's inline math:

```markdown
An inline example: $$x^2 + y^2 = z^2$$ in the middle of a sentence.

$$
x^2 + y^2 = z^2
$$
```

**Linking to another essay** — an essay can mark itself as a **Response** to another essay (challenges or disagrees with it) and/or an **Addition** to another essay (builds on it). Add either to the front matter as a list of the target essay's filename, without `.md`:

```yaml
responses:
  - "2026-09-11-on-first-principles"
additions:
  - "2026-09-12-kinds-and-their-boundaries"
```

The linked essay's real title and URL are looked up automatically — you never type them by hand. If a field is empty or omitted, nothing extra is shown.

## Previewing Locally

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

## Publishing Changes

Any change — a new essay, an edit to `about.md`, a CSS tweak — is published the same way: commit and push to `main`. There's no separate deploy step to run yourself.

## How GitHub Pages Deploys the Site

Pushing to `main` triggers the workflow in `.github/workflows/pages.yml`, which builds the site with Jekyll and publishes it — usually within a minute or two. You can watch it run under the repo's **Actions** tab.

One-time setup on a fresh repo: under **Settings → Pages**, set **Source** to **GitHub Actions**. Also open `_config.yml` and set `url` to your GitHub Pages address (`baseurl` is already set correctly for this repo's name; only change it if you rename the repo or move it to a `your-username.github.io` root site).

## Where the CSS Lives

Everything is in the single file `assets/css/style.css`. There's no preprocessor or build step for styles — edit it directly and refresh.

## Where the Layouts Live

`_layouts/` holds the three page templates:

- `default.html` — the outer HTML shell every page shares (used by the other two layouts)
- `page.html` — used by `about.md` and `archive.html`
- `post.html` — used by every essay

`_includes/` holds smaller pieces reused across pages: `header.html` (site title and nav), `footer.html`, and `essay-relations.html` (the Response/Addition sections on an essay page).
