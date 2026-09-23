# CWI Masters API — v1

The verified machine-readable catalog of Cumulative Web Inc, served as
static JSON. Zero auth, zero rate limits on the free tier, $0 infrastructure.

Base URL (planned): `https://cumulativewebinc.github.io/masters`

## Endpoints

| Endpoint | What |
|---|---|
| `/v1/manifest.json` | Version, counts, tier/ISRC tallies, endpoint list |
| `/v1/catalog.json` | All 52 track records, full fidelity |
| `/v1/tracks/{track_id}.json` | One track: `derived` envelope + full `record` |
| `/v1/indexes/by-artist.json` | artist → [track_ids] |
| `/v1/indexes/by-isrc.json` | verified ISRC value → track_id |
| `/v1/indexes/by-tier.json` | silver / bronze → [track_ids] |
| `/v1/llms.txt` | LLM-ingestible catalog summary (llmstxt.org convention) |
| `/v1/llms-full.txt` | Expanded per-track summary |
| `/v1/sync/availability.json` | Per-track sync status (fail-closed) |
| `/v1/sync/inquiry-schema.json` | JSON Schema for inbound sync inquiries |

## The `derived` envelope

Every track file carries a machine-first summary:

```json
{
  "track_id": "that-boy-hi-hat-diabolique",
  "title": "Diabolique",
  "artist": "That Boy Hi Hat",
  "tier": "silver",
  "isrc": { "value": "QZ8EF2666377", "status": "verified" },
  "is_stale": false,
  "sync_availability": { "status": "blocked_missing", "reasons": ["publishing splits unverified"] },
  "canonical_url": "https://cumulativewebinc.github.io/masters/v1/tracks/that-boy-hi-hat-diabolique.json"
}
```

## Evidence tiers

- **silver** — identifiers verified from the distributor dashboard (label-provided).
- **bronze** — identifiers from public sources, not distributor-confirmed.
- **conflicted** — sources disagree; `value` is `null`, candidates documented in the record. Dashboard values are authoritative and flagged to the label.
- **unknown** — no source anywhere; never guessed.

## Sync front door

`sync_availability.status` is `blocked_missing` unless one-stop is claimed
and splits/PRO are verified. An inquiry submitted against the
`inquiry-schema.json` is **inbound only** — it creates a structured payload
for CWI Affairs review. It licenses nothing by itself.

## Versioning

SemVer, additive-only. v1 will never rename or remove a field.
