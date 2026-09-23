# CWI Masters

The verified machine-readable catalog of **Cumulative Web Inc.** — served as a versioned static JSON API.

- **Live API:** https://cumulativewebinc.github.io/masters/v1/
- **Docs:** [API.md](API.md) · **License:** [LICENSE.md](LICENSE.md)

## What it is

52 verified track records (That Boy Hi Hat, Black Lansky, King Akeem, Dre50, Fleekz, 183 Wildboi, GregPorn) with ISRCs, credits, sync-availability flags, and provenance tiers — built for LLMs, agents, and platforms to ingest via `llms.txt`.

## Honest limits

- **8 silver / 44 bronze** provenance tiers. Bronze records are corroborated, not distributor-confirmed.
- **2 ISRC conflicts are served as `null` + flagged** (Diabolique, Rainbows And Roses vocal) — dashboard values are authoritative, nothing is resolved by assumption.
- **4 tracks have no ISRC anywhere** — served as `unknown`, never guessed.
- Sync rights are **fail-closed**: unverified splits → `blocked_missing`.
- Staleness: records past `stale_after_days` must be treated as unverified.

## Use

Free tier with attribution (see LICENSE.md). Commercial data licensing: **hp@cumulativeweb.com** — no public pricing without written approval.

Built by Cumulative Web Inc. $0 infrastructure.
