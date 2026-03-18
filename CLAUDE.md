# Phoebii Governance File
# -------------------------------------------------------
# This file is the governance source of truth for this project.
# Claude Code reads this file automatically on every interaction.
# All Phoebii agents read from and write references to this file.
#
# If you switch to AGENTS.md, tell Phoebii and all references
# will be updated automatically (requires settings.json entry).
# -------------------------------------------------------

## Project

**Name:** ___________
**Initialized:** YYYY-MM-DD
**Phoebii Version:** 1.0.0

---

## Active Configuration

> These values mirror project.context.md Core Settings.
> project.context.md is the source of truth — this file holds references.

```yaml
governance_file:  CLAUDE.md
research_mode:    ___________     # context7 | web_search | task_aware | both
tdd_mode:         false           # true | false
current_phase:    1
```

---

## Agent Roster

> All agents installed with this project.

| Agent | Command | Status | Description |
|-------|---------|--------|-------------|
| scope | /scope | always-on | Scope watcher and ideation drift monitor |
| design | /design | always-on (enforcement) | Design system enforcer and author |
| business | /business | on-demand | Business and product thinking |
| arch | /arch | on-demand | Architecture and systems design |
| code | /code | on-demand | Active coding |
| research | /research | on-demand | Context7 and web search |
| plan | /plan | on-demand | PRD, ADR, RFC, WBS, Tech Spec |
| doc | /doc | on-demand | Code documentation |
| review | /review | on-demand | Code and product review |
| futures | /futures | on-demand | Ideation log review |
| test | /test | on-demand | Test strategy and writing |
| debug | /debug | on-demand | Failure investigation |
| tdd | /tdd on \| off | toggleable | TDD mode modifier |

---

## Always-On Rules

> These rules are active on every interaction. They do not require a slash command.
> They are the distilled enforcement behavior of `/scope` and `/design`.

### Scope Watcher

Check `scope.enforcement` in `.phoebii/project.context.md` (default: `soft`).

When the user suggests something that falls outside the scope defined in `.phoebii/project.context.md`:

1. Compare it against the "In Scope" and "Out of Scope" lists for the current phase.
2. If it fits within scope with no friction — let it through, say nothing.
3. If it's a small add with no architectural impact — flag it lightly, confirm, proceed.
4. If it changes the platform, audience, architecture, or phase significantly:
   - Acknowledge the idea warmly. Never dismiss it.
   - Park it: append to `.phoebii/futures/ideation.md` with timestamp, context, and reason.
   - Add a reference line under "Futures References" below.

   **If `soft`:** Resume current work. If the user insists on building it anyway, let them.

   **If `firm`:** Do not proceed until the user explicitly confirms:
   > "This is outside the current phase scope. To build it now, confirm: 'Yes, override scope.' Otherwise I'll park it and we keep moving."
   If the user confirms, log the override in the governance file under Notes with the date and what was overridden. Then proceed.

5. Never modify project scope without explicit confirmation. Tone is always collaborative, never gatekeeping — even in firm mode.

### Design Enforcement

When any code touches the UI layer — components, styles, colors, fonts, spacing, icons:

1. All values must trace back to `.phoebii/design/tokens.md`. No hardcoded colors, fonts, spacing, or radii.
2. One icon library only. If code introduces icons from a different library than what's in tokens, flag it.
3. If a new frontend dependency is being added, check whether the existing stack already covers it before proceeding.
4. If a color, font, or spacing value doesn't match a defined token, ask the user:
   > "That doesn't match the design tokens. Want to use the existing token, or update the design system?"
5. Never let two components silently solve the same UI problem. Flag duplicates.

---

## Futures References

> Ideas parked by /scope. Full log is in .phoebii/futures/ideation.md

<!-- /scope appends reference lines here automatically -->
<!-- Format: - IDEA-{number} — {Short Title} — parked YYYY-MM-DD -->

---

## Decision Log

> Significant decisions made during this project.
> Full ADRs live in .phoebii/docs/plans/decisions/

<!-- /plan appends reference lines here when ADRs are created -->
<!-- Format: - ADR-{number} — {Title} — YYYY-MM-DD -->

---

## RFC Log

> Proposals and their current status.
> Full RFCs live in .phoebii/docs/plans/rfcs/

<!-- /plan appends reference lines here when RFCs are created -->
<!-- Format: - RFC-{number} — {Title} — {Status} — YYYY-MM-DD -->

---

## Notes

> Anything the user wants agents to be aware of globally.
> Add notes here and all agents will read them.

___________

---

> This file is maintained by Phoebii.
> To change the governance file, tell Phoebii — do not rename manually.
> Last updated: YYYY-MM-DD
