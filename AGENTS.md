# Build: MediaKit — LinkedIn Creator Network Website

Build a single-page web application that serves as a media kit for a LinkedIn creator network. The site presents three YC-backed founders as a creator network for B2B startup brand partnerships. It is not an agency — it is a creator network.

---

## Tech Stack & Constraints

- Pure HTML + CSS + vanilla JavaScript. No frameworks, no build tools.
- Single `index.html` file with all pages included as `<section>` elements.
- External CSS in `assets/theme.css`.
- Must work by opening `index.html` directly in a browser.
- Font: Inter from Google Fonts.

---

## Layout

The entire app is a two-panel layout filling 100vh with no scroll on the outer shell:

```
┌─────────────────────────────────────────────────────┐
│  SIDEBAR (220px fixed) │  MAIN CONTENT (flex: 1)    │
│                        │                             │
│  Brand kicker          │  One page visible at        │
│  Nav buttons 00–09     │  a time (page stack)        │
│                        │                             │
│  Footer                │  Pages scroll internally    │
└─────────────────────────────────────────────────────┘
```

**Sidebar:**
- Background: `#111`
- Right border: `1px solid #1e1e1e`
- Top: small-caps kicker label "MediaKit" in `#444`
- Navigation buttons stacked vertically with 2px gaps
- Each button: number prefix (00, 01...) + label text
- Active button: `background #1e1e1e`, text white, number turns `#e63946`
- Footer: brand name + tagline in muted text

**Page stack:**
- `position: relative` container, `overflow: hidden`
- Each page: `position: absolute; inset: 0; overflow-y: auto; display: none`
- Active page: `display: block`
- Fade-in animation on page change: `opacity 0 → 1, translateY 6px → 0` over 0.25s
- Page padding: `40px 48px`

**Page loader:**
- Full-screen `#0d0d0d` overlay on initial load
- Centered spinner (32px circle, border `#222`, border-top `#e63946`, spinning animation)
- Small uppercase label "Loading media kit…"
- Fades out after 600ms

---

## Design System

### Colors
```
App background:     #0d0d0d
Sidebar bg:         #111
Card bg:            #141414
Card bg alt:        #1a1a1a
Border default:     #1e1e1e
Border subtle:      #2a2a2a
Accent red:         #e63946
Red tint bg:        rgba(230, 57, 70, 0.10)
Red tint border:    rgba(230, 57, 70, 0.25)
Text primary:       #ffffff
Text secondary:     #aaaaaa
Text muted:         #666666
Text dim:           #444444
Text very dim:      #333333
Growth green:       #4caf50
```

### Typography
- All text: Inter
- H1: `1.75rem / 800 / letter-spacing -0.03em`
- Large metric values: `1.5–2rem / 800`
- Section labels: `0.65rem / 700 / letter-spacing 0.1em / UPPERCASE / color #333`
- Badges: `0.65rem / 700 / letter-spacing 0.1em / UPPERCASE`
- Body: `0.875rem / 400 / line-height 1.6`
- Subtitles: `0.875rem / color #666`
- Small labels under metrics: `0.7rem / color #555`

### Cards
- Background: `#141414`, border: `1px solid #1e1e1e`, border-radius: `10px`
- Inner padding: `22–28px`
- Metric values inside cards: large, weight 800, white

### Badges
```html
<span class="badge">LABEL</span>            <!-- default: #1e1e1e bg, #666 text -->
<span class="badge badge-red">LABEL</span>  <!-- red tint bg, #e63946 text -->
```

### Visual Emphasis — Red Highlight System
Three patterns used to draw attention to key metrics:

**1. Highlight line** — a 2px red horizontal rule, placed under key numbers:
```html
<div class="highlight-line"></div>
```
```css
.highlight-line { height: 2px; background: #e63946; border-radius: 1px; margin: 4px 0 12px; }
```

**2. Callout arrow row** — red upward arrow + red uppercase label:
```html
<div class="callout-row">
  <div class="callout-arrow">↑</div>
  <div class="callout-label">KEY INSIGHT TEXT HERE</div>
</div>
```
```css
.callout-arrow  { color: #e63946; font-size: 1rem; font-weight: 700; }
.callout-label  { font-size: 0.7rem; color: #e63946; font-weight: 600; letter-spacing: 0.05em; text-transform: uppercase; }
```

**3. Accent border card** — left red border on metric cards:
```css
.accent-border { border-left: 3px solid #e63946; }
```

**4. Red metric value** — apply inline `style="color:#e63946"` on KPI values that represent the most important number on a given page (e.g. 21% C-suite, impression YoY growth).

---

## Navigation Logic (JavaScript)

```javascript
const pageMap = {
  cover:     { page: 'page-cover',     nav: 'nav00' },
  overview:  { page: 'page-overview',  nav: 'nav01' },
  reach:     { page: 'page-reach',     nav: 'nav02' },
  yurii:     { page: 'page-yurii',     nav: 'nav03' },
  stanislav: { page: 'page-stanislav', nav: 'nav04' },
  nikolai:   { page: 'page-nikolai',   nav: 'nav05' },
  audience:  { page: 'page-audience',  nav: 'nav06' },
  results:   { page: 'page-results',   nav: 'nav07' },
  pricing:   { page: 'page-pricing',   nav: 'nav08' },
  contact:   { page: 'page-contact',   nav: 'nav09' },
};

function setPage(key) {
  // Remove .active from current page + nav button
  // Add .active to new page + nav button
  // Scroll new page element to top
  // Update window.location.hash to key
}
```

- On load: read `window.location.hash`, navigate to that page if valid
- Keyboard navigation: ArrowRight/Down = next page, ArrowLeft/Up = previous page
- Page loader fades out 600ms after load

---

## All Pages — Full Specification

### PAGE 00 — Cover (`cover`)

Full-height centered layout. No sidebar scroll needed.

Elements (top to bottom, centered):
1. Three circular avatar initials in a row: `YR` · `SB` · `NG`
   - Each: 52px circle, `background #1e1e1e`, `border 2px solid #2a2a2a`, initials in `#888`
2. H1: "LinkedIn Creator Network<br>for **B2B Startups**"
   - "B2B Startups" wrapped in `<span style="color:#e63946">`
3. Subtitle paragraph: "Three YC-backed founders. One high-trust audience of decision-makers."
4. Three inline metric items (horizontal row):
   - `240K+` / Combined followers
   - `59.7M` / Impressions / year
   - `21%` / Founders & C-suite
5. Red CTA button: "Start reading →" → calls `setPage('overview')`
   - Style: `background #e63946`, white text, `padding 12px 28px`, `border-radius 8px`
6. Small copyright line

---

### PAGE 01 — Overview (`overview`)

Badge: `TL;DR` | H1: "What we do" | Subtitle describes founder-led LinkedIn marketing.

**Two-column card grid** (`.tldr-grid`):

Card 01 — "The network":
- Number label: `01`
- Title: "The network"
- Sub: "Three YC-backed founders with combined reach across SF, London, and NYC"
- Metric grid (3 cells with vertical dividers between):
  - `240K+` / Combined followers
  - `59.7M` / Impressions per year
  - `21%` / Founders & C-suite

Card 02 — "Why it works":
- Number label: `02`
- Title: "Why it works"
- Sub: "Founder credibility converts. Decision-makers trust other founders — not ads."
- Four bullet points with small red circle dots:
  - **YC-backed founders** — built-in credibility with the startup ecosystem
  - **Organic distribution** — no paid amplification, pure audience trust
  - **2–3%+ CTR** vs LinkedIn Ads' 0.4% — 10× better performance
  - **B2B decision-makers** — VCs, startup founders, CMOs, growth leads

**Bottom lever cards** (3-column grid, below the main cards):
- Title row: "Three creators — one ecosystem"
- Card 1: badge "Creator 01" · name "Yurii Rebryk" · value `129K` · label "followers · $4,500/post"
- Card 2: badge "Creator 02" · name "Stanislav Beliaev" · value `72K` · label "followers · $3,500/post"
- Card 3: badge "Creator 03" · name "Nikolai Golos" · value `39K` · label "followers · $2,000/post"

---

### PAGE 02 — Combined Reach (`reach`)

Badge: `Combined` | H1: "Network reach" | Subtitle about B2B decision-makers in SF/London/NYC.

**KPI row** (4 equal cards, horizontal):
- Combined followers: `240K+` / "Across 3 creators"
- Impressions / year: `59.7M` / "Organic · no paid boost"
- Founders & C-suite: `21%` in red / "Of total audience"
- Top locations: `SF · NYC / London` (smaller font, two lines) / "#1 audience markets"

**Horizontal bar chart** comparing 3 creators by followers:
- Row format: `[name label 140px] [track bar flex] [value 80px]`
- Yurii Rebryk: 100% width, fill color `#e63946` (accent red), label "129,126"
- Stanislav Beliaev: 56% width, fill color `#8a2020` (dark red), label "72,177"
- Nikolai Golos: 30% width, fill color `#3a1a1a` (very dark red), label "38,926"
- Track bg: `#1a1a1a`, height 28px

Below chart: callout row — "↑ Combined: 240,229 followers · #1 in SF startup ecosystem"

---

### PAGE 03 — Yurii Rebryk (`yurii`)

Badge: `Creator 01` | H1: "Yurii Rebryk" | Subtitle: "Founder & CEO, Fluently AI · YC W24 · Ex-Google · Ex-NVIDIA · Forbes 30u30"

**Creator hero card** (2-column: left = identity, right = metric cards):

Left column:
- Avatar circle (72px) with initials "YR"
- Name: Yurii Rebryk (large, bold)
- Title: Founder & CEO, Fluently AI
- Tag row: `YC W24` (red badge) · `Ex-Google` · `Ex-NVIDIA` · `Forbes 30u30` (red badge)

Right column (stacked metric cards, min-width 160px):
- Card 1 (accent-border): `129K` / LinkedIn followers
- Card 2: `27.3M` / "Impressions / year ▲21%" (▲21% in green `#4caf50`)
- Card 3: `$4,500` / Per dedicated post

Below hero:
- Callout row: "↑ LARGEST CREATOR IN NETWORK · 21% FOUNDERS & C-SUITE AUDIENCE"
- Red highlight line

**Campaign results section:**
- Section label: "Campaign results — Framer"
- Two result cards side by side:
  - Card 1: brand label "Framer · Post 1" · red arrow ↑ · `529,582` (large) · "total impressions" · callout label "TOP POST IN NETWORK HISTORY" · red highlight line
  - Card 2: brand label "Framer · Post 2" · `18,783` · "total impressions" · note "Combined Framer campaign: 548,365 impressions"

**Analytics section:**
- Section label: "Impressions analytics (365 days)"
- Image: `assets/yurii-impressions.jpg` — full width, rounded, bordered
- Section label: "Audience breakdown — top demographics"
- Image: `assets/yurii-audience.jpg` — full width, rounded, bordered
- Three stat cards: `26%` Senior · `10%` Founders · `18%` Software Development
- Callout: "↑ SF BAY AREA = #1 LOCATION · 22% FROM 2–10 PERSON STARTUPS · FOUNDERS TOP JOB TITLE"
- Red highlight line

---

### PAGE 04 — Stanislav Beliaev (`stanislav`)

Badge: `Creator 02` | H1: "Stanislav Beliaev" | Subtitle: "Co-Founder & CTO, GetFluently.App · YC W24 · ex-NVIDIA"

**Creator hero card:**

Left: avatar "SB" · name · title · tags: `YC W24` (red) · `ex-NVIDIA`

Right metric cards:
- `72.2K` / "LinkedIn followers ▲6,252%" (growth in green)
- `24.6M` / Impressions / year
- `$3,500` / Per dedicated post

Callout: "↑ TECHNICAL FOUNDER — STRONG REACH WITH ENGINEERING & AI AUDIENCES"
Red highlight line.

**Analytics section:**
- Section label: "Impressions analytics (365 days)"
- Image: `assets/stanislav-impressions.jpg`
- Section label: "Audience breakdown"
- Image: `assets/stanislav-audience.jpg`
- Three stat cards: `30%` Senior seniority · `23%` Software Development · `▲6,252%` Follower growth YoY (red)
- Callout: "↑ 72,161 FOLLOWERS · SENIOR = #1 SENIORITY · SOFTWARE DEV = #1 INDUSTRY"
- Red highlight line

---

### PAGE 05 — Nikolai Golos (`nikolai`)

Badge: `Creator 03` | H1: "Nikolai Golos" | Subtitle: "Product & Growth, Fluently AI · YC W24"

**Creator hero card:**

Left: avatar "NG" · name · title · tags: `YC W24` (red) · `LinkedIn Research Lead`

Right metric cards:
- `39K` / LinkedIn followers
- `7.7M` / "Impressions / year ▲97%" (▲97% in green)
- `$2,000` / Per dedicated post

Callout: "↑ GROWTH & PRODUCT AUDIENCE · HIGHEST ENGAGEMENT RATE IN NETWORK"
Red highlight line.

**Campaign results:**
- Section label: "Campaign results — Rork"
- Two cards:
  - Card 1: "Rork · Post 1" · red arrow ↑ · `115,424` impressions · red highlight line
  - Card 2: "Rork · Post 2" · `36,187` impressions

**Analytics section:**
- "Impressions analytics (365 days)" → `assets/nikolai-impressions.jpg`
- "Audience seniority & company breakdown" → `assets/nikolai-audience.jpg` + `assets/nikolai-audience2.jpg`
- Three stat cards: `32.2%` Senior (red) · `8.3%` Director (red) · `7.7%` CXO
- Callout: "↑ SENIOR + DIRECTOR + OWNER + CXO = 56.2% · TOP COMPANIES: MICROSOFT, AMAZON, GOOGLE"
- Red highlight line

---

### PAGE 06 — Audience (`audience`)

Badge: `Audience` | H1: "Who sees your content" | Subtitle about B2B decision-makers.

**Top stat row** (3 cards):
- `21%` red / Founders & C-suite
- `59.7M` red / Impressions / year
- `SF · NYC · LDN` / #1 audience locations

Callout: "↑ TIER 1 MARKETS — SAN FRANCISCO, NEW YORK CITY, LONDON"
Red highlight line.

**Three creator sections stacked vertically (in this order: Yurii → Stanislav → Nikolai):**

Yurii (section label: "Yurii Rebryk · 129K followers · 27.3M impressions/year ▲21%"):
- `assets/yurii-impressions.jpg`
- `assets/yurii-audience.jpg`

Stanislav (section label: "Stanislav Beliaev · 72K followers · 24.6M impressions/year ▲6,252% growth"):
- `assets/stanislav-impressions.jpg`
- `assets/stanislav-audience.jpg`

Nikolai (section label: "Nikolai Golos · 39K followers · 7.7M impressions/year ▲97%"):
- `assets/nikolai-impressions.jpg`
- `assets/nikolai-audience.jpg`
- `assets/nikolai-audience2.jpg`

---

### PAGE 07 — Results (`results`)

Badge: `Results` | H1: "Proven campaign performance" | Subtitle about verified analytics.

**Performance comparison panel** (red-tinted box, `rgba(230,57,70,0.06)` bg, red border):
- Three columns centered:
  - `2–3%+` in red / "Our CTR"
  - `0.4%` in muted / "LinkedIn Ads avg CTR"
  - `~10×` in white / "Better performance"
- Below: callout "↑ ORGANIC REACH OUTPERFORMS LINKEDIN ADS AT FRACTION OF CPM"

**Framer campaign** (section label: "Campaign: Framer × Yurii Rebryk"):
- Two result cards:
  - Post 1: red ↑ arrow · `529,582` · "total impressions" · callout "TOP POST IN NETWORK HISTORY" · red highlight line
  - Post 2: `18,783` · note "Combined Framer campaign: 548,365 impressions"

**Rork campaign** (section label: "Campaign: Rork × Nikolai Golos"):
- Two result cards:
  - Post 1: red ↑ arrow · `115,424` · red highlight line
  - Post 2: `36,187` · note "Combined Rork campaign: 151,611 impressions"

---

### PAGE 08 — Pricing (`pricing`)

Badge: `Pricing` | H1: "Partnership packages" | Subtitle: "Transparent, performance-driven."

**Three pricing cards side by side:**

**Card 1 — Network Bundle — FEATURED (highlighted with red border)**
- Style: `border-color #e63946`, slightly darker red-tinted bg `#161010`, subtle red radial gradient overlay
- Tier label: "Most popular"
- Name: "Network Bundle"
- Price: `$8,000` / campaign
- Description: Full network activation. One post from each creator.
- Line items (with red dot bullets):
  - 1× Yurii Rebryk post (129K reach) — $4,500 value
  - 1× Stanislav Beliaev post (72K reach) — $3,500 value
  - 1× Nikolai Golos post (39K reach) — $2,000 value
  - 240K+ combined reach · 3 posts
  - Full campaign brief & content review
- Red callout box: "↑ Save $2,000 vs. buying posts individually"

**Card 2 — Single Post**
- Tier label: "Flexible"
- Price: `$2,000` – `$4,500`
- Description: Pick the creator that fits your audience best.
- Items (plain dot bullets):
  - Yurii Rebryk (129K) — $4,500
  - Stanislav Beliaev (72K) — $3,500
  - Nikolai Golos (39K) — $2,000
  - 1 revision round included
  - Performance report post-publish

**Card 3 — CPM Model**
- Tier label: "Performance"
- Price: `$45` / 1K impressions
- Description: Pay only for impressions delivered.
- Items (red dot bullets for first two, plain for rest):
  - Pay per verified impression
  - Works across any creator account
  - LinkedIn Ads: $33–65 CPM · 0.4% CTR
  - We deliver: 2–3%+ CTR
- Red callout box: "↑ ~10× better CTR than LinkedIn Ads"

Below all cards: info bar with "→" arrow explaining minimums and what's included.

---

### PAGE 09 — Book a Call (`contact`)

Badge: `Contact` | Full-height centered layout.

Elements (centered, column):
1. Badge: "Contact"
2. H1: "Let's talk<br>partnerships"
3. Subtitle: "Interested in working with our creator network? We typically book 2 weeks out — reach out early."
4. Two buttons side by side:
   - Primary (red): "Send an email →" → `mailto:contactnadiiashpvl@gmail.com`
   - Secondary (dark): "LinkedIn ↗" → `https://www.linkedin.com/in/nadiia-shapovalova-25653628a` (opens new tab)
5. Contact block:
   - Label: "Direct email"
   - Value: `contactnadiiashpvl@gmail.com`
6. Small copyright line

---

## All Creator Data

```
Yurii Rebryk
- Followers: 129,126 (display: 129K)
- Impressions/year: 27,349,430 (display: 27.3M) · ▲21% YoY
- Title: Founder & CEO, Fluently AI
- Bio tags: YC W24, Ex-Google, Ex-NVIDIA, Forbes 30u30
- Price: $4,500/post
- Campaigns: Framer Post 1 = 529,582 · Post 2 = 18,783
- Audience: Senior 26%, Founder 10%, Software Dev 18%, SF Bay Area #1, 2-10 employees 22%

Stanislav Beliaev
- Followers: 72,161 (display: 72.2K) · ▲6,252% YoY
- Impressions/year: 24,627,794 (display: 24.6M)
- Title: Co-Founder & CTO, GetFluently.App
- Bio tags: YC W24, ex-NVIDIA
- Price: $3,500/post
- Audience: Senior 30%, Software Dev 23%

Nikolai Golos
- Followers: 38,926 (display: 39K)
- Impressions/year: 7,714,818 (display: 7.7M) · ▲97.4% YoY
- Title: Product & Growth, Fluently AI
- Bio tags: YC W24, LinkedIn Research Lead
- Price: $2,000/post
- Campaigns: Rork Post 1 = 115,424 · Post 2 = 36,187
- Audience: Senior 32.2%, Director 8.3%, Owner 8%, CXO 7.7%
  Company size: 1-10 (16.7%), 11-50 (14.8%), 10001+ (13.9%)
  Top companies: Stealth Startup, Microsoft, Amazon, Google
```

---

## Image Assets

All images are in `assets/`:
```
yurii-impressions.jpg      — Yurii content analytics (impressions chart)
yurii-audience.jpg         — Yurii audience top demographics
stanislav-impressions.jpg  — Stanislav content analytics
stanislav-audience.jpg     — Stanislav audience breakdown
nikolai-impressions.jpg    — Nikolai content analytics
nikolai-audience.jpg       — Nikolai audience seniority overview
nikolai-audience2.jpg      — Nikolai audience seniority + company detail
```

All displayed full-width with `border-radius: 8px` and `border: 1px solid #1e1e1e`.

---

## Tone & Copy Rules

- Data first. Lead every section with the number.
- No adjectives without data to back them up.
- Never use "agency" — always "creator network" or "MediaKit".
- Short sentences. Present tense.
- Callout labels are always UPPERCASE, short, and punchy.
- Pricing copy is direct: state what you get, state the price, nothing else.
- The site presents the work, it does not sell it. Let the numbers do the selling.
