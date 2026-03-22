# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **RedSeed LMS API documentation site**, built on [Slate](https://github.com/slatedocs/slate) — a Ruby/Middleman-based static site generator for API docs. The API base endpoint is `https://api.redseed.me/api/v0`.

## Commands

```bash
# Install dependencies
bundle install

# Local development server (port 4567)
bundle exec middleman serve --watcher-force-polling
# Or via Docker:
docker run --rm --name slate -p 4567:4567 -v $(pwd)/source:/srv/slate/source -v $(pwd)/data:/srv/slate/data slatedocs/slate serve

# Build static site to ./build/
bundle exec middleman build --clean

# Deploy (builds + pushes to gh-pages branch)
./deploy.sh
# Build only: ./deploy.sh --source-only
# Push only: ./deploy.sh --push-only
```

The `slate.sh` wrapper also supports: `./slate.sh serve`, `./slate.sh build`, `./slate.sh deploy`.

## Architecture

- **`source/index.html.md.erb`** — Main entry point. YAML frontmatter controls which includes are loaded, language tabs, and TOC footers.
- **`source/includes/_*.md`** — Individual API endpoint documentation files (users, locations, courses, training, etc.). These are referenced by filename (without `_` prefix and extension) in the `includes:` frontmatter of `index.html.md.erb`.
- **`data/redseed.json`** — Shared data (API endpoint URL) accessible in ERB templates.
- **`config.rb`** — Middleman configuration: markdown settings (Redcarpet), asset pipeline, syntax highlighting, build optimizations.
- **`lib/`** — Custom Ruby extensions:
  - `multilang.rb` — Multi-language code block support (syntax: `` ```lang--tab-name`` ``)
  - `unique_head.rb` / `nesting_unique_head.rb` — Unique HTML ID generation for headers
  - `toc_data.rb` — Table of contents data extraction
  - `monokai_sublime_slate.rb` — Custom syntax highlighting theme

## Adding/Editing API Docs

1. Create or edit a markdown file in `source/includes/` (prefix with `_`).
2. Register it in `source/index.html.md.erb` under the `includes:` frontmatter list.
3. Use ERB to reference shared data: `<%= config[:endpoint] %>` or `<%= data.redseed.endpoint %>`.

## Deployment

Pushes to `main` trigger a GitHub Actions workflow (`.github/workflows/deploy.yml`) that builds and deploys to the `gh-pages` branch via `peaceiris/actions-gh-pages`.
