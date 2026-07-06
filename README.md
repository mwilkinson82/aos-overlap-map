# AOS — Role Overlap & Interaction Map

A standalone, self-contained analysis page for the ALP Operating System (AOS). It maps a
company's seats, people, and functional domains, then surfaces concentration, overlap, and
gaps — with a Neural Web view, an Overlap Matrix view, digested findings, per-node
deep-dives, and a recommended action sequence.

Currently pre-loaded with the **G&M V2** data. Everything is in one file (`index.html`) —
no build step, no dependencies, no server. Fonts (Instrument Serif, JetBrains Mono) load
from Google Fonts; everything else is inline.

---

## Deploy options (no viewer login required)

### Option A — Drop it into the AOS app (same domain, cleanest)
Copy `index.html` into the AOS app's static/public directory and route to it, e.g.:

    cp index.html <aos-app>/public/overlap-map.html

It then serves at `https://alpos.alpcontractorcircle.com/overlap-map.html` — on the exact
AOS domain, outside the sign-in gate, using your existing deploy pipeline. Best fit for
"a separate page on my AOS domain."

### Option B — GitHub Pages (fastest standalone link)
    gh repo create aos-overlap-map --private --source=. --remote=origin --push
    gh api -X POST repos/mwilkinson82/aos-overlap-map/pages -f build_type=legacy \
      -f 'source[branch]=main' -f 'source[path]=/'

Live at `https://mwilkinson82.github.io/aos-overlap-map/` within ~1 minute.
(Pages from a private repo requires GitHub Pro/Team; a public repo works on the free tier
but makes the source — including the names in `index.html` — publicly readable.)

Custom subdomain (optional): add a `CNAME` file containing e.g. `map.alpcontractorcircle.com`,
then create a DNS `CNAME` record pointing `map` → `mwilkinson82.github.io`.

### Option C — Vercel / Netlify
Connect this repo (or drag the folder into the dashboard). Auto-deploys; add a custom
domain in project settings.

---

## Editing the data
All data lives in the `<script>` in `index.html`: `PEOPLE`, `DOMAINS`, `DCOL`, and
`FINDINGS`. Swap those for another client and the whole tool re-derives. The long-term
plan is a generator that reads any client's accountability chart + scorecard from AOS and
builds these structures automatically.

## Note on privacy
The page displays real employee names and a candid role analysis. If it's reachable
without a login, treat the URL as sensitive. A private repo (Option A or B-private) keeps
the source out of public search; the rendered page is still viewable by anyone with the link.
