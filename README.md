# Tokyo Debunker — SSR Card Ranking Archive (Darkwick Archive)

A wiki + ranking system for **all 147 SSR character cards** in *Tokyo Debunker*.
Every card is scored on a TU · MP · Speed combat model and ranked accordingly.

Built as a **single HTML file + local images**, so it runs with no build step or server and deploys to GitHub Pages as-is.

## Features

- **147 SSR cards** in a grid — tier badge (S/A/B/C/D) + ranking score
- **Filters**: search (card, character, skill text), house (8), card type color (Red/Green/Blue), skill type (P.ATK/S.ATK)
- **Sort**: rank score / speed / card name / character
- **Card detail**: `Character: Card Name`, card type, skill type, Unique/Active/Passive skills, combat readout (entry delay · MP gauge · action delay), score breakdown
- **Ranking weight sliders**: Offense / Burst / Speed / MP Economy / Utility, adjustable in real time

## Combat model

- **Entry delay** = `ceil((Speed − 100) / 10)` — lower acts sooner
- **Action delay** = `ceil((skill TU − 100) / 10)` — how far a skill pushes back your next action
- **MP** starts at 5, range 0–10 (never below 0), shifts per skill
- **All-target skills** are scored against a 3-enemy encounter

The ranking score normalizes five axes (Offense · Burst · Speed · MP Economy · Utility)
0–100 across the full card pool, then takes a weighted average. Weights are adjustable in the UI.

## Deploy to GitHub Pages

1. Push this folder to a GitHub repo (with `index.html` at the repo root):
   ```bash
   git init
   git add .
   git commit -m "Tokyo Debunker SSR card archive"
   git branch -M main
   git remote add origin https://github.com/<user>/<repo>.git
   git push -u origin main
   ```
2. Repo **Settings → Pages**
3. Set **Source** to `Deploy from a branch`, **Branch** to `main` / `/ (root)`, then Save
4. The site goes live at `https://<user>.github.io/<repo>/`

> To deploy from `/docs` instead, put these files under `docs/` and pick `/docs` as the Pages source.

## Data source & notes

- Data (skills, TU, MP, Speed, etc.) is compiled from the Tokyo Debunker community wiki (Fandom, CC BY-SA). Card labels are reconstructed in `Character: Card Name` form.
- Cards with blank stats in the source have their Speed filled with the median; these are marked "est." in the detail view.
- Images are downloaded locally (`images/`) and optimized to 560px-wide WebP to avoid the source CDN's hotlink protection.
- Ranking scores are estimates under the model above and may differ from actual game balance.

## File structure

```
.
├── index.html        # the whole app (HTML + CSS + JS + inlined card data)
├── images/           # 147 card images (WebP)
├── .nojekyll         # disable Jekyll processing on GitHub Pages
└── README.md
```
