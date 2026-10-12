# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static marketing site for Bruno Mello & Anderson Alves (AI consulting / training), served by GitHub Pages at **knowai.today** (`CNAME`). There is no build step, package manager, linter, or test suite: every page is a single hand-edited `index.html` with inline `<style>` and `<script>`. `.nojekyll` disables Jekyll processing. Deploy = push to `main`.

Preview locally with any static server from the repo root (absolute paths like `/favicon.svg` and `/assets/...` require serving from root, not opening the file directly), e.g. `python3 -m http.server 8000`.

Content and commit messages are in Brazilian Portuguese.

## Pages

- `/` (`index.html`) — main page, pt-BR.
- `/en/` (`en/index.html`) — en-US translation of the main page. It is a separate copy, so content/layout changes to one must be mirrored in the other.
- `/letramento/` — landing page for the in-person "Letramento de IA na Prática" event; CTAs go to Asaas checkout links and WhatsApp (links built at runtime from a `WHATSAPP` constant and `data-wa` attributes). `/letramento/termos/` holds the registration terms and privacy policy.
- `/register/` — pre-registration page (English path because the audience is mostly American). Unlike the main site, it is bilingual in a single file via paired `<span data-lang="pt">` / `<span data-lang="en">` elements. Config lives in constants at the top of its script: `FORM_ENDPOINT` (POSTs JSON; when empty it only logs to console and shows the thank-you state), `VIDEO` sources, and the selectable date range.

## Cross-page conventions

- **Language routing**: the inline script at the top of `index.html` redirects non-Portuguese browsers to `/en/` unless `localStorage.lang` is `'pt'` (and skips bots/link-preview crawlers). The PT | EN switcher (`[data-set-lang]`) saves the choice to `localStorage`. Both versions carry `canonical`, `hreflang` (pt-BR, en-US, x-default → `/`) and `og:locale` tags — keep these in sync when adding pages/translations.
- **Shared head**: every page links `/favicon.ico`, `/favicon.svg`, `/apple-touch-icon.png` and loads Poppins (display), Manrope (body) and JetBrains Mono (mono) from Google Fonts. The main pages also load Lucide icons from unpkg (`lucide.createIcons()` on DOMContentLoaded).
- **Brand**: dark background `#0A0A12`, gradient `#E61EFD → #A855F5 → (#5B8DEF) → #14D4DF`, accent text `#D89DF9`. There is no shared stylesheet — styles are duplicated per page (`letramento/` uses `:root` CSS variables; the main pages mostly use inline styles from the original Claude Design export).
- **Images**: `assets/` holds each photo as both `.webp` (used/preloaded) and `.jpg` fallback. `assets/originais/` (unoptimized originals) is gitignored.
- Contact points reused across pages: WhatsApp `5513996402074`, `bruno@manycontent.com`, the two founders' LinkedIn profiles.
