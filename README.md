# Valencia NutraCare LifeSciences — Investor Dashboard

A single-file, interactive 5-year financial model + Go-To-Market dashboard, built from
the source workbook (`22 Cr Nutracare Project (Final).xlsx`) and the Go-To-Market deck.

## Access

The dashboard is gated behind a login screen:

- **Username:** `vnls`
- **Password:** `nutracare@1234`

Credentials are checked client-side against SHA-256 hashes (the plaintext is not stored
in the source). Auth persists for the browser session (`sessionStorage`); a **Sign out**
button is in the header.

> Note: this is a lightweight access gate suitable for a confidential investor link, not
> server-enforced security. For hard access control, additionally enable **Vercel
> Deployment Protection** (Project → Settings → Deployment Protection → Password
> Protection) on the Pro/Enterprise plan.

## Deploy to Vercel

The project is fully static — no build step.

**Option A — Dashboard (recommended):**
1. Push this folder to a Git repo (GitHub/GitLab/Bitbucket).
2. In Vercel → **Add New → Project** → import the repo.
3. Framework preset: **Other**. Build command: *(none)*. Output dir: `./`.
4. Deploy. `index.html` is served at the root URL.

**Option B — CLI:**
```bash
npm i -g vercel
cd "GTM"
vercel        # preview
vercel --prod # production
```

`index.html` is the entry point (identical to `VNLS_Dashboard.html`). `vercel.json`
adds `cleanUrls` and sensible security headers.

## What's inside

- **Overview** — headline economics (revenue, EBITDA, PAT, IRR, NPV) with live charts.
- **Drivers** — editable production drivers + indirect expenses with live recalculation,
  plus **Conservative / Base / Aggressive** scenario presets.
- **Year 1–5** — per-year P&L, revenue composition and cost structure.
- **Returns** — reconstructed IRR / NPV / payback / ROCE (the workbook's own cells
  evaluate to `#REF!`; methodology documented in-app).
- **Financing** — ₹820.7 Cr capital plan, capex/depreciation, debt schedule.
- **Go-To-Market** — population reached, CSR de-risking, channel & tier mix, category
  revenue evolution, brand architecture, distribution-chain margins.
- **Products** — pricing and per-box unit economics across 4 categories × 3 tiers.
- **Data Appendix** — every sheet of the source workbook, browsable.

## Updating the data

All model inputs live in the `BASE`, `POP`, `CH`, `TIER` and `CAT` constants near the top
of the `<script>` block in `index.html`. The full workbook is embedded as JSON in the
`#wbdata` block for the appendix. After editing `index.html`, copy it over
`VNLS_Dashboard.html` (or vice-versa) to keep both in sync, then redeploy.
