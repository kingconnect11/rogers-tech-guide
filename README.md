# Roger's Guide

Roger King's business desk for Pitch an Angel. A static site with no build step, deployed by Vercel from `main` to rogers-tech-guide.vercel.app.

## What is where

| File | What it is |
|---|---|
| `index.html` | The guide (October 2026). Six tabs: Today, Plan, Offers, Guide, ChatGPT, Build, plus the 30-day test at `#check`. Plain JavaScript, no framework. The Guide tab (`#guide/<part>`) is Roger's field guide deck from `kingconnect11/pitch-to-an-angel` (`docs/roger-field-guide/` on `claude/fervent-meitner-yc9q9c`), kept current here |
| `kit/` | Product samples linked from the Build tab: the personal workbook, the cohort workshop, the Full Program overview, the Pitch Clinic, the recorded course, the mock panel scorecard. Each prints cleanly |
| `kit/pitch-an-angel-chatgpt-package.zip` | Everything for Roger's ChatGPT project in one download: Start here, the project instructions and eight knowledge files. Built from `docs/roger-chatgpt-package/` in `kingconnect11/pitch-to-an-angel` with `node scripts/build-roger-chatgpt-package.mjs`; copy the new ZIP here whenever it is rebuilt. The prompts on the ChatGPT tab name files 05 and 06, so keep those names |
| `classic.html` | The original February 2026 guide (Claude, social media, photography, travel). `ARCHITECTURE_PLAN.md` describes it |
| `images/` | Photos. `roger-hero.jpg` is a crop of `roger-excited-panel.jpg` |
| `apple-touch-icon.png`, `icon-*.png`, `manifest.webmanifest` | Home screen icon and app settings |
| `robots.txt` | Keeps search engines out. Every page also carries `noindex` |

## Changing things

- **Prices, offers, the calculator, message templates and prompts** are data arrays near the top of the script in `index.html` (`PRICE`, `OFFERS`, `CALC`, `RECIPES`, `MESSAGES`, `PROMPTS`). Edit the text there.
- **Launch pricing** (`PRICE` and `LAUNCH_ENDS`) mirrors `app/lib/pricing.ts` in the pitch repo: launch prices with a "then" line until 30 November, list prices after. Keep the two in step.
- **The field guide chapters** are in `CHAPTER_HTML`.
- **The weekly checklists** are in `WEEKS`. Dates are fixed to the 28 October to 18 November plan.
- **What Roger types is stored only in his browser** (`localStorage`, keys starting `rg2.`). Nothing is sent anywhere. A second device starts empty.

## The reasoning

The plan behind the guide, the hours math for the Full Program, and the split options are in `docs/2026-10-28-roger-business-plan.md` in `kingconnect11/pitch-to-an-angel`.

## Writing rules

No long dashes or double hyphens in anything Roger or a founder reads. Plain words, sentence case, large type.
