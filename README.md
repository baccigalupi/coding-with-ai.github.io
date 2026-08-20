# coding-with-ai.github.io

Jekyll site for [Coding with AI](https://www.coding-with.ai). Source lives in this repo; GitHub Pages builds and publishes it on push to `main`.

## Prerequisites

- Ruby **3.3.4** (see [`.ruby-version`](.ruby-version))
- Bundler
- Optional but recommended: a Ruby version manager (rvm etc.) and the project gemset in [`.ruby-gemset`](.ruby-gemset) (`coding-with-ai-github-io`)

## Local development

From the repo root:

```bash
bundle install
./dev/server
```

`./dev/server` runs `bundle exec jekyll serve --livereload`. Open [http://127.0.0.1:4000](http://127.0.0.1:4000). Edits to pages, posts, layouts, and styles reload automatically.

To skip `bundle install` on startup:

```bash
SKIP_BUNDLE_INSTALL=1 ./dev/server
```

### Create a post

```bash
./dev/new-post "My Post Title"
# or
./dev/new-post --title "My Post Title"
```

This creates a dated file under `_posts/` with front matter and a placeholder heading.

### Build without serving

```bash
bundle exec jekyll build
```

Output goes to `_site/` (gitignored). Useful for checking that the site builds cleanly before pushing.

### Config changes

If you edit [`_config.yml`](_config.yml), restart `./dev/server` — Jekyll does not reload config on the fly.

## Publish / deploy

This site uses **GitHub Pages** with the [`github-pages`](https://pages.github.com/versions/) gem. There is no GitHub Actions workflow; GitHub builds Jekyll when you push to `main`.

1. Commit your changes (do not commit `_site/`).
2. Push to `main`:

   ```bash
   git push origin main
   ```

3. GitHub Pages publishes the built site. After a minute or two, changes appear at:
   - https://coding-with-ai.github.io
   - https://www.coding-with.ai (custom domain)

### Custom domain

The [`CNAME`](CNAME) file sets the custom domain to `www.coding-with.ai`. After the first push that includes `CNAME`, confirm it under **Repo → Settings → Pages → Custom domain**.

At your DNS provider, point `www.coding-with.ai` at GitHub Pages (typically a CNAME to `<user>.github.io` or the apex/`www` records GitHub documents for your setup). See [GitHub's custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).

## Project layout

| Path | Purpose |
|------|---------|
| `_config.yml` | Site title, author, permalink style |
| `_posts/` | Blog posts (Markdown) |
| `_layouts/`, `_includes/`, `_sass/` | Templates and Bootstrap-based styles |
| `assets/` | CSS and images |
| `dev/server` | Local preview with livereload |
| `dev/new-post` | Scaffold a new post |
