# kotak-cloud-skills

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
