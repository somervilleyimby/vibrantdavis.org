# vibrantdavis.org

Source for <https://vibrantdavis.org>, a project of [Somerville YIMBY](https://somervilleyimby.org).

Hosted with [GitHub Pages](https://pages.github.com/), served from the `main` branch. Pushes to `main` deploy automatically. The site uses Jekyll's stock [Cayman theme](https://github.com/pages-themes/cayman) — no `_layouts` override, no forked template. Site title and the homepage's `<title>` are both "Vibrant Davis"; the theme's own header renders `site.title`/`page.title` and `page.description` as-is.

- `_config.yml` — site title/description and `theme:`.
- `assets/css/style.scss` — the theme's own documented customization hook (`@import "{{ site.theme }}";` plus additions), not a theme modification. Retunes the accent colors to the Vibrant Davis teal and adds `.kicker`, `.hero-headline`, `.button-row`/`.btn-outline`, `.stat-strip`, `.timeline`, `.cta-box`, and `.footnote` classes used by `index.md`.
- `index.md` — the page content, as Markdown with a few raw HTML blocks (stat strip, hero button row, timeline, CTA card) that lean on those classes. The kicker line and campaign headline live here in the body, not in the theme's header — Cayman's stock layout only has room for a title and one tagline.

## Local preview

The `Gemfile` pins the `github-pages` gem, so a local build matches what GitHub's servers actually run — but that gem's dependency chain (Jekyll 3.9, Liquid 4.0.3) requires Ruby ≤ 3.1; anything newer removed `String#tainted?`, which Liquid still calls.

If your system Ruby is newer than 3.1, use [rbenv](https://github.com/rbenv/rbenv) to run this project on an older Ruby without touching your system install:

```bash
brew install rbenv ruby-build
brew install ruby@3.1   # bottled/precompiled — more reliable than building 3.1 from source on a modern macOS SDK
ln -s "$(brew --prefix ruby@3.1)" ~/.rbenv/versions/3.1.7-homebrew
cd vibrantdavis.org      # .ruby-version here already pins 3.1.7-homebrew
gem install bundler
bundle install
bundle exec jekyll serve
```

Then open <http://localhost:4000>. `jekyll serve` live-reloads on file changes.

If your system Ruby is already ≤ 3.1, you can skip rbenv entirely and just run `bundle install && bundle exec jekyll serve` directly.

## Custom domain

The `CNAME` file pins the custom domain (`vibrantdavis.org`). DNS must point at GitHub Pages:

- Apex `A` records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- `www` `CNAME` → `somervilleyimby.github.io`
