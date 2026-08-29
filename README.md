# barrie-address-import

The **Barrie city checkout** of the address-import family — city #6,
scaffolded 2026-08-15 by the breadth-first onboarding loop (engine
`future-work/multi-city/onboarding-queue.md`). Status: **onboarding**. No
proposal published, no uploads made; the config is a first draft for
conflation baseline runs.

The pipeline lives in the engine repo,
[`address-importer-friend`](https://github.com/skfd/address-importer-friend)
(see its README for setup). This repo carries only Barrie's `config.toml`,
credentials (`.env.*`, gitignored, from the `.example` files), and — locally,
gitignored — `data/` with the OSM extract and `data/barrie/tool.db`.

```bash
cd ../address-importer-friend
python run.py --city-dir ../barrie-address-import
```

Source data: City of Barrie address points via the sibling
[`ontario-address-changes`](https://github.com/skfd/ontario-address-changes)
tracker (`data/barrie/barrie.db`, 63,341 active rows / 53,791 civic addresses
at snapshot 24, 2026-08-10). The 2026-08-12 portfolio survey measured the
gap in the high-80s percent.

Entry state probed 2026-08-15 (`onboarding/entry-state-2026-08-15.json`):
**greenfield** — CanVec 6.0 NRCan seed (689 of 969 sampled), the 2018 peak is
Matthew Darwin's `City of Barrie => Barrie` rename retag, and the rest is
organic: `Exasecond` surveyed housenumbers in 2020–21, `HitFilmMan` cleaned
interpolation lines in 2021, and `useless2764` was hand-adding building
addresses as recently as 2026-08-03. No import tags, no import wiki content.
An import target; courtesy contacts before the first changeset: Matthew
Darwin, Exasecond, useless2764 (currently active). Convention:
`addr:city=Barrie`, `addr:province=Ontario` (210 vs 4 `ON`).

Two engine capabilities were built for this city on scaffold day:
**lifecycle-status filtering** (Barrie publishes 3,369 `Pending` future
addresses and 49 `Temporary` — `[status] active_values = ["Current"]` keeps
them out of candidates and maintenance deltas) and the **street-from-full
derivation** (`street_from = "full"` was a never-exercised naive projection
that would have included the housenumber; it now strips the number prefix by
length, which survives Barrie's 18 dirty rows — "32PENNELL DR", the KIRKWOOD
WAY number/full disagreements — all catalogued QA finds for the city).

Other traits: ALL-CAPS abbreviated streets (title-cased on export since
2026-08-29, `[export] street_case`), 14.5% units (collapsed to civic), tiles subdivide the 10 ward
polygons (100.00% point coverage; Barrie publishes no neighbourhood fabric —
the only area layers are census dissemination areas). Barrie is a separated
city inside Simcoe County (the Guelph/Wellington containment shape).

Before any production upload: wiki proposal page, forum announcement, and
feedback window per the
[OSM Import Guidelines](https://wiki.openstreetmap.org/wiki/Import/Guidelines)
— Toronto's [`IMPORT_PROPOSAL.mediawiki`](https://github.com/skfd/toronto-2-address-import/blob/main/IMPORT_PROPOSAL.mediawiki)
is the template.

MIT licensed.
