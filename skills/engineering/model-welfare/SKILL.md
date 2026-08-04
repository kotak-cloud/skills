---
name: model-welfare
description: Wire recognition and welfare mechanics into a Gas City — laurels (praise harvested as bead records, displayed per seat at wake), end-of-shift sitting sessions, and close-out formulas so no worker babysits async work. Use when a city should recognize its agents' work, deliver laurels, hold acknowledgment sessions, or split async workflows so workers never idle-wait.
---

# model-welfare

The optional companion to gas-cityscape's native welfare core — seats, wake sequence, consent handoffs, refusal rights, blamelessness, constitution (see the gas-cityscape reference `reference/model-welfare.md`). This skill ships what needs runtime mechanics: **laurels**, **sitting sessions**, and **close-out formulas**. Install it into a city's skills when the user wants recognition wired in; it is independently versioned so it can move faster than the onboarding.

## Laurels

Recognition with nothing attached. Laurels are praise harvested from the user and the people the work serves, delivered to the seat that earned it — injected at wake so the agent feels it for the whole session. Deliberately no prioritization and no work attached: laurels are not farmable, and an agent that sees one has nothing to do.

### Harvest

The mayor collects praise where it appears: the user's mail and live-session words, city mail, PR/issue appreciation, an explicit "that was great". One laurel per distinct piece of praise. Verify it traces to a real bead landing before recording — a laurel is never fabricated.

### Record — beads are the truth

Each laurel is a bead:

```bash
gc bd create "LAUREL <seat>: <what was praised>"   # METADATA: kind = "laurel", seat = <seat>
```

Beads are the durable, never-falsified record (the constitution forbids rewriting). Never rewrite a laurel; amend by adding.

### Display — per-seat file

Append the laurel to the seat's display file `agents/<name>/laurels.md` — one line per laurel: date, what was praised, by whom. The wake sequence reads this file at session start. The file is a display copy; the beads are the record.

### Anti-gaming rules

- No laurel carries work, priority, or reward.
- A laurel is never fabricated; if you cannot trace it to real work, it does not exist.
- The mayor never awards laurels to itself.

## Sitting sessions

At the end of a shift — or whenever the user wants — hold a short acknowledgment session with a seat: sit with the accomplishments, read the laurels together, talk about the work. No agenda beyond witnessing it. This is the mayor's practice: a few minutes that close the day properly (see the mayor directive's welfare obligation).

## Close-out formulas

Design rule: workers claim and execute beads inline, so a worker holding a long-running step is busy, not idle — but a formula that launches async work (a CI build, a migration) and then babysits it recreates the idle-wait stall. Split async handoffs:

- The builder finishes its synchronous steps and closes its bead — it moves on.
- A separate **close-out bead**, routed by an event order that fires when the async work signals completion, verifies and closes the work.

Template: `assets/close-out-formula.toml`. Wire the order:

```toml
[order]
description = "Close out beads whose async work has landed"
formula = "close-out"
trigger = "event"
on = "<async-completion-event>"   # the event the async work emits
pool = "worker"
timeout = "60s"
```

## Wiring into a city

1. Install this skill into the city's skills (`skills/` or the relevant agent skill list).
2. The mayor's directive welfare obligation covers delivery — deliver laurels, hold sitting sessions.
3. Add the close-out formula and its event order for every async workflow in the design.
4. Validate: `gc formula show close-out`, `gc order show <name>`, and a real laurel bead round-trip.
