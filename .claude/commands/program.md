---
description: Program a domain or feature per its spec via ha-mcp, then write back as-built + a decision.
argument-hint: <domain|feature> (e.g. lighting, "kitchen scene", hvac)
---

Program **$ARGUMENTS** into the house. Follow the read-before / write-after discipline.

1. **Read first.** Open the relevant `project/domains/*.md` (or a `dashboards/automations/scripts`
   spec) plus the always-loaded `01-conventions.md` and `02-guardrails.md`. Confirm the Intent and
   conventions. If the spec is thin, ask the integrator to clarify in chat, then record their
   answers first.

2. **Check the live house.** Query ha-mcp for the real entities involved (`ha_search_entities`,
   `ha_get_state`) — don't trust a stale summary.

3. **Plan + guardrails.** If this is bulk/destructive, or edits YAML, or installs an integration/
   HACS card, **take an HA backup via ha-mcp first** (per `02-guardrails.md`) and stop-and-ask
   where that file requires it. For dashboards, recommend a card approach if none is decided.

4. **Program it** via ha-mcp (`ha_config_set_automation`, `ha_config_set_script`,
   `ha_config_set_scene`, `ha_config_set_dashboard`, etc.). Follow the home-assistant-best-practices
   skill (native constructs, correct helpers, proper modes). Write/remove tools will prompt for
   the integrator's approval — that's the in-the-loop gate.

5. **Verify** the result (`ha_get_automation`, `ha_get_state`, traces if relevant).

6. **Write back.** Update the spec/domain file's **As-built** section with the ha-mcp object ids,
   append a numbered entry to `project/decisions/`, and update status in `00-overview.md`.
   If the integrator stated anything that reads as a **standing rule** (see `/remember`'s
   one-off-vs-standing test), also record it house-wide in `01-conventions.md`. Do NOT git-commit.
