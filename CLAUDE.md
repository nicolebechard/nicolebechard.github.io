# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static HTML/CSS portfolio website hosted on GitHub Pages at `https://nicolebechard.github.io`. No build tools, frameworks, or dependencies.

## Running Locally

```bash
python3 -m http.server 8000
# Then open http://localhost:8000
```

Or open any `.html` file directly in a browser.

## Deployment

Push to the `main` branch — GitHub Pages auto-deploys.

## Architecture

Each page is a self-contained HTML file with all CSS embedded in `<style>` tags. There are no external stylesheets, no JavaScript, and no build step.

**Pages and current status:**
- `index.html` — complete; teal/indigo/magenta palette, dark hero with gradient wash, company name cards in brand colors
- `blackbaud_casestudy.html` — complete; purple (#7b4f9e) accent, five base64-embedded dashboard images; pending updated images and navigation fix
- `microsoft_casestudy.html` — complete; pending navigation fix
- `msft_roadmap.html` — standalone page intended for iframe embed (830px height); per-row theme color gradients, vision diagram embedded
- `wrike_casestudy.html` — complete; pending updated images and navigation fix
- `gooddata_casestudy.html` — complete; pending small tweaks, updated images, and navigation fix

**Pending across all pages:** fix navigation, final QA, contact page.

**Design system conventions:**
- CSS custom properties defined in `:root` for colors (`--ink`, `--slate`, `--cream`, plus a per-page `--accent` color)
- Typography: Playfair Display (headings) and DM Sans (body) loaded from Google Fonts
- Responsive layout via CSS Grid and Flexbox; fluid type sizing via `clamp()`
- Each case study page uses a distinct accent color to distinguish the company
- Navigation bar is sticky on all pages; case study pages link back to `index.html`

## FrigoTime pages (`frigotime/`)

A side project hosted on this site but **separate from the portfolio**: its own branding, not linked from portfolio pages. A future "Side Projects" section may link to it. The site's live domain is `nicolebechard.com` (see `CNAME`); absolute URLs in meta tags use it.

**Pages (both live, launched September 2026):**
- `frigotime/index.html` → `nicolebechard.com/frigotime/`: beta tester landing page. Built from a Claude Design handoff ("FrigoTime Beta Testing Brief").
- `frigotime/privacy/index.html` → `nicolebechard.com/frigotime/privacy/`: beta privacy notice. Text is Nicole's own, reproduced verbatim; do not edit wording without her. Written in first person ("I"), unlike the beta page ("we"), because Nicole is the individual data controller.

**Do not move or rename anything in `frigotime/`.** The URLs are in testers' inboxes and chats, the privacy URL is linked from the Tally form, and `frigotime/logo-wide.png` is loaded by URL in the FrigoTime Gmail signature.

**Link-only by design:** both pages have `<meta name="robots" content="noindex, nofollow">`, are not in `sitemap.xml`, and are not linked from portfolio pages. Keep it that way unless Nicole decides otherwise.

**External connections:**
- All "Sign up" buttons (marked `data-signup`) → Tally form `https://tally.so/r/kdqD8r`. The form has its own cover image, thank-you page, and a link to the privacy notice.
- "Contact us" buttons → `mailto:frigotimeapp@gmail.com`.
- Applicants get replies from Gmail templates on frigotimeapp@gmail.com (accepted / not this round). The page promises a reply "within a few days"; keep page, thank-you page, and emails consistent.

**Design (FrigoTime design system, not the portfolio's):**
- Fonts: Fredoka (headings, buttons) + Inter (body), from Google Fonts.
- Colors: brand green `#8dc63f`, amber `#fbb040`, pumpkin `#f7901e`, ink `#58595b` for all text. Tokens are in each page's `:root`.
- Beta page structure: hero (green wash) → proof strip → amber band = the problem (intro, landscape, why it happens, the gap) → green band = the approach (how it works, what we're testing, what this isn't) → green sign-up section → footer.
- Hero fridge photo is a half-oval dome anchored to the hero's bottom edge, centered on the phone screenshot; width responsive; hidden below 720px.
- Images are separate files in `frigotime/` (not base64), resized for web. `og-image.png` (1200×630) is the link preview; preview title "Join the FrigoTime beta".
- No JavaScript, consistent with the rest of the site.

**Content rules:**
- Photo `fridge-bg.jpg` is from Magnific (formerly Freepik) under the free license, which **requires** the footer credit "Designed by Magnific" linking to magnific.com. Do not remove it while the photo is used.
- Food waste figures in "The landscape" are from UNEP Food Waste Index Report 2024 (2022 data) via Our World in Data, and are cited on the page.
- Testing commitment is **4 weeks, at least 5 items per week**. Page, Tally form, and acceptance email must match.
- Same copy rules as the portfolio: no em dashes, no hype or guilt framing.

**Open / possible next work:** in-app feedback form and weekly check-in survey (not built yet; privacy notice already mentions the feedback form); Side Projects section on the portfolio.

## Copy and Voice

- **No em dashes** — flagged as an AI signal; use commas, colons, or restructure the sentence
- **No arrogant or AI-sounding language** — avoid phrases that overstate individual impact
- **Collaborative framing always** — Nicole is connective tissue, not sole driver; always validate attributions and avoid overstating her individual role
- Chosen homepage headline: "I build data products the same way I've built my career: by adapting, experimenting, and never waiting for perfect conditions."

## Working with Large HTML Files

Files with base64-embedded images can be very large. For targeted edits, Python string replacement is more reliable than `sed`:

```bash
python3 << 'EOF'
with open('file.html', 'r') as f:
    html = f.read()
html = html.replace('old string', 'new string')
with open('file.html', 'w') as f:
    f.write(html)
EOF
```

Do not use f-strings or heredocs with these files at scale — they fail at large file sizes.
