# CONTEXT.md

Shared language for this repo.

- **Skill** — a directory of instructions (`SKILL.md` plus co-located `reference/` and `assets/`) an agent harness exposes to a model. Invocation is model-invoked (anyone can reach it) or user-invoked (only the human typing its name); see `.agents/invocation.md`.
- **Gas City** — the runtime this repo's one skill configures: `gc`, the supervisor daemon, and a fleet of agents that execute work as **beads**.
- **City** — one project's declarative Gas City configuration: `city.toml` (workspace, providers, rigs, daemon), `pack.toml` (imports, named sessions), `agents/` (roles), `formulas/` (how), `orders/` (when), `rigs/` (where).
- **Rig** — a registered project a city runs work in, with a prefix and a default branch.
- **Bead** — a unit of work; agents claim, execute, and close beads via `gc hook --claim --drain-ack --json`; the bead store persists them durably.
- **Formula** — a method the city runs (review, build, migration…). **Order** — a trigger that fires a formula (cooldown, cron, event, manual).
- **Pack** — a reusable bundle of agents/formulas/orders/rigs imported by `pack.toml` (builtins: `core`, `bd`; community: `gastown`, the `gascity` build pack, methodology packs like bmad).
- **Mayor** — the always-on, city-scoped agent that is the human's agent: coordinates the fleet, manages the context base, and surfaces decisions.
- **Context base** — the city's living memory at `<city>/context/` with `future/`, `current/`, `archive/`; plans move future → current → archive.
- **Wayfinder** — the mattpocock planning skill and the map it keeps: Destination, Decisions so far, Not yet specified (fog), Out of scope.
- **Changeset** — a markdown file in `.changeset/` describing one change; the Release workflow turns changesets into version bumps and `CHANGELOG.md` entries.
