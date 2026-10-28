# Roger's Guide

Roger King's business desk for Pitch an Angel. A static site with no build step, deployed by Vercel from `main` to rogers-tech-guide.vercel.app.

## What is where

| File | What it is |
|---|---|
| `index.html` | The guide (October 2026). Five tabs: Today, Plan, Offers, ChatGPT, Build, plus the 30-day test at `#check`. Plain JavaScript, no framework |
| `kit/` | Product samples linked from the Build tab: the personal workbook, the cohort workshop, the Full Program overview, the Pitch Clinic, the recorded course, the mock panel scorecard. Each prints cleanly |
| `kit/roger-chatgpt-offers-and-outreach.md` | Copy of the ChatGPT knowledge file. The source is `docs/For Roger's ChatGPT - offers and outreach.md` in `kingconnect11/pitch-to-an-angel`; keep the two identical |
| `classic.html` | The original February 2026 guide (Claude, social media, photography, travel). `ARCHITECTURE_PLAN.md` describes it |
| `images/` | Photos. `roger-hero.jpg` is a crop of `roger-excited-panel.jpg` |
| `apple-touch-icon.png`, `icon-*.png`, `manifest.webmanifest` | Home screen icon and app settings |
| `robots.txt` | Keeps search engines out. Every page also carries `noindex` |

## Changing things

- **Prices, offers, the calculator, message templates and prompts** are data arrays near the top of the script in `index.html` (`OFFERS`, `CALC`, `RECIPES`, `MESSAGES`, `PROMPTS`). Edit the text there.
- **The weekly checklists** are in `WEEKS`. Dates are fixed to the 28 October to 18 November plan.
- **What Roger types is stored only in his browser** (`localStorage`, keys starting `rg2.`). Nothing is sent anywhere. A second device starts empty.

## The reasoning

The plan behind the guide, the hours math for the Full Program, and the split options are in `docs/2026-10-28-roger-business-plan.md` in `kingconnect11/pitch-to-an-angel`.

## Writing rules

No long dashes or double hyphens in anything Roger or a founder reads. Plain words, sentence case, large type.
