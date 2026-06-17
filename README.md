# jekyll-with-admin-install-local-base

A ready-to-copy Jekyll starter with the default minima theme and a built-in admin panel. Everything needed to run is already bundled — no internet required after setup.

---

## What is this?

This is a base template for quickly spinning up new Jekyll sites. Instead of running `bundle install` from scratch every time (which needs the internet), all the gem files are already saved in `vendor/cache/`. You just copy the folder, install locally, and go.

The minima theme files are also copied directly into the project instead of being pulled from the gem at build time, so the site looks and behaves consistently.

---

## Getting started

```bash
# 1. Copy this folder to your new project location
# 2. Install gems from the local cache (no internet needed)
bundle install --local

# 3. Start the server
bundle exec jekyll serve
```

Your site will be at `http://localhost:4000`
The admin panel will be at `http://localhost:4000/admin`

---

## What's inside

```
├── _layouts/       ← page templates (default, home, post, page)
├── _includes/      ← reusable HTML parts (header, footer, head)
├── _sass/          ← styles
├── assets/         ← compiled CSS and icons
├── _plugins/       ← runtime patches (see Notes below)
├── _posts/         ← your blog posts go here
├── vendor/cache/   ← saved gem files for offline install
├── Gemfile         ← declares dependencies (jekyll, minima, jekyll-admin)
├── Gemfile.lock    ← locks exact versions so every install is identical
└── _config.yml     ← site settings (title, plugins, theme)
```

---

## What to commit to GitHub

```
┌────────────────────────────────────────┬──────────┬───────────────────────────────────┐
│                  Path                  │ Include? │                Why                │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ _layouts/, _includes/, _sass/, assets/ │ ✅       │ Local minima copy                 │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ _posts/                                │ ✅       │ Content                           │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ vendor/cache/                          │ ✅       │ Offline gem cache                 │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ Gemfile, Gemfile.lock                  │ ✅       │ Pinned deps                       │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ _config.yml                            │ ✅       │ Site config                       │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ README.md                              │ ✅       │                                   │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ .gitignore                             │ ✅       │                                   │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ _site/                                 │ ❌       │ Generated output, rebuild locally │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ vendor/bundle/                         │ ❌       │ Installed gems, machine-specific  │
├────────────────────────────────────────┼──────────┼───────────────────────────────────┤
│ .jekyll-cache/, .sass-cache/           │ ❌       │ Temporary build caches            │
└────────────────────────────────────────┴──────────┴───────────────────────────────────┘
```

> `vendor/bundle/` is already excluded by `.gitignore`. The cache (`vendor/cache/`) is intentionally kept so clones work offline.

---

## Notes

### jekyll-admin UI fix

jekyll-admin 0.12.0 has two bugs when used with Jekyll 4.x:

1. The configuration API endpoint fails to serialize the config object, causing the admin panel to show **"Could not fetch the config"** error.
2. The admin panel crashes on load if `jekyll_admin:` is not present in `_config.yml`.

Both are fixed by `_plugins/jekyll_admin_patch.rb`, which is included in this project and loads automatically. No manual steps needed — it works as soon as you run `bundle install --local` and serve.
