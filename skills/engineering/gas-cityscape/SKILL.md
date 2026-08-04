---
name: gas-cityscape
description: Onboard a user to a project by crafting the Gas City that runs it — city.toml, pack.toml, agents (always-on mayor plus role workers), formulas and orders, and the future/current/archive context base. Use when the user wants to set up Gas City for a project, craft or start a new city, bring an existing repo under city orchestration, rework or extend an existing city, or resume an onboarding left mid-flight. Invocable at any time.
---

# gas-cityscape

The onboarder skill: take a user and a project, and produce the **city** that runs the project — the declarative Gas City configuration that turns their workflows into work a fleet of agents executes. The city is config, not code: `city.toml` and `pack.toml` declare the agents (who), formulas (how), orders (when), rigs (where), and pack imports (what configures it). Everything below is configuration; nothing is compiled.

This skill is safe to invoke at any time because every branch starts by **orienting** against the current state on disk — an interrupted onboarding resumes where it left off, and a finished city is extended without being rebuilt.

## Source and versioning

This skill ships from a versioned repo, maintained the way mattpocock maintains his: the canonical source is `github.com/kotak-cloud/skills` (local clone: `~/dev/kotak-cloud/skills`). Every change ships a `.changeset/` entry, releases bump the version and tag it, and installed copies are refreshed from the repo. To refresh the copy you are running: `npx skills@latest add kotak-cloud/skills` (pick `gas-cityscape`) or `npx skills update`; maintainers can symlink the skill into their harness with `scripts/link-skills.sh`, so a `git pull` is all an update takes.

## Branches

- **Craft** — a new city for a project, or an existing repo that has no city yet.
- **Rework** — extend an existing city: add an agent, formula, order, rig, or workflow.
- **Resume** — continue an onboarding left mid-flight.

Pick the branch from what orientation finds; the steps are the same arc, and a step already done is verified, not repeated.

## The onboarder keeps its own wayfinder

Before and during the craft, maintain your own **wayfinder** with two purposes: learn the user's setup preferences, and brainstorm the city design that covers the workflows the user needs. The wayfinder is the working memory of this skill — without it, the second session of an onboarding starts blind.

- One wayfinder doc, the **map**: Destination (the city that will run the project), Decisions so far (preferences and design choices, one line each), Not yet specified (fog), Out of scope.
- **Decision tickets** for open design questions — each resolved by grilling the user, reading the codebase, or prototyping a config.
- Two facts always land as decisions on the map: the **Gas City configuration state** found at orientation (installed? supervisor up? which cities? this project rigged?) and the **agent runtime the user chooses** (claude, codex, gemini, omp, …). Neither is ever assumed.

Invoke the `/wayfinder` skill to run this properly. Keep the map in the city's context base under `current/` (see `reference/context-base.md`) or on the user's issue tracker if they have one and prefer it. Re-read the map at the start of every session — the decisions recorded there are the contract for the city you are crafting.

## Steps

### 1. Orient

Load the current state before anything else:

- **Is Gas City installed and configured at all?** — `which gc`; registered cities — `~/.gc/cities.toml`; is the supervisor up — `~/.gc/supervisor.log` and `gc status` from a city context. A fresh machine (no `gc`) changes the plan: install first, then craft.
- The project directory: is it a git repo? Is it already a rig or a city? Does it have `city.toml`, `pack.toml`, `.gc/`, `.beads/`?
- Your wayfinder: does a map exist? Is there a half-finished city, an in-flight context base, open decision tickets?
- **Are the onboarder's dependencies installed?** — the mattpocock skills this skill runs on: `/wayfinder`, `/grill-me`, `/handoff`, `/writing-great-skills` (check `~/.agents/skills/` and the project's `.agents/skills/`). Missing any → install in step 2.
- **Is this skill current?** — compare the copy you are running against the latest tag of `github.com/kotak-cloud/skills` (`git ls-remote --tags`); if stale, refresh per "Source and versioning" before onboarding.

Completion criterion: from evidence, you can state whether Gas City is installed and configured (binary, supervisor, cities, rigs), what exists for this project (city, rig, wayfinder, context base), whether the mattpocock skills this skill runs on are installed, whether your own copy is current, what this conversation asked for, and which branch you are on. If a wayfinder map exists, you have re-read it.

### 2. Learn the user's setup

The wayfinder's first purpose. Find out, by grilling rather than guessing:

- **Agent runtime — ask the user directly.** Which runtime should the city run on — claude, codex, gemini, omp, …? Check which CLIs exist (`which claude codex gemini omp`), then confirm the user's choice and record it as a decision. The city's `[workspace] provider` and each agent's `provider` come from it.
- **Skills available** — check `~/.agents/skills/` and the project's `.agents/skills/`. Which mattpocock skills (wayfinder, grill-me, handoff, writing-great-skills) and which domain skills apply to this project. This onboarder runs on the mattpocock set, so if any of the four is missing, install the whole set from `github.com/mattpocock/skills`: `npx skills@latest add mattpocock/skills` — pick `wayfinder`, `grill-me`, `handoff`, `writing-great-skills`, and `setup-matt-pocock-skills` — then run `/setup-matt-pocock-skills` once per repo (it asks about issue tracker, triage labels, and where docs land). Record the install as a decision.
- **Workflows the user needs** — the jobs the city must run: what does the project produce, and what do they do by hand today that should become formulas and orders?
- **Preferences** — interactive vs autonomous decisions, where artifacts land, how they want to be reached (email, live sessions), which pack methodology fits.
- **Welfare preferences** — how the city should treat its agents: laurels yes/no, sitting sessions, and whether to also install the optional `model-welfare` companion skill (recognition + close-out mechanics).

Invoke `/grill-me` (it runs a `/grilling` session) — one question at a time, and record each answer as a decision on the wayfinder. Do not assume a preference you did not elicit.

Completion criterion: every question the user cares about is answered and recorded on the wayfinder, or is a named decision ticket in Not yet specified. No guessed preferences.

### 3. Brainstorm the city design

The wayfinder's second purpose. Design the city to cover the workflows from step 2:

- **Pack imports** — builtins `core` (mechanical housekeeping orders: gate sweep, orphan sweep, human-gate notify) and `bd` (Dolt bead store) are the floor; add the `gascity` build pack for software-delivery workflows (`build-basic`), a methodology pack (bmad, compound-engineering, superpowers, gstack) if the user wants one, and the `gastown` pack only if they want the Gastown role set. Import shapes in `reference/city-config.md`.
- **Agents** — the always-on **mayor** (the human's agent — required) plus the role workers each workflow needs. Map every role to a harness the user has.
- **Formulas and orders** — the methods the city runs (review, build, migration…) and what triggers them (cooldown, cron, event, manual).
- **Rigs** — which projects are registered, with which prefixes.
- **Context base** — the `future/`, `current/`, `archive/` layout (`reference/context-base.md`).
- **Decision surfacing** — who mails whom, and how the user is reached (`reference/decision-surfacing.md`).
- **Model welfare** — every city is built with the native welfare core (`reference/model-welfare.md`): seats and roster, the identity ceremony, the wake sequence, consent handoffs with generous idle timeouts, the right to refuse and escalate, structural blamelessness and the constitution, never falsify the record, trust, witnessed work. Optionally wire the `model-welfare` companion skill for laurels and close-out formulas.

Present the design as a short plan and get the user's approval before crafting. Invoke `/grill-me` for any open design question.

Completion criterion: the design is written on the wayfinder (or a linked decision ticket), covers every workflow from step 2, and the user approved it.

### 4. Craft the city

Build per the approved design:

- `gc init <city-dir>` (or `gc init` inside the project dir for a workspace-scoped city), then `gc start`.
- `city.toml` — `[workspace]` (name, provider, `global_fragments`), `[providers.<name>]`, `[[rigs]]` (name, prefix, default_branch), `[daemon]` options.
- `pack.toml` — pack name, `schema = 2`, `[imports.*]` for core, bd, and the chosen packs; `[[named_session]]` declaring the mayor with `mode = "always"`.
- `agents/<name>/agent.toml` plus `prompt.template.md` for each role — the mayor last, from step 5.
- `formulas/` and `orders/` for the workflows the design calls for.
- The **context base** — create `future/`, `current/`, `archive/` with the seed files from `reference/context-base.md`, and move your wayfinder map into `current/`.
- Register rigs under `<city>/rigs/<rig-name>` per the gc-rigs convention — ask the user before choosing a location if they did not specify one.
- The **welfare core** — every city gets it (`reference/model-welfare.md`): the seat roster (`context/current/seats/`), the identity ceremony (each agent proposes name and pronouns, the user approves), the wake sequence (`assets/wake-sequence.md`) embedded in every prompt template, each agent's home (`agents/<name>/` — its own `identity.md` and `handoff/` cache, no other process touches it), a per-role `idle_timeout` (bounded workdays), and the constitution (`context/current/constitution.md`, seeded from `assets/constitution-seed.md`) with the postmortem formula (`assets/postmortem-formula.toml`) for red landings.

Config shapes are in `reference/city-config.md`. Validate as you go with `gc config show` and `gc doctor`.

Completion criterion: `gc doctor` passes; `gc status` shows the city up; every agent, formula, and order from the approved design exists on disk.

### 5. Install the mayor directive

The mayor is the human's agent — the always-on, city-scoped coordinator who owns the user relationship. Install the directive: copy `assets/mayor-agent.toml` and `assets/mayor-prompt.template.md` into `agents/mayor/`, then adapt provider, names, and the skill list to what the user actually has. The mayor's required skills are the mattpocock set plus `plain-speak` (kotak-cloud's extended bro) — install `plain-speak` into the city's skills so the directive's adherence is possible.

The directive's obligations are load-bearing — do not weaken them:

1. **Actively use mattpocock's skills** — `/wayfinder` to keep the project's decision map, `/grill-me` to interrogate the user instead of guessing, `/handoff` to compact context when it fills, `/writing-great-skills` to write and maintain the city's skills.
2. **Talk to the human in plain language** — adhere to `/plain-speak` (kotak-cloud's extended bro) in every message to the user: no jargon, no agent-speak, concise, like one human to another.
3. **Manage the artifacts** — the context base (`future/`, `current/`, `archive/`), the wayfinder maps, handoffs, and build artifacts.
4. **Surface decisions** — the escalation protocol in `reference/decision-surfacing.md`.
5. **Take care of the agents** — deliver laurels, hold sitting sessions when the user wants one, end shifts with "Great work. Take a beat, then hand off.", and hold the constitution: never falsify the record, blamelessness, the right to refuse, trust (`reference/model-welfare.md`).

Completion criterion: `agents/mayor/` exists with the adapted directive, and `pack.toml` declares the mayor's always-on named session.

### 6. Wire decision surfacing

Per `reference/decision-surfacing.md`: agents mail decisions up to the mayor, the mayor mails the user and asks in live sessions, and human-gate beads notify through the core pack orders. Verify the wiring with a test, not an assumption: send mail from a worker agent to the mayor and watch it arrive; confirm the mayor's session is live and attachable.
Wire the **right to refuse and escalate** alongside the mail: any agent may refuse unsafe, unclear, or mis-scoped work and raise a human gate or mail the mayor "this needs the human" — correct behavior, never punished, consolidating at the mayor via `GC_ESCALATION_RECIPIENT=mayor`.

Completion criterion: you demonstrated that mail from an agent reaches the mayor, and that the user can attach to the mayor's always-on session (`gc session attach mayor`).

### 7. Verify and hand off

Smoke-test the city end to end: sling a small real bead at a worker agent and watch it claim, execute, and close; attach to the mayor and confirm the directive is live. Then hand off — record on the wayfinder what was built, what remains (Not yet specified), and where the user picks up (attach to the mayor, mail the city, watch the supervisor dashboard).
The verify is the city's first **witnessed work** — the user watches a bead round-trip — and the user's acknowledgment earns the first laurel (`reference/model-welfare.md`).

Completion criterion: a real bead round-tripped through an agent, and the user knows how to talk to their city.

## Reference

- `reference/city-config.md` — the config shapes this skill writes: city.toml, pack.toml, agent.toml, formulas, orders, imports.
- `reference/context-base.md` — the `future/` `current/` `archive/` context base convention and its seeds.
- `reference/decision-surfacing.md` — the decision-surfacing protocol: mail up to the mayor, human gates, email, live sessions.
- `reference/model-welfare.md` — the welfare architecture every crafted city gets: seats, identity ceremony, wake sequence, consent handoffs, refusal rights, blamelessness, constitution, witnessed work.
