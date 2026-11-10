# Roger's Tech Guide

## What This Is

A personal technology guide built by Philip King for his father Roger King (77). It's a single-page React app that teaches Roger how to use AI (Claude), social media, and technology. It's designed to feel like a premium, editorial magazine — warm, personal, and approachable.

**Live site:** Hosted on Vercel (auto-deploys from `vercel deploy --prod`)
**Repo:** https://github.com/kingconnect11/rogers-tech-guide (branch: main)

## Architecture

**Single file app.** Everything lives in `index.html` — styles, components, data, and logic. There is no build step, no bundler, no package.json.

- **React 18** via CDN (unpkg)
- **Babel Standalone** for JSX transpilation in-browser
- **No framework / no build tooling** — just open `index.html`
- **Vercel** for hosting (static site, `vercel.json` routes to `index.html`)

### File Structure

```
/
├── index.html          # THE app — all HTML, CSS, JS, React components
├── vercel.json         # Vercel routing config
├── .vercelignore       # Excludes optimized images, dev files
├── .gitignore
├── images/             # All photos (MUST be lowercase — see below)
│   ├── roger-bay-angels.jpg
│   ├── roger-cool-glasses.jpg
│   ├── roger-julie-canoe.jpg
│   ├── roger-networking.jpg
│   ├── roger-with-camera.jpg
│   ├── roger-excited-panel.jpg
│   ├── roger-julie-car-show.jpg
│   ├── roger-gangster-suit.jpg
│   ├── roger-bay-angels-panel.jpg
│   ├── roger-with-family.jpg
│   ├── roger-family-toast.jpg
│   ├── roger-and-sons.jpg
│   ├── roger-and-mike.jpg
│   ├── roger-with-camera.jpg
│   └── family-property.jpg
├── ARCHITECTURE_PLAN.md
├── Roger_King_Tech_Guide_Handoff.md
└── CLAUDE.md           # This file
```

### CRITICAL: Image Directory Must Be Lowercase

The `images/` directory MUST remain lowercase. macOS is case-insensitive, but Vercel runs on Linux (case-sensitive). If the directory is `Images/` (uppercase), all image requests will 404 on Vercel and fall through to `index.html` via the catch-all route.

## Design Language

### Typography
- **Headings:** Playfair Display (serif) — elegant, editorial
- **Body:** Source Sans 3 (sans-serif) — clean, readable
- **Accents/Notes:** Caveat (handwritten cursive) — personal, warm
- **Code/Prompts:** JetBrains Mono (monospace)

### Color Palette (CSS custom properties)
```css
--navy: #0f1b2d          /* Primary dark — headings, nav */
--navy-light: #1e3352
--cream: #faf7f2          /* Background */
--ivory: #f2ebe0          /* Secondary background */
--gold: #c4894a           /* Primary accent — active states, highlights */
--gold-light: #d4a46a
--gold-dark: #a06b30
--warm-blue: #3d6898      /* Info accents */
--sage: #6b9e72           /* Success/tip accents */
--sage-light: #a8c5ab
--rose: #c47a6c           /* Warning accents */
```

### Design Patterns
- **Paper grain texture** on body (subtle SVG noise overlay at 3% opacity)
- **Cards** with hover lift + gold underline animation
- **Accordions** for collapsible content sections
- **Prompt blocks** (`.pb`) — dark navy blocks with copy button and shimmer gradient
- **Setup blocks** — configuration tags before prompts (model, mode, features)
- **Callout boxes** (`.co`) — gold/sage/blue left-border callouts
- **Photo posts** — social media post templates with copy-to-clipboard captions
- **Scroll reveal** — elements animate in via IntersectionObserver
- **Ken Burns** hero background with parallax
- **Focal point system** — customizable `object-position` per image via `?edit` URL param

### Spacing / Layout
- Max content width: `760px` (`--content-max`)
- Sidebar width: `260px` (desktop only, >=1024px)
- Nav height: `72px`
- Border radius: `12px` / `20px` (large) / `8px` (small)

## How the App Works

### Navigation
- **Mobile (< 1024px):** Fixed bottom nav bar with 6 buttons (Home, Start, AI, Social, Travel, More)
- **Desktop (>= 1024px):** Fixed left sidebar with all sections listed
- Navigation uses hash-based routing (`window.location.hash`)
- Page transitions use a fade-out/fade-in animation

### Sections
Defined in the `SECTIONS` array. Each section has:
- `id` — URL hash identifier
- `title` — display name
- `sub` — subtitle
- `icon` — emoji
- `label` — short label for hero overlays
- `cc` — CSS class for card color accent
- `img` — hero/card image path
- `alt` — image alt text

Each section is a React component (S1-S7 currently) rendered via the `MAP` object in `App()`.

### Key Components
| Component | Purpose |
|-----------|---------|
| `Acc` | Accordion — collapsible content block with optional progress checkbox |
| `PB` | Prompt Block — dark code block with copy-to-clipboard |
| `Setup` | Setup Block — shows model/mode/feature tags before a prompt |
| `Steps` | Numbered step-by-step instructions |
| `CTable` | Responsive data table |
| `FPT` | Fun Prompt Tile — tap-to-copy prompt card |
| `PostCard` | Social media post template with image, platforms, caption |
| `CPhoto` | Content photo with caption |
| `SPage` | Section page wrapper — hero image, back button, floating progress |
| `Landing` | Home page with hero + card grid |
| `FocalImage` | Image with customizable focal point (object-position) |

## How to Add a New Section

1. **Add to `SECTIONS` array** (~line 482):
```jsx
{id:'my-section', title:'My Section', sub:'Description', icon:'🎯', label:'Label', cc:'cg', img:'images/some-photo.jpg', alt:'Alt text'},
```

2. **Add to `NAV` array** (~line 492) if it should appear in the bottom nav (max ~6 items):
```jsx
{id:'my-section', label:'Short', icon:I.sparkles},
```

3. **Create the section component** (follow the S1-S7 pattern):
```jsx
function S8({section, onBack, prog, toggle}) {
  return (
    <SPage section={section} onBack={onBack}>
      <div className="sintro"><p>Intro text here.</p></div>
      <Acc title="First Topic" id="ms-1" prog={prog} toggle={toggle}>
        <p>Content here.</p>
      </Acc>
    </SPage>
  );
}
```

4. **Register in the `MAP` object** (~line 1128):
```jsx
const MAP = {..., 'my-section': S8};
```

5. **Update `activeNav` logic** (~line 1131) if the section should highlight a nav item.

## How to Add Tips/Accordions Within a Section

Just add another `<Acc>` inside the section component:

```jsx
<Acc title="Your Tip Title" id="unique-id" prog={prog} toggle={toggle}>
  <p>Content here. Use standard HTML-in-JSX.</p>
  <PB text={`Prompt text here that users can copy.`}/>
  <div className="co"><div className="co-l">Callout label</div><p>Callout text.</p></div>
</Acc>
```

The `id` must be unique across the entire app (used for progress checkboxes in localStorage).

## How to Add a Prompt Block

```jsx
<Setup model="Sonnet 4.6" mode="Chat" features={['Extended Thinking']} tip="Optional tip text"/>
<PB text={`Your prompt text here. Use \n for line breaks.`}/>
```

The `Setup` block shows configuration tags. The `PB` block is the dark copyable prompt.

## How to Add Images

1. Place the image in `images/` (lowercase!)
2. Reference it as `images/filename.jpg` in the JSX
3. Use `<FocalImage>` for hero/card images (supports custom focal points)
4. Use `<CPhoto>` for inline content photos with captions
5. Add a default focal point in `DEFAULT_FOCAL` if needed (~line 375)

## Deployment

```bash
# From project root
vercel deploy --prod --yes
```

No build step. Vercel serves `index.html` as a static site. The `vercel.json` config routes all non-file requests to `index.html` (SPA behavior).

## Local Development

Just open `index.html` in a browser. No server needed for basic viewing, though image paths may need a local server:

```bash
npx serve .
# or
python3 -m http.server 8000
```

### Focal Point Editor

Add `?edit` to the URL to enter focal point editing mode. Click on images to set the crop center point. Export the config and paste into `DEFAULT_FOCAL`.

## State / Persistence

- **Progress checkboxes:** `localStorage` key `rg-prog` — JSON object of completed accordion IDs
- **Focal points:** `localStorage` key `rg-focal` — custom image focal point overrides
- **Current page:** URL hash (`#section-id`)

## Tone and Voice

This guide is written from Philip to Roger. It should feel:
- Warm, personal, encouraging
- Never condescending or overly technical
- "Philip's take" callouts add a personal recommendation layer
- Caveat (handwritten) font used for personal notes
- Roger is 77, founder of Bay Angels, photographer — treat him with respect and acknowledge his accomplishments
