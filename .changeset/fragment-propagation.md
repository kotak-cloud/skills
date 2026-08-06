---
"kotak-cloud-skills": patch
---

gas-cityscape: propagate agent-behavioral directives as single-source-of-truth fragments. Add ready-to-copy fragment templates (`templates/fragments/model-welfare.fragment.md`, `templates/fragments/beads-practices.fragment.md`) that each city copies into `template-fragments/<name>.template.md` and each agent's prompt invokes via explicit `{{ template "<name>" . }}`. Document the mechanism in `reference/city-config.md`, teach it in the Brainstorm + Craft steps, and mark `workspace.global_fragments` as deprecated (does not reliably inject into bespoke prompts). Also wire the `/design-thinking` skill into the Brainstorm step so city design is graphed before crafting.
