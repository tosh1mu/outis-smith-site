# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Corporate website for オーティス・スミス株式会社 (Outis Smith Inc.), a Japanese M&A advisory / management consulting firm. The entire site is a single self-contained static page: `index.html` (~180KB), served via GitHub Pages at the custom domain in `CNAME` (outis-smith.co.jp).

There is no build step, no framework, no JavaScript, and no dependencies. Editing `index.html` and pushing to `main` deploys the site.

## Design concept

The visual identity is built on the firm's name: **Outis** (Οὖτις, Greek "no one" — Odysseus's alias, punning on *mētis*, "cunning craft") + **Smith** (maker) = "the anonymous craftsman of cunning." The site is styled as a discreet, editorial **dossier / private letter** for a sophisticated finance audience (PE funds, investment banks) — restraint is the brief, not decoration. Keep changes quiet and deliberate; the one signature flourish is the hero colophon (`ΟΥΤΙΣ` in Cormorant + gloss). Do not add loud UI or extra animation.

## Architecture

- **`index.html`** — the whole site. One HTML document with all CSS inlined in a single `<head>` `<style>` block. Content is in Japanese, `lang="ja"`. Sections are `#services`, `#company`, `#representative`, `#contact`, anchored from the sticky nav. Design tokens live in CSS custom properties under `:root`: palette (`--paper #F6F5EF`, `--forest #14503A`, `--deep`, `--ink`, `--moss`, `--line`) and four type roles (`--serif` Shippori Mincho for headings, `--display` Cormorant Garamond for the Greek colophon, `--sans` Noto Sans JP for body, `--mono` IBM Plex Mono for eyebrows/labels/data). Sections use a `.section-grid` (170px margin column holding a mono `.eyebrow` label + a hairline `border-left` rule on `.section-main`) — an editorial margin-note layout; it collapses to one column under 820px. There are **no `01/02/03` section numbers** (deliberately avoided). The hero has a single CSS-only page-load reveal sequence (`.reveal` + staggered `animation-delay`), guarded by `@media (prefers-reduced-motion: no-preference)`. The mobile nav is a **JS-free CSS toggle** (hidden `#nav-toggle` checkbox + `.nav-btn` label hamburger, revealed via `.nav-toggle:checked ~ nav`) — keep it script-free.
- **Logo files** — `outis-smith_logo_{green,white,black}.svg` are the same wordmark in three fills. Header uses green (on paper), hero (`<h1>`) and footer use white (on green). Referenced as external `<img src>` so the browser caches one copy instead of re-inlining. The representative portrait (`#representative`) is the only image still embedded inline (base64 JPEG) — it has no external file.
- **`ogp.jpg`** — Open Graph share image (`og:image`), 1568×168 wordmark. Thin banner aspect; replace with a 1200×630 card if a proper OGP asset is produced.
- **`CNAME`** — GitHub Pages custom domain binding.
- **`robots.txt` + page `<meta name="robots">`** — the site is deliberately kept out of search and AI crawlers. `robots.txt` `Disallow: /` for all user-agents (with explicit entries for Googlebot, GPTBot, ClaudeBot, CCBot, PerplexityBot, etc.), and the page carries `noindex, nofollow, noarchive, nosnippet, noimageindex`. Preserve this posture unless explicitly asked to make the site indexable.

## Working in this repo

- Preview by opening `index.html` directly in a browser — no server required. Webfonts require network; opened offline the type falls back to system serif/sans/mono (layout is still faithful).
- Logos are external SVGs; the favicon and representative portrait are inline (SVG data-URI / base64 JPEG respectively).
- Fonts load from Google Fonts (Shippori Mincho, Cormorant Garamond, Noto Sans JP, IBM Plex Mono). This is the only external network dependency.
- Deployment is automatic on push to `main` via GitHub Pages; there are no CI, test, or lint steps.
