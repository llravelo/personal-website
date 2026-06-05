# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal website/blog for Leiko Ravelo, built with [Hugo](https://gohugo.io/) using the [Blowfish](https://blowfish.page/) theme. Deployed on Netlify to https://leikoravelo.com.

## Commands

```bash
hugo server -D          # Local dev server with drafts (live reload)
hugo server             # Local dev server, published content only
hugo --gc --minify      # Production build (output to public/)
hugo new content posts/my-post/index.md   # Scaffold a new post from archetypes/default.md
```

Netlify build (see `netlify.toml`): `hugo --gc --minify --baseURL "${URL}"` with Hugo 0.152.2, Go 1.25.3, Node 22.20.0.

## Theme submodule

The Blowfish theme is a git submodule at `themes/blowfish` (see `.gitmodules`). If it is ever missing/empty (e.g. fresh clone), fetch it before building:

```bash
git submodule update --init --recursive
```

All theme layouts, partials, and shortcodes live inside the submodule. To override theme behavior, mirror the theme's file path under the project root (`layouts/`, `assets/`) rather than editing the submodule.

## Configuration

Config is split across `config/_default/` (these take precedence over the root `hugo.toml`, which still holds Hugo's placeholder defaults — `baseURL` is correctly set in `config/_default/hugo.toml`):

- `hugo.toml` — core Hugo settings: taxonomies (tags, categories, authors, series), outputs, pagination, related-content config.
- `params.toml` — Blowfish theme params (color scheme, homepage `profile` layout, header/footer/article/list display toggles).
- `languages.en.toml` — site title ("Leiko's Blog"), author identity, and author social links (GitHub, LinkedIn).
- `menus.en.toml` — nav menu (Posts, About). Note: the `pageRef = "about"` menu entry has no backing content yet (`content/about/` does not exist).
- `markup.toml` — Goldmark/highlight settings required by the theme; includes math passthrough delimiters. Do not weaken these.

## Content

- Posts live in `content/posts/<slug>/index.md` as page bundles (co-locate images in the same folder).
- Front matter uses TOML (`+++`) per `archetypes/default.md`; existing posts may use YAML (`---`). New posts default to `draft = true`.
- `public/` and `resources/` are generated output — do not edit by hand; they are regenerated on build.
