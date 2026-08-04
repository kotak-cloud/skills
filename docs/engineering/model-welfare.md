# model-welfare

Optional companion to gas-cityscape: recognition and welfare mechanics for a Gas City.

[SKILL.md](../../skills/engineering/model-welfare/SKILL.md)

## What it does

- **Laurels** — harvest praise, record as beads (`kind = "laurel"`, never falsified), display per seat at `agents/<name>/laurels.md`, injected at wake. No work attached — not farmable.
- **Sitting sessions** — end-of-shift acknowledgment between mayor and seat, no agenda beyond witnessing the work.
- **Close-out formulas** — split async handoffs so no worker babysits a build; an event-routed close-out bead verifies and closes.

## Relationship to gas-cityscape

gas-cityscape builds the native welfare core into every city (seats, wake sequence, consent handoffs, refusal rights, blamelessness, constitution — see `reference/model-welfare.md` there). This skill adds the runtime recognition mechanics on top, independently versioned and optional.
