# kotak-cloud/skills

Agent skills for the kotak-cloud org, modeled on [mattpocock/skills](https://github.com/mattpocock/skills): small, composable skills that work with any model, versioned with changesets, installed with the `skills` CLI.

## Skills

- **gas-cityscape** (`skills/engineering/gas-cityscape/`) — onboard a user to a project by crafting the Gas City that runs it: `city.toml`, `pack.toml`, agents (always-on mayor plus role workers), formulas and orders, and the `future/current/archive` context base. The onboarder keeps its own wayfinder, checks whether Gas City is already installed and configured, asks which agent runtime you want, and pulls mattpocock's skills from `github.com/mattpocock/skills` to set itself up.
- **plain-speak** (`skills/productivity/plain-speak/`) — the extended bro: talk to the human in plain language — no jargon, no agent-speak, concise, like one human to another. The mayor adheres to it for every human-facing message.

## Installation

### 1. Get the skills

```bash
npx skills@latest add kotak-cloud/skills
```

Pick `gas-cityscape`. The installer writes it into your repo as ordinary files you own.

### 2. Run it

```
/gas-cityscape
```

The onboarder orients (Gas City installed? project already a city or rig? its dependencies installed?), grills you on the agent runtime and workflows, and crafts the city.

### Keeping it updated

```bash
npx skills update
```

or re-add with `npx skills@latest add kotak-cloud/skills`. Maintainers can symlink instead — see below.

## Versioned maintenance

This repo follows mattpocock's maintenance model exactly:

- **Every change ships a changeset** — add `.changeset/<topic>.md` describing the change (see `.changeset/README.md`).
- **Releases are automatic** — the `Release` workflow (`.github/workflows/release.yml`) opens a version PR on merge to `main`; merging it bumps the version, regenerates `CHANGELOG.md`, and tags the release. Never edit `CHANGELOG.md` by hand.
- **Installed copies refresh from the repo** — `npx skills update`, or `scripts/link-skills.sh` for maintainers, which symlinks every skill into `~/.claude/skills` and `~/.agents/skills` so a `git pull` is all an update takes.

## Why these skills exist

The failure mode this skill fixes: agents get dropped into a project and asked to "set up the automation" — so they improvise. `gas-cityscape` replaces improvisation with a repeatable onboarding: a wayfinder that records what was decided, an explicit check of the current state, a grilled agreement on the agent runtime and workflows, and a crafted city that verifiably runs (a real bead round-trips through an agent before handoff).

## License

MIT
