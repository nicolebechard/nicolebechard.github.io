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
