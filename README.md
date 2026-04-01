# MediaKit — LinkedIn Creator Network

A media kit website for a LinkedIn creator network managing 3 YC-backed founders with 240K+ combined followers.

## Quick Start

```bash
# No build step needed. Just open in browser:
open index.html
```

Or serve locally:
```bash
npx serve .
# → http://localhost:3000
```

## Project Structure

```
mediakit/
├── index.html          ← Main website (all pages)
├── assets/
│   └── theme.css       ← Design system & styles
├── data/
│   └── creators.json   ← Creator data (followers, pricing, campaigns)
├── ABOUT.md            ← Master AI prompt — use this to regenerate the site
└── README.md           ← This file
```

## Customization

### Adding Audience Screenshots
Replace the placeholder divs in each creator section:
```html
<!-- Find this: -->
<div class="img-placeholder">
  <div class="img-placeholder-label">Audience Screenshot — Yurii</div>
</div>

<!-- Replace with: -->
<img src="assets/yurii-audience.png" alt="Yurii Rebryk LinkedIn audience breakdown" style="width:100%;border-radius:8px;">
```

### Adding Creator Photos
Replace avatar initials with photos:
```html
<!-- Find: -->
<div class="creator-avatar">YR</div>

<!-- Replace with: -->
<img src="assets/yurii-photo.jpg" alt="Yurii Rebryk" style="width:72px;height:72px;border-radius:50%;object-fit:cover;">
```

### Updating Metrics
Edit `data/creators.json` — then update the corresponding HTML manually (the site doesn't dynamically load this file, it's for reference and AI regeneration).

## Deployment

### GitHub Pages
1. Push to GitHub repository
2. Settings → Pages → Source: `main` branch, `/ (root)`
3. URL: `https://yourusername.github.io/mediakit`

### Cloudflare Pages (recommended)
1. Connect GitHub repo to Cloudflare Pages
2. Build command: (leave empty)
3. Output directory: `/`
4. URL: `https://mediakit.pages.dev` (or custom domain)

### Netlify Drop
1. Drag the `mediakit/` folder to netlify.com/drop
2. Instant live URL

## Sharing Access

### GitHub Collaborator Access
To share repo with Nikolai:
1. GitHub → Your repo → **Settings** → **Collaborators**
2. Click **Add people**
3. Enter: `n.golos.suai@gmail.com`
4. Select role: **Write** (or Maintain)
5. They'll receive an email invitation

## AI Regeneration

To regenerate or extend this website with any AI tool:
1. Open `ABOUT.md`
2. Copy the entire contents
3. Paste into Cursor / Claude / v0 / Bolt
4. Prompt: "Build this website exactly as described"

The ABOUT.md contains the full design system, page structure, creator data, and visual rules needed to recreate the site from scratch.

## Contact

- Email: contactnadiiashpvl@gmail.com
- LinkedIn: https://www.linkedin.com/in/nadiia-shapovalova-25653628a
