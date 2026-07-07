# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Corporate website for オーティス・スミス株式会社 (Outis Smith Inc.), a Japanese M&A advisory / management consulting firm. The entire site is a single self-contained static page: `index.html` (~180KB), served via GitHub Pages at the custom domain in `CNAME` (outis-smith.co.jp).

There is no build step, no framework, no JavaScript, and no dependencies. Editing `index.html` and pushing to `main` deploys the site.

## Architecture

- **`index.html`** — the whole site. One HTML document with all CSS inlined in a single `<head>` `<style>` block. Content is in Japanese, `lang="ja"`. Sections are `#services`, `#company`, `#representative`, `#contact`, anchored from the sticky nav. Design tokens (brand green, grays, spacing) are CSS custom properties under `:root`. The mobile nav is a **JS-free CSS toggle** (hidden `#nav-toggle` checkbox + `.nav-btn` label hamburger, revealed via `.nav-toggle:checked ~ nav`) — keep it script-free.
- **Logo files** — `outis-smith_logo_{green,white,black}.svg` are the same wordmark in three fills. Header uses green (on white), hero (`<h1>`) and footer use white (on green). Referenced as external `<img src>` so the browser caches one copy instead of re-inlining. The representative portrait (`#representative`) is the only image still embedded inline (base64 JPEG) — it has no external file.
- **`ogp.jpg`** — Open Graph share image (`og:image`), 1568×168 wordmark. Thin banner aspect; replace with a 1200×630 card if a proper OGP asset is produced.
- **`CNAME`** — GitHub Pages custom domain binding.
- **`robots.txt` + page `<meta name="robots">`** — the site is deliberately kept out of search and AI crawlers. `robots.txt` `Disallow: /` for all user-agents (with explicit entries for Googlebot, GPTBot, ClaudeBot, CCBot, PerplexityBot, etc.), and the page carries `noindex, nofollow, noarchive, nosnippet, noimageindex`. Preserve this posture unless explicitly asked to make the site indexable.

## Working in this repo

- Preview by opening `index.html` directly in a browser — no server required.
- To change images, replace the inline base64 `data:` URIs (the logo is JPEG base64, the favicon is an inline SVG). There are no external asset files.
- Fonts load from Google Fonts (Jost for Latin/EN accents, Noto Sans JP for body). This is the only external network dependency.
- Deployment is automatic on push to `main` via GitHub Pages; there are no CI, test, or lint steps.
