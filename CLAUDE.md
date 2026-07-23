# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Static HTML website for the FEEDBACK SOFIA Legacy Project (University of Maryland astronomy research group), served from `http://feedback.astro.umd.edu`. There is no build system, package manager, or test suite — it is plain HTML/CSS/JS edited directly and deployed by pulling the repo to the web server.

## Deployment model

- The `master` branch is the source of truth. The live site auto-syncs from `master` once per day (not on every push).
- There is no CI/CD, staging environment, or build step. Editing an `.html` file in the repo is the entire "deploy" workflow once it's pushed.
- For urgent changes, an out-of-band email to the site maintainer (Marc Pound) is needed to trigger an immediate pull.

## Architecture

- **Server Side Includes (SSI)**: every page shares common chrome via Apache SSI directives, not a templating engine:
  - `<!--#include virtual="includes/links.inc" -->` — CSS/font `<link>` tags, placed in `<head>`
  - `<!--#include virtual="includes/nav.inc" -->` — the top navbar, placed right after `<body>`
  - `<!--#include virtual="includes/footer.inc" -->` — scripts (jQuery/Popper/Bootstrap CDN + `js/dynamic-menu.js`) and the page footer, placed before `</body>`
  - When adding a new top-level page, copy this three-include skeleton from an existing page (e.g. `index.html`) rather than hand-rolling nav/footer markup.
  - Because these are SSI includes, they only render correctly when served through Apache (or another SSI-aware server) — opening the raw `.html` file in a browser will show the include comments literally, not the rendered nav/footer.
- **Navigation**: the navbar structure (including dropdown menus for Sources, Data, Tools, Team, About) lives solely in `includes/nav.inc`. Adding/removing a page from the nav means editing that one file, which then applies to every page.
- **Per-source pages**: `M16.html`, `M17.html`, `MonR2.html`, `NGC6334.html`, `NGC7538.html`, `RCW36.html`, `RCW49.html`, `RCW79.html`, `W40.html`, `W43.html`, `CygnusX.html` are near-identical templates for individual observed sources/nebulae — each pairs with a corresponding image in `images/` (e.g. `M16_8micron_noCII_smooth_2.png`). `sourcetable.html` and `sources.html` provide the overview/index of these.
- **Styling**: `css/fbslpstyle.css` is the site's custom stylesheet;  Bootstrap 4 (via CDN) provides the grid/component base.
- **Fonts**: both self-hosted (`fonts/audiowide-*`) and Google Fonts (linked in `includes/links.inc`/`includes/fonts.inc`) are used; `includes/fonts.inc` currently duplicates the Google Fonts `<link>` from `includes/links.inc` and does not appear to be included by any page — check before relying on it.
- **`publications.html`** and **`team.html`** are the two most actively maintained content pages (frequent edits in git history) — publications is a long, manually maintained bibliography list; team is the member roster.

## Editing conventions

- Preserve the existing SSI include structure and Bootstrap 4 class conventions when editing or adding pages.
- Internal nav links use root-relative paths (e.g. `/index.html`, `/publications.html`); keep this convention for consistency across pages regardless of directory depth.
