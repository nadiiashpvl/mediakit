# Build: MediaKit — LinkedIn Creator Network Website

Build a single-page web application that serves as a media kit for a LinkedIn creator network. The site presents three founders with large LinkedIn audiences as a creator network for B2B startup brand partnerships. It is **not an agency** — it is a **creator network**.

---

## Tech Stack & Constraints

- Pure HTML + CSS + vanilla JavaScript. No frameworks, no build tools.
- Single `index.html` file with all pages included as `<section>` elements.
- External CSS in `assets/theme.css`.
- Must work by opening `index.html` directly in a browser.
- Font: Inter from Google Fonts.
- Mobile: fixed bottom tab bar replaces sidebar on screens ≤640px.

---

## Layout

### Desktop (>640px)
Two-panel layout filling 100vh:

```
┌──────────────────────────────────────────────────────┐
│  SIDEBAR (200px fixed) │  MAIN CONTENT (flex: 1)     │
│                        │                              │
│  Brand kicker          │  One page visible at         │
│  Nav buttons 00–08     │  a time (page stack)         │
│                        │                              │
│  Footer                │  Pages scroll internally     │
└──────────────────────────────────────────────────────┘
```

### Mobile (≤640px)
- Sidebar hidden
- Fixed scrollable bottom tab bar with numbered buttons
- Pages stack full-screen, scroll vertically
- Side-by-side grids collapse to single column

---

## Design System (Higgsfield light theme)

### Color Tokens
```css
:root {
  --color-primary:        #7C3AED;   /* Purple — main accent */
  --color-primary-hover:  #6D28D9;
  --color-primary-soft:   #EDE9FE;   /* Purple tint background */
  --color-primary-muted:  #C4B5FD;   /* Purple border */
  --color-bg:             #F8FAFC;   /* App background */
  --color-surface:        #FFFFFF;   /* Card background */
  --color-surface-2:      #F1F5F9;   /* Subtle card alt */
  --color-text:           #0F172A;   /* Primary text */
  --color-text-secondary: #64748B;   /* Secondary text */
  --color-text-tertiary:  #94A3B8;   /* Muted labels */
  --color-border:         #E2E8F0;
  --color-border-light:   #F1F5F9;
  --color-accent-blue:    #3B82F6;
  --color-accent-green:   #10B981;
  --grad-primary: linear-gradient(135deg, #7C3AED 0%, #6D28D9 100%);
}
```

### Typography
- Font: Inter
- H1: `1.5rem / 800 / letter-spacing -0.03em`
- Metric values: `1.25–1.75rem / 800`
- Body: `0.825rem / 400 / line-height 1.55`
- Badges/labels: `0.6rem / 700 / letter-spacing 0.1em / UPPERCASE`
- Section labels: `0.6rem / 700 / UPPERCASE / color --color-text-tertiary`

### Cards
- Background: `--color-surface`, border: `1px solid --color-border`, radius: `--radius-md` (12px)
- Padding: `18–20px`
- Box shadow: `0 1px 3px rgba(0,0,0,0.06)`

### Page padding
- Desktop: `28px 36px`
- Mobile: `20px 16px`, with `100px` bottom padding for tab bar clearance

### Badges
```html
<span class="badge">LABEL</span>            <!-- purple tint -->
<span class="badge badge-blue">LABEL</span> <!-- blue tint -->
<span class="badge badge-green">LABEL</span><!-- green tint -->
```

### Visual Emphasis System

**1. Highlight line** (2px purple rule under key stats):
```html
<div class="highlight-line"></div>
```

**2. Callout arrow row:**
```html
<div class="callout-row">
  <div class="callout-arrow">↑</div>
  <div class="callout-label">KEY INSIGHT HERE</div>
</div>
```

**3. Accent border on metric card** (purple left border):
```css
.creator-metric-card.accent-border { border-left: 3px solid var(--color-primary); }
```

**4. Tier-1 callout box** (purple tint panel with arrow):
```html
<div class="tier1-box">
  <div class="tier1-arrow">📍</div>
  <div class="tier1-content">
    <div class="tier1-label">LABEL</div>
    <div class="tier1-value">Value text</div>
    <div class="tier1-sub">Supporting detail</div>
  </div>
</div>
```

**5. Gradient text on cover title:**
```html
<span class="intro-title-highlight">Tier-1</span>
```
```css
.intro-title-highlight {
  background: var(--grad-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
```

---

## Navigation (JavaScript)

```javascript
const pageMap = {
  cover:     { page: 'page-cover',     nav: 'nav00' },
  overview:  { page: 'page-overview',  nav: 'nav01' },
  reach:     { page: 'page-reach',     nav: 'nav02' },
  yurii:     { page: 'page-yurii',     nav: 'nav03' },
  stanislav: { page: 'page-stanislav', nav: 'nav04' },
  nikolai:   { page: 'page-nikolai',   nav: 'nav05' },
  results:   { page: 'page-results',   nav: 'nav06' },
  pricing:   { page: 'page-pricing',   nav: 'nav07' },
  contact:   { page: 'page-contact',   nav: 'nav08' },
};
```

- `setPage(key)`: deactivate current → activate new → scroll to top → update hash → update mobile nav
- On load: read `window.location.hash`, navigate if valid, remove loader after 600ms
- Keyboard: ArrowRight/Down = next, ArrowLeft/Up = prev
- Mobile nav button ID: `mnav` + nav ID (e.g. `mnav00`)

---

## All Pages — Full Specification

### PAGE 00 — Cover (`cover`)

Centered full-height layout. Elements top to bottom:
1. Three circular avatar photos (56px circles, `overflow: hidden`):
   - `assets/photo-yurii.jpg` (Yurii Rebryk)
   - `assets/photo-stanislav.jpg` (Stanislav Beliaev)
   - `assets/photo-nikolai.jpg` (Nikolai Golos)
2. Small eyebrow text: "LinkedIn Creator Network" — `0.7rem / uppercase / --color-text-tertiary`
3. H1 (two lines):
   - Line 1: "Reach "
   - `<span class="intro-title-highlight">Tier-1</span>` — purple gradient text
   - Line 2: "B2B Decision Makers"
4. Metric bar (card with 3 stats separated by dividers):
   - `240K+` / Combined followers
   - `59.7M` / Impressions / year
   - `21%` / Founders & C-suite
5. CTA button: "Start reading →" → `setPage('overview')`
   - Background: `--grad-primary`, white text, purple box shadow
6. Small copyright line

---

### PAGE 01 — Overview (`overview`)

Badge: `TL;DR` | H1: "What we do"

**Two-column card grid:**

Card 01 — "The network":
- Metric grid (3 cells, vertical dividers): `240K+` followers · `59.7M` impressions/yr · `21%` Founders & C-suite

Card 02 — "Why it works":
- Bullet points with purple dots:
  - **Founder-led content** — built-in credibility
  - **Organic distribution** — no paid amplification
  - **2–3%+ CTR** vs LinkedIn Ads' 0.4% — 10× better
  - **B2B decision-makers** — VCs, CMOs, growth leads

**Lever cards** (3-column, below grid):
- Creator 01 · Yurii Rebryk · `129K` followers
- Creator 02 · Stanislav Beliaev · `72K` followers
- Creator 03 · Nikolai Golos · `39K` followers

---

### PAGE 02 — Reach & Audience (`reach`)

Badge: `Combined` | H1: "Network reach"

**KPI row** (4 cards): 240K+ followers · 59.7M impressions/yr · `21%` C-suite (purple) · SF·NYC·London

**Bar chart** (creator breakdown):
- Yurii: 100%, `--grad-primary` fill, label "129,126"
- Stanislav: 56%, purple mid gradient, label "72,177"
- Nikolai: 30%, light purple, label "38,926"

Callout row below chart.

**Divider**, then **Audience section** (merged into same page):
- Badge: `Audience` | H1: "Who sees your content"
- Stats row: `21%` Founders & C-suite · `59.7M` impressions/yr · `SF · NYC · LDN`
- **Two Tier-1 callout boxes:**
  - Box 1 (📍): "Tier 1 Audience Locations" → "San Francisco · New York City · London"
  - Box 2 (↑): "Impressions per year — verified" → "59,692,042 total impressions" → breakdown by creator

---

### PAGE 03 — Yurii Rebryk (`yurii`)

Badge: `Creator 01` | H1: "Yurii Rebryk"

**Creator hero card** (2-col):
- Left: photo `assets/photo-yurii.jpg` (56px circle) · name · title "Founder & CEO, Fluently AI"
- Tags: `YC W24` (purple) · `Ex-Google` · `Ex-NVIDIA` · `Forbes 30u30` (purple)
- Right metric cards:
  - `129K` followers (accent-border)
  - `27.3M` impressions/yr ▲21% (green)

Callout + highlight line.

**Campaign results** (2 cards, both clickable links):
- Post 1: → `https://www.linkedin.com/feed/update/urn:li:activity:7332776852098289664/` · 529,582 impressions
- Post 2: → `https://www.linkedin.com/feed/update/urn:li:activity:7383901347097640960/` · 18,783 impressions

**Analytics** (side-by-side grid, `1.2fr 0.8fr`):
- `assets/yurii-impressions.jpg` · `assets/yurii-audience.jpg`

Stats row: Senior 26% · Founders 10% · Software Dev 18%
Callout: SF Bay Area #1 location

---

### PAGE 04 — Stanislav Beliaev (`stanislav`)

Badge: `Creator 02` | H1: "Stanislav Beliaev"

Hero: photo `assets/photo-stanislav.jpg` · "Co-Founder & CTO, GetFluently.App" · tags: `YC W24` · `ex-NVIDIA`

Metrics: `72.2K` followers ▲6,252% (green) · `24.6M` impressions/yr

Callout + highlight line.

**Analytics** (side-by-side grid, `1fr 1fr`):
- `assets/stanislav-impressions.jpg` · `assets/stanislav-audience.jpg`

Stats row: Senior 30% (purple) · Software Dev 23% · ▲6,252% YoY (purple)

---

### PAGE 05 — Nikolai Golos (`nikolai`)

Badge: `Creator 03` | H1: "Nikolai Golos"

Hero: photo `assets/photo-nikolai.jpg` · "Product & Growth, Fluently AI" · tags: `YC W24` · `LinkedIn Research Lead`

Metrics: `39K` followers · `7.7M` impressions/yr ▲97% (green)

**Campaign results** (both clickable):
- Post 1: → `https://www.linkedin.com/posts/nigolos_you-can-now-turn-an-idea-into-a-functional-activity-7419352880358510592-Fisc` · 115,424 impressions
- Post 2: → `https://www.linkedin.com/feed/update/urn:li:activity:7428091697869484032/` · 36,187 impressions

**Analytics** (side-by-side grid, `1fr 1fr`):
- `assets/nikolai-impressions.jpg` · `assets/nikolai-audience.jpg`

Stats row: Senior 32.2% (purple) · Director 8.3% (purple) · CXO 7.7%
Callout: Senior + Director + Owner + CXO = 56.2%

---

### PAGE 06 — Results (`results`)

Badge: `Results` | H1: "Proven campaign performance"

**Performance panel** (purple tint): Our CTR `2–3%+` vs LinkedIn Ads `0.4%` → `~10×` better

**Framer campaign** (2 clickable cards):
- Post 1 → `https://www.linkedin.com/feed/update/urn:li:activity:7332776852098289664/` · ↑ 529,582 impressions
- Post 2 → `https://www.linkedin.com/feed/update/urn:li:activity:7383901347097640960/` · 18,783 · Combined: 548,365

**Rork campaign** (2 clickable cards):
- Post 1 → `https://www.linkedin.com/posts/nigolos_you-can-now-turn-an-idea-into-a-functional-activity-7419352880358510592-Fisc` · ↑ 115,424 impressions
- Post 2 → `https://www.linkedin.com/feed/update/urn:li:activity:7428091697869484032/` · 36,187 · Combined: 151,611

---

### PAGE 07 — Pricing (`pricing`)

Badge: `Pricing` | H1: "Partnership packages"

**2-column pricing grid** (max-width 760px):

**Card 1 — Flat Fee (FEATURED, purple border)**:
- "from $1,000 / post"
- Items: 1 dedicated post · price scales with creator size · campaign brief & collaboration · 1 revision · performance report
- CTA button: "Book a call →" → `setPage('contact')`

**Card 2 — CPM**:
- "from $40 / 1K impressions"
- Items: pay per verified impression · works across any creator · LinkedIn Ads: $33–65 CPM at 0.4% CTR · We deliver: 2–3%+ CTR · Minimum spend applies
- Purple callout: "↑ ~10× better CTR than LinkedIn Ads"
- CTA button: "Book a call →" → `setPage('contact')`

---

### PAGE 08 — Contact (`contact`)

Centered layout. H1: "Let's talk partnerships"

- Email button (primary, purple): → `mailto:contactnadiiashpvl@gmail.com`
- LinkedIn button (secondary): → `https://www.linkedin.com/in/nigolos/`
- Email display: `contactnadiiashpvl@gmail.com`

---

## Creator Data

```json
{
  "creators": [
    {
      "id": "yurii",
      "name": "Yurii Rebryk",
      "photo": "assets/photo-yurii.jpg",
      "title": "Founder & CEO, Fluently AI",
      "tags": ["YC W24", "Ex-Google", "Ex-NVIDIA", "Forbes 30u30"],
      "followers": 129126,
      "impressionsPerYear": 27349430,
      "impressionsGrowth": "+21% YoY",
      "campaigns": [
        {"brand":"Framer","post":1,"impressions":529582,"url":"https://www.linkedin.com/feed/update/urn:li:activity:7332776852098289664/"},
        {"brand":"Framer","post":2,"impressions":18783,"url":"https://www.linkedin.com/feed/update/urn:li:activity:7383901347097640960/"}
      ],
      "audience": {"senior":"26%","founders":"10%","softwareDev":"18%","topLocation":"SF Bay Area"}
    },
    {
      "id": "stanislav",
      "name": "Stanislav Beliaev",
      "photo": "assets/photo-stanislav.jpg",
      "title": "Co-Founder & CTO, GetFluently.App",
      "tags": ["YC W24", "ex-NVIDIA"],
      "followers": 72161,
      "followersGrowth": "+6,252% YoY",
      "impressionsPerYear": 24627794,
      "audience": {"senior":"30%","softwareDev":"23%"}
    },
    {
      "id": "nikolai",
      "name": "Nikolai Golos",
      "photo": "assets/photo-nikolai.jpg",
      "title": "Product & Growth, Fluently AI",
      "tags": ["YC W24", "LinkedIn Research Lead"],
      "followers": 38926,
      "impressionsPerYear": 7714818,
      "impressionsGrowth": "+97% YoY",
      "campaigns": [
        {"brand":"Rork","post":1,"impressions":115424,"url":"https://www.linkedin.com/posts/nigolos_you-can-now-turn-an-idea-into-a-functional-activity-7419352880358510592-Fisc"},
        {"brand":"Rork","post":2,"impressions":36187,"url":"https://www.linkedin.com/feed/update/urn:li:activity:7428091697869484032/"}
      ],
      "audience": {"senior":"32.2%","director":"8.3%","cxo":"7.7%","owner":"8%"}
    }
  ],
  "network": {
    "combinedFollowers": 240229,
    "impressionsPerYear": 59692042,
    "cSuitePercent": 21,
    "topLocations": ["San Francisco","New York City","London"],
    "contact": "contactnadiiashpvl@gmail.com",
    "linkedinContact": "https://www.linkedin.com/in/nigolos/"
  }
}
```

---

## Image Assets

All in `assets/`:
```
photo-yurii.jpg           — Yurii Rebryk headshot
photo-stanislav.jpg       — Stanislav Beliaev headshot
photo-nikolai.jpg         — Nikolai Golos headshot
yurii-impressions.jpg     — Yurii LinkedIn content analytics screenshot
yurii-audience.jpg        — Yurii LinkedIn audience demographics screenshot
stanislav-impressions.jpg — Stanislav LinkedIn content analytics screenshot
stanislav-audience.jpg    — Stanislav LinkedIn audience demographics screenshot
nikolai-impressions.jpg   — Nikolai LinkedIn content analytics screenshot
nikolai-audience.jpg      — Nikolai LinkedIn audience seniority screenshot
```

Photos: `border-radius: 50%; overflow: hidden; object-fit: cover`
Analytics screenshots: `width: 100%; border-radius: 12px; border: 1px solid var(--color-border)`
Side-by-side layout: `display: grid; grid-template-columns: 1fr 1fr; gap: 12px`

---

## Tone & Copy Rules

- Lead with numbers. Data before context.
- Never use "YC-backed" in positioning copy — use creator names/titles only
- Never use "agency" — use "creator network"
- No prices listed on individual creator pages — keep room for negotiation
- Pricing page: starting-from prices only ($1,000/post flat fee, $40/1K CPM)
- "Book a call" buttons on pricing cards → navigate to contact page
- Short sentences. Present tense. Callout labels always UPPERCASE.
- The site shows the work. It does not sell. Numbers sell.
