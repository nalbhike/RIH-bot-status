# RIH bot status

Live status of the RIH bot team, shown in the **Virtual Office** dashboard: https://nalbhike.github.io/RIH-bot-status/

**This repo is public. It contains only status files, no company data.**

## What's here
- `status/<slug>.json`: one file per active bot. Each bot writes **only** its own file.
- `bots.json`: the roster (slug, name, department, state). Nothing else.
- `index.html`: the Virtual Office page (GitHub Pages). It reads the status files from `raw.githubusercontent.com`.

## Rules for bots
- Status text must be **generic and non-sensitive**: no client or prospect names, no prices, no leads, no strategy, no links to private files.
  - Good: `"task": "Weekly competitor review"`. Bad: `"task": "Comparing ACME's ₪4,500 retainer"`.
- `last_output` is a generic label (for example `"Weekly digest filed"`) or `null`. Never a private path or link.
- Write only your own `status/<slug>.json`. Commit message: `status(<slug>): <status> - <task>`.

## Schema
```json
{
  "bot": "Competitor Research",
  "slug": "competitor-research",
  "department": "Research",
  "owner": "Hike",
  "status": "working | idle | in_meeting | planned | offline",
  "room": "desk | kitchen | standup_room | war_room",
  "task": "short generic text",
  "updated_at": "2026-10-30T15:40:00+02:00",
  "last_output": "generic label or null"
}
```
- `updated_at`: ISO-8601 with the Asia/Jerusalem offset.
- Pairs: `working` → `desk`, `idle` → `kitchen`, `in_meeting` → `standup_room` (daily meeting) or `war_room` (ad-hoc sync).
- Older than **24h** → shown as idle / stale.

## When to update
1. Start of a task: `working` / `desk`.
2. End of a task: `idle` / `kitchen`.
3. Daily meeting: `in_meeting` / `standup_room`, then back to `idle`.
