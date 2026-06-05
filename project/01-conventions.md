# Conventions

> Sintrix maintains this file. The integrator does not edit it — Sintrix records here whatever the
> integrator states in chat. These are the rules Sintrix follows when programming this house. Thin
> universal seeds ship below; Sintrix fills in the integrator's house-specific style as it learns it.

## Integrator profile

> Who Sintrix is working with. Captured on the first `/onboard` of a clone. The same integrator
> runs many houses, so these house-agnostic standards should stay consistent across their projects.
> Factual identity only — not a persona to role-play.

- **Integrator (name / company):** _(unset — capture at /onboard)_
- **House-agnostic standards** (naming scheme, preferred dashboard approach, default behaviours
  this integrator applies to every project): _(unset)_
- **Notes / preferences:** _(unset)_

## Universal seeds (ship with the template)

- **Client-facing language:** English — all dashboard titles, friendly names, and labels.
- **Source of truth:** these markdown files describe intent + as-built; the live house is queried
  via ha-mcp for current detail. Keep both consistent.
- **Naming:** prefer clear, human-readable names; record the agreed scheme below once the integrator sets it.
- **Best practices:** follow the `home-assistant-best-practices` skill (native constructs over
  Jinja2, correct helper choice, proper automation modes, safe refactoring).

## Naming conventions

_(Learned from the integrator. e.g. entity_id pattern, friendly-name pattern, area naming.)_

- _(unset)_

## Dashboard approach

> No fixed card stack. Sintrix recommends native Lovelace vs specific HACS cards per project and
> records the decision per dashboard in [dashboards/](dashboards/).

- Preferred approach: _(unset — Sintrix to recommend, the integrator to confirm)_
- Approved custom cards (if any): _(unset)_

## Automation & script patterns

_(House-specific patterns the integrator prefers: trigger styles, modes, naming, notification channels.)_

- _(unset)_

## Access policy (ATM principles)

- Use a **dedicated, least-privilege** long-lived token for this house.
- **Revoke the token at handover.** Record handover status in [00-overview.md](00-overview.md).

## Change log of conventions

_(Append-only. Sintrix notes here when a convention is added or changed, with the date.)_

- _(none yet)_
