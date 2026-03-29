# Jekyll Minimal Mistakes — Multilingual Setup (EN / DE / NE)

A complete multilingual configuration for the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) Jekyll theme supporting **English**, **German (Deutsch)**, and **Nepali (नेपाली)**.

---

## 📁 File Structure

```
├── _config.yml                          # Main config with language defaults
├── Gemfile
│
├── _data/
│   ├── navigation.yml                   # Nav links (titles auto-translated)
│   └── translations/
│       ├── en.yml                       # English strings
│       ├── de.yml                       # German strings
│       └── ne.yml                       # Nepali strings
│
├── _includes/
│   ├── language-switcher.html           # Language switcher nav component
│   ├── i18n.html                        # Translation helper macro
│   ├── i18n-head.html                   # hreflang SEO tags
│   ├── masthead.html                    # Masthead override with lang switcher
│   └── head/
│       └── custom.html                  # Custom <head> (hreflang + Devanagari font)
│
├── _pages/
│   ├── en/  home.md, about.md ...       # English pages
│   ├── de/  home.md, about.md ...       # German pages
│   └── ne/  home.md, about.md ...       # Nepali pages
│
├── _posts/
│   ├── en/  YYYY-MM-DD-slug.md          # English posts
│   ├── de/  YYYY-MM-DD-slug.md          # German posts
│   └── ne/  YYYY-MM-DD-slug.md          # Nepali posts
│
└── assets/css/
    ├── main.scss                        # Main stylesheet entry point
    └── language-switcher.scss           # Switcher styles
```

---

## 🚀 Quick Start

### 1. Install dependencies

```bash
bundle install
```

### 2. Run locally

```bash
bundle exec jekyll serve
```

### 3. Visit

| Language | URL                     |
|----------|-------------------------|
| English  | http://localhost:4000/  |
| German   | http://localhost:4000/de/ |
| Nepali   | http://localhost:4000/ne/ |

---

## ✍️ Creating Content

### Page front matter

Every page needs `lang`, `permalink`, and `lang_alts`:

```yaml
---
layout: single
title: "About"
lang: en                    # en | de | ne
permalink: /about/
lang_alts:                  # links to equivalent pages in other languages
  de: /de/about/
  ne: /ne/about/
author_profile: true
---
```

### Blog posts

Place posts in the correct language subfolder and prefix with a date:

```
_posts/
  en/2024-03-01-my-post.md
  de/2024-03-01-mein-beitrag.md
  ne/2024-03-01-mero-lekh.md
```

Post front matter:

```yaml
---
layout: single
title: "My Post Title"
date: 2024-03-01
lang: de
permalink: /de/blog/mein-beitrag/
lang_alts:
  en: /blog/my-post/
  ne: /ne/blog/mero-lekh/
categories: [news]
tags: [jekyll, multilingual]
---
```

---

## 🌐 Using Translations in Templates

### In any layout or include:

```liquid
{% assign t = site.data.translations[page.lang | default: site.default_lang] %}

{{ t.nav.home }}
{{ t.posts.read_time | replace: '%{time}', page.read_time }}
{{ t.pagination.next }}
```

### Using the i18n helper include:

```liquid
{% include i18n.html key="nav.home" %}
{% include i18n.html key="posts.read_time" time=5 %}
{% include i18n.html key="search.results_found" count=42 %}
```

### Language switcher (already in masthead):

```liquid
{% include language-switcher.html %}
```

---

## 🔤 Nepali / Devanagari Script

- The **Noto Sans Devanagari** font is loaded automatically from Google Fonts **only on Nepali pages** (`lang: ne`) — no extra weight on other pages.
- `_includes/head/custom.html` handles the conditional font load.
- `assets/css/main.scss` applies comfortable `line-height` and `font-size` for Devanagari.
- No plugin required — pure CSS `:lang(ne)` selector.

---

## ➕ Adding a New Language

1. Create `_data/translations/fr.yml` (copy `en.yml` and translate)
2. Add `"fr"` to `languages` in `_config.yml`
3. Add defaults for `_pages/fr` and `_posts/fr` in `_config.yml`
4. Create `_pages/fr/` and `_posts/fr/` folders
5. Add `lang_alts.fr:` entries to existing pages

---

## 🔍 SEO

`_includes/i18n-head.html` (loaded via `head/custom.html`) automatically outputs:

```html
<link rel="alternate" hreflang="en" href="https://yoursite.com/about/" />
<link rel="alternate" hreflang="de" href="https://yoursite.com/de/about/" />
<link rel="alternate" hreflang="ne" href="https://yoursite.com/ne/about/" />
<link rel="alternate" hreflang="x-default" href="https://yoursite.com/about/" />
```

This tells Google which page to show for which language/region.

---

## 📦 Plugins Used

| Plugin | Purpose |
|--------|---------|
| jekyll-paginate | Pagination |
| jekyll-sitemap | XML sitemap (auto includes all lang pages) |
| jekyll-feed | RSS feed |
| jekyll-include-cache | Performance |

> **GitHub Pages**: All plugins above are whitelisted. Use `remote_theme: mmistakes/minimal-mistakes` instead of `theme:` in `_config.yml`.

---

## 🎨 Theme Skins

Change `minimal_mistakes_skin` in `_config.yml`:

`default` · `air` · `aqua` · `contrast` · `dark` · `dirt` · `neon` · `mint` · `plum` · `sunrise`
