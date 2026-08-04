# gas-cityscape

Model-invoked onboarder skill: craft the **city** that runs a project on Gas City — declarative configuration, not code.

[SKILL.md](../../skills/engineering/gas-cityscape/SKILL.md)

## What it does

- **Orients** against the machine and the project: is Gas City installed and configured (`which gc`, `~/.gc/cities.toml`, supervisor), is this project already a city or rig, are the mattpocock skills it runs on installed, is its own copy current.
- **Learns the setup by grilling**: which agent runtime (claude, codex, gemini, omp…), which workflows the city must run, how the user wants to be reached.
- **Crafts the city**: `city.toml`, `pack.toml`, agents (always-on mayor plus role workers), formulas and orders, rigs, and the `future/current/archive` context base.
- **Installs the mayor directive**: the mayor actively uses wayfinder, grill-me, handoff, and writing-great-skills, manages the artifacts, and surfaces decisions to the user.
- **Wires decision surfacing**: agents mail decisions up to the mayor; the mayor reaches the user (email via mcp-agent-mail when wired, otherwise `gc mail send human` plus live `gc session attach mayor` sessions).
- **Verifies and hands off**: a real bead round-trips through a worker agent, the mayor's session is attachable.

## Dependencies

- [mattpocock/skills](https://github.com/mattpocock/skills) — wayfinder, grill-me, handoff, writing-great-skills; installed with `npx skills@latest add mattpocock/skills`.
- Gas City itself (`gc`) — the runtime the skill configures.

## Versioned

Ships from this repo; every change goes through a `.changeset/`; releases are tagged. Refresh an installed copy with `npx skills update`.
