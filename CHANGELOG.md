# kotak-cloud-skills

## 1.3.4

### Patch Changes

- [`f6a5594`](https://github.com/kotak-cloud/skills/commit/f6a5594b3ff38b66c6bbf79a072547f29a7d046e) - gas-cityscape: propagate agent-behavioral directives as single-source-of-truth fragments. Add ready-to-copy fragment templates (`templates/fragments/model-welfare.fragment.md`, `templates/fragments/beads-practices.fragment.md`) that each city copies into `template-fragments/<name>.template.md` and each agent's prompt invokes via explicit `{{ template "<name>" . }}`. Document the mechanism in `reference/city-config.md`, teach it in the Brainstorm + Craft steps, and mark `workspace.global_fragments` as deprecated (does not reliably inject into bespoke prompts). Also wire the `/design-thinking` skill into the Brainstorm step so city design is graphed before crafting.

## 1.3.3

### Patch Changes

- [`1351ea3`](https://github.com/kotak-cloud/skills/commit/1351ea32bbbf1479f9dd84a0ef7fd27e8edce46e) Thanks [@kotak-cloud](https://github.com/kotak-cloud)! - Add `reference/beads-ops.md` to gas-cityscape: operational rules for the bead store (hygiene loop, sizing, upgrade cadence, plan-then-import, restart-not-beads, file eagerly). Cross-link from Orient step (operational state), Brainstorm step (hygiene order), and model-welfare (consent handoff principle).

## 1.3.2

### Patch Changes

- [`5544e91`](https://github.com/kotak-cloud/skills/commit/5544e91993a96336942096c463bd3f5ae0bc7017) Thanks [@kotak-cloud](https://github.com/kotak-cloud)! - Scrub pronouns from the model-welfare materials: the identity ceremony is now names only (seat proposes its name, user approves) — removed from `gas-cityscape`'s reference/model-welfare.md, the identity/roster/wake-sequence seeds, and the SKILL.md craft step. Roster table drops the Pronouns column.

## 1.3.1

### Patch Changes

- [`81e1ba1`](https://github.com/kotak-cloud/skills/commit/81e1ba172aa90bba98d1121b201b0143f4a2c0dc) Thanks [@kotak-cloud](https://github.com/kotak-cloud)! - Fix install instructions: the README now lists all three skills (`gas-cityscape`, `model-welfare`, `plain-speak`) instead of telling readers to pick only `gas-cityscape`, and separates the interactive path (for humans) from the non-interactive flag-based path (`--skill <names> -y`, for AI agents — the CLI's picker is a menu that agents cannot drive). `gas-cityscape`'s own install/refresh instructions now use the non-interactive form too.

## 1.3.0

### Minor Changes

- [`43c80a7`](https://github.com/kotak-cloud/skills/commit/43c80a77df8c9a00c3e6757088ad5f4ab9a766a0) Thanks [@kotak-cloud](https://github.com/kotak-cloud)! - Add **`model-welfare`** — recognition and welfare mechanics for a Gas City: laurels (praise harvested, recorded as beads, displayed per seat at wake), end-of-shift sitting sessions, and close-out formulas so no worker babysits async work. Also make `gas-cityscape`'s welfare core native to every crafted city: seats roster, identity ceremony, wake sequence, consent handoffs, the right to refuse and escalate, structural blamelessness with a constitution and postmortem formula, and witnessed work (verify step reframed, first laurel).

## 1.2.0

### Minor Changes

- [`9f968f1`](https://github.com/kotak-cloud/skills/commit/9f968f188f6ddfac9539a4c4fe14b3a7a5ee34e4) Thanks [@kotak-cloud](https://github.com/kotak-cloud)! - Add **`plain-speak`** — the extended bro: a standing plain-language standard for the mayor's human-facing messages (no jargon, no agent-speak, concise, human-to-human), keeping the original bro's restate-on-request behavior. The mayor directive in `gas-cityscape` now obliges the mayor to adhere to `/plain-speak` when composing any message to the user, and the city craft installs `plain-speak` into the city's skills.

## 1.1.0

### Minor Changes

- [`6fa55c1`](https://github.com/kotak-cloud/skills/commit/6fa55c14b1df30173c957113961919dc34ff878c) Thanks [@kotak-cloud](https://github.com/kotak-cloud)! - Add the **`gas-cityscape`** onboarder skill: craft the Gas City that runs a project — `city.toml`, `pack.toml`, agents (always-on mayor plus role workers), formulas and orders, and the `future/current/archive` context base. The onboarder keeps its own wayfinder, checks whether Gas City is already installed and configured, asks the user which agent runtime the city should run on, and installs the mattpocock skills it runs on (wayfinder, grill-me, handoff, writing-great-skills) from `github.com/mattpocock/skills`.

## 1.0.0

### Minor Changes

- Initial release: the **`gas-cityscape`** onboarder skill — craft the Gas City that runs a project (`city.toml`, `pack.toml`, agents, formulas/orders, context base). The onboarder keeps its own wayfinder, checks whether Gas City is already installed and configured, asks the user which agent runtime the city should run on, and pulls mattpocock's skills from `github.com/mattpocock/skills` to set itself up.
