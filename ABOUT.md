# MediaKit — Website Master Prompt

> Paste this file into Cursor, Claude, v0, or any AI coding tool to regenerate or extend this website.

---

## Project Overview

**Name:** MediaKit  
**What it is:** A LinkedIn creator media kit website for a network of 3 YC-backed founders  
**Brand name:** MediaKit (NOT "Trendz", NOT "agency")  
**Positioning:** LinkedIn Creator Network for B2B Startups — NOT an agency  
**Purpose:** Sell sponsored post partnerships to startup brands  
**Contact:** contactnadiiashpvl@gmail.com  
**LinkedIn:** https://www.linkedin.com/in/nadiia-shapovalova-25653628a

---

## Visual Design System

Replicated from the Higgsfield LinkedIn Research document (trendy-linkedin.pages.dev). Do NOT redesign — map content into this structure.

### Colors
```
Background:      #0d0d0d
Card bg:         #141414
Card bg alt:     #1a1a1a
Border:          #1e1e1e
Border subtle:   #2a2a2a
Accent red:      #e63946
Red dim:         rgba(230, 57, 70, 0.12)
Red border:      rgba(230, 57, 70, 0.25)
Text primary:    #ffffff
Text secondary:  #aaaaaa
Text muted:      #666666
Text very muted: #444444
Text dim:        #333333
```

### Typography
- Font: Inter (Google Fonts)
- H1: 1.75rem, weight 800, letter-spacing -0.03em
- Metric values: 1.5–2rem, weight 800
- Body: 0.875rem, weight 400, line-height 1.6
- Badges/labels: 0.65rem, weight 700, letter-spacing 0.1em, UPPERCASE
- Subtitles: 0.875rem, color #666

### Layout
- Full-height app shell: `display: flex; height: 100vh; overflow: hidden`
- Left sidebar: fixed 220px wide, `background: #111`, border-right `#1e1e1e`
- Main content: flex: 1, page stack with `overflow: hidden`
- Pages: `position: absolute; inset: 0; overflow-y: auto; padding: 40px 48px`
- Only one page visible at a time — toggle `.active` class via JavaScript

### Page Loader
- Full-screen overlay on initial load
- Spinner: 32px, border `#222`, border-top `#e63946`, spin animation
- Fades out after 600ms via `.done { opacity: 0; pointer-events: none }`

---

## Page Structure

### Sidebar Navigation (left, fixed)
```
00  Cover
01  Overview
02  Combined Reach
03  Yurii Rebryk
04  Stanislav Beliaev
05  Nikolai Golos
06  Audience
07  Results
08  Pricing
09  Book a Call
```

Nav button structure:
```html
<button class="nav-btn active" onclick="setPage('cover')">
  <span class="nav-num">00</span>
  <span class="nav-label">Cover</span>
</button>
```

Active state: `background: #1e1e1e; color: #fff`  
Active num: `color: #e63946`

### Page 00 — Cover
- Centered layout, full height
- 3 creator initials in circles: YR, SB, NG
- Title: "LinkedIn Creator Network for B2B Startups"
  - "B2B Startups" in `color: #e63946`
- Subtitle: "Three YC-backed founders. One high-trust audience of decision-makers."
- 3 metric badges: 240K+ followers | 5M+ monthly impressions | 21% Founders & C-suite
- CTA button: "Start reading →" → goes to page 'overview'
  - Style: `background: #e63946; color: #fff; padding: 12px 28px; border-radius: 8px`

### Page 01 — Overview (TL;DR)
Structure: 2-column grid of cards (`.tldr-grid`)

**Card 01 — "The network":**
- Metric grid (3 cells with dividers):
  - 240K+ / Combined followers
  - 5M+ / Monthly impressions  
  - 21% / Founders & C-suite

**Card 02 — "Why it works":**
- 4 bullet points with red dot indicators:
  - YC-backed founders — built-in credibility
  - Organic distribution — no paid amplification
  - 2–3%+ CTR vs LinkedIn Ads' 0.4%
  - B2B decision-makers — VCs, CMOs, growth leads

**Bottom lever cards** (3-column grid):
```
Creator 01 | Yurii Rebryk    | 129K followers · $4,500/post
Creator 02 | Stanislav Beliaev | 72K followers · $3,500/post
Creator 03 | Nikolai Golos   | 39K followers · $2,000/post
```

### Page 02 — Combined Reach
- KPI row (4 cards): 240K+ | 5M+ | 21% (red) | SF·NYC·London
- Bar chart comparing 3 creators:
  - Yurii: 100% width, `background: #e63946` (accent)
  - Stanislav: 56% width, `background: #8a2020` (mid)
  - Nikolai: 30% width, `background: #3a1a1a` (low)
- Red callout arrow: "Combined: 240,229 followers · #1 in SF startup ecosystem"

### Page 03 — Yurii Rebryk
- Badge: "Creator 01"
- Creator hero card (2-column: info left, metrics right)
  - Avatar circle: initials "YR"
  - Tags: YC W24 (red), Ex-Google, Ex-NVIDIA, Forbes 30u30 (red)
  - Metric cards (right column, accent border left): 129K followers | ~2.5M impressions/mo | $4,500/post
- Red callout: "↑ Largest creator in network · 21% Founders & C-suite audience"
- Red highlight line (2px solid #e63946)
- Campaign results (2-column grid):
  - Framer Post 1: ↑ 529,582 impressions (red arrow, emphasized)
  - Framer Post 2: 18,783 impressions
- Audience placeholder: `[AUDIENCE SCREENSHOT — YURII]`
- Audience stats: 21% Founders & C-suite (red) | SF · NYC | London

### Page 04 — Stanislav Beliaev
- Badge: "Creator 02"
- Same hero structure as Yurii
  - Avatar: "SB"
  - Tags: YC W24 (red), ex-NVIDIA
  - Metrics: 72K followers | $3,500/post
- Red callout: "Technical founder — strong reach with engineering & AI audiences"
- Audience placeholder: `[AUDIENCE SCREENSHOT — STANISLAV]`

### Page 05 — Nikolai Golos
- Badge: "Creator 03"
- Same hero structure
  - Avatar: "NG"
  - Tags: YC W24 (red), LinkedIn Research Lead
  - Metrics: 39K followers | $2,000/post
- Red callout: "Growth & product audience · highest engagement rate in network"
- Campaign results:
  - Rork Post 1: ↑ 115,424 impressions
  - Rork Post 2: 36,187 impressions
- Audience placeholder: `[AUDIENCE SCREENSHOT — NIKOLAI]`

### Page 06 — Audience
- Audience stats row: 21% (red) | 240K+ | SF · NYC · LDN
- Red callout: "Tier 1 markets — San Francisco, New York City, London"
- Red highlight line
- 3 image placeholders in grid:
  - `[AUDIENCE SCREENSHOT — YURII REBRYK]`
  - `[AUDIENCE SCREENSHOT — STANISLAV BELIAEV]`
  - `[AUDIENCE SCREENSHOT — NIKOLAI GOLOS]`
- Implementation note: replace with LinkedIn Analytics screenshots showing job titles, seniority, industries, geography

### Page 07 — Results
- Performance comparison bar (red panel):
  - Our CTR: 2–3%+ (red, 1.75rem)
  - LinkedIn Ads avg: 0.4% (muted)
  - Better: ~10× (white)
- Framer campaign:
  - Post 1: ↑ 529,582 impressions (red arrow emphasized)
  - Post 2: 18,783 impressions
  - Combined: 548,365
- Rork campaign:
  - Post 1: ↑ 115,424 impressions
  - Post 2: 36,187 impressions
  - Combined: 151,611

### Page 08 — Pricing
3-column pricing cards:

**Card 1: Network Bundle — $8,000 (FEATURED)**
- `border-color: #e63946; background: #161010`
- Radial gradient overlay: `rgba(230,57,70,0.08)`
- Line items with red dots:
  - 1× Yurii post (129K) — $4,500 value
  - 1× Stanislav post (72K) — $3,500 value
  - 1× Nikolai post (39K) — $2,000 value
  - 240K+ combined reach · 3 posts
- Red callout box: "↑ Save $2,000 vs. buying posts individually"

**Card 2: Single Post — $2,000–$4,500**
- Yurii: $4,500 | Stanislav: $3,500 | Nikolai: $2,000
- 1 revision + performance report

**Card 3: CPM — $45/1K impressions**
- Pay per impressions delivered
- vs LinkedIn Ads: $33-65 CPM, 0.4% CTR
- Red callout: "~10× better CTR than LinkedIn Ads"

### Page 09 — Book a Call
- Centered layout
- Title: "Let's talk partnerships"
- Two buttons:
  - Primary (red): "Send an email →" → mailto:contactnadiiashpvl@gmail.com
  - Secondary (dark): "LinkedIn ↗" → https://www.linkedin.com/in/nadiia-shapovalova-25653628a
- Email display: contactnadiiashpvl@gmail.com

---

## Creator Data

```json
{
  "creators": [
    {
      "id": "yurii",
      "name": "Yurii Rebryk",
      "initials": "YR",
      "title": "Founder & CEO, Fluently AI",
      "bio": "YC W24 · Ex-Google · Ex-NVIDIA · Forbes 30u30",
      "followers": 129126,
      "followersDisplay": "129K",
      "estimatedMonthlyImpressions": 2500000,
      "linkedin": "https://www.linkedin.com/in/yurii-rebryk/",
      "pricePerPost": 4500,
      "campaigns": [
        {"brand": "Framer", "post": 1, "impressions": 529582},
        {"brand": "Framer", "post": 2, "impressions": 18783}
      ]
    },
    {
      "id": "stanislav",
      "name": "Stanislav Beliaev",
      "initials": "SB",
      "title": "Co-Founder & CTO, GetFluently.App",
      "bio": "YC W24 · ex-NVIDIA",
      "followers": 72177,
      "followersDisplay": "72K",
      "linkedin": "https://www.linkedin.com/in/stanislav-beliaev/",
      "pricePerPost": 3500,
      "campaigns": []
    },
    {
      "id": "nikolai",
      "name": "Nikolai Golos",
      "initials": "NG",
      "title": "Product & Growth, Fluently AI",
      "bio": "YC W24",
      "followers": 38926,
      "followersDisplay": "39K",
      "linkedin": "https://www.linkedin.com/in/nigolos/",
      "pricePerPost": 2000,
      "campaigns": [
        {"brand": "Rork", "post": 1, "impressions": 115424},
        {"brand": "Rork", "post": 2, "impressions": 36187}
      ]
    }
  ],
  "network": {
    "combinedFollowers": 240229,
    "combinedFollowersDisplay": "240K+",
    "monthlyImpressions": 5000000,
    "monthlyImpressionsDisplay": "5M+",
    "cSuiteAudiencePercent": 21,
    "topAudiences": ["San Francisco", "London", "New York City"],
    "networkBundlePrice": 8000,
    "singlePostRange": "$2,000–$4,500",
    "cpmPrice": 45
  }
}
```

---

## Visual Emphasis System

### Red Highlight Line
```html
<div class="highlight-line"></div>
```
```css
.highlight-line { height: 2px; background: #e63946; border-radius: 1px; margin: 4px 0 12px; }
```
Use under: key metric numbers, section headings, creator stats

### Red Arrow Callout
```html
<div class="callout-row">
  <div class="callout-arrow">↑</div>
  <div class="callout-label">21% Founders & C-suite</div>
</div>
```
```css
.callout-arrow { color: #e63946; font-size: 1rem; font-weight: 700; }
.callout-label { font-size: 0.7rem; color: #e63946; font-weight: 600; letter-spacing: 0.05em; text-transform: uppercase; }
```
Use on: large impression numbers, follower counts, CTR comparisons

### Red Badge
```html
<span class="badge badge-red">YC W24</span>
```
Use on: creator tags, "Most popular" tier, key audience facts

### Accent Border Card
```html
<div class="creator-metric-card accent-border">
```
```css
.accent-border { border-left: 3px solid #e63946; }
```
Use on: primary metric card per creator (followers)

### Red Metric Value
```html
<div class="kpi-value" style="color: #e63946">21%</div>
```
Use on: the 21% C-suite metric wherever it appears

---

## JavaScript Navigation

```javascript
// Page map: key → page element ID + nav button ID
const pageMap = {
  'cover':     { page: 'page-cover',     nav: 'nav00' },
  'overview':  { page: 'page-overview',  nav: 'nav01' },
  // ... etc
};

function setPage(key) {
  // Remove .active from current page + nav btn
  // Add .active to new page + nav btn
  // Scroll new page to top
  // Update window.location.hash
}

// Keyboard: ArrowRight/Down = next, ArrowLeft/Up = prev
// Hash routing: read window.location.hash on load
```

---

## File Structure

```
mediakit/
├── index.html          ← All pages in one file (page stack)
├── assets/
│   └── theme.css       ← Design system
├── data/
│   └── creators.json   ← Creator & network data
├── ABOUT.md            ← This file (master AI prompt)
└── README.md           ← Setup & deployment
```

---

## Implementation Notes

### DO NOT
- Use "Trendz" anywhere
- Use "agency" in positioning — use "creator network" or "MediaKit"
- Merge creators onto one page
- Change the sidebar nav structure
- Add a build step — must work by opening index.html directly
- Invent fake metrics

### DO
- Replace `img-placeholder` divs with actual LinkedIn Analytics screenshots
- Keep the Higgsfield visual DNA: dark, data-first, left sidebar, page stack
- Use Inter font from Google Fonts
- Keep all HTML/CSS/JS in index.html + assets/theme.css (no build tools)
- Add creator photo `<img>` tags once photos are available (replace avatar initials)

### Deployment
- **GitHub Pages:** push to `main` branch → Settings → Pages → Source: main / root
- **Cloudflare Pages:** connect GitHub repo → build: none, output: `/`
- **Local:** open `index.html` in any browser

### GitHub Access
To share with collaborator:  
GitHub → Repository → Settings → Collaborators → Add people → `n.golos.suai@gmail.com`

---

## Tone & Copy Rules

- Direct. Results-driven. No fluff.
- Lead with numbers: impressions, followers, CTR
- Never use superlatives without data ("best", "top") — use the data itself
- Avoid "agency", "influencer marketing agency", "we are an agency"
- Use: "creator network", "founder-led marketing", "partnership"
- Short sentences. Data first. Context second.
