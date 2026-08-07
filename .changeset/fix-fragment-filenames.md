---
"kotak-cloud-skills": patch
---

gas-cityscape: align fragment and beads-sweep instructions with the gc 1.4 prompt renderer. The shipped fragment templates are renamed to `*.template.md` — gc loads only `*.template.md` (legacy `.md.tmpl`) from `template-fragments/`, so the previous `.fragment.md` names silently rendered nothing when copied per the skill's "copy, don't rewrite" step; SKILL.md and city-config.md now say to keep the shipped filename. The `city.health.bd-sweep` order example in beads-ops.md is replaced with the verified exec-script form (`scripts/bd-sweep.sh` running `bd doctor --fix` + `bd cleanup --max-age 30d` + `bd sync`): the formula is not in the gascity pack catalog, and exec orders reject a `pool` key.
