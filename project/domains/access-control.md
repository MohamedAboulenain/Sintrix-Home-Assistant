# Domain — Access Control

> Spec + as-built, maintained by Sintrix. Read before programming; update after.
> ⚠️ SAFETY-CRITICAL: locks, alarms, gates, garage/doors. Follow [02-guardrails.md](../02-guardrails.md):
> STOP and ask the integrator before changing behaviour here, and back up first.

## Intent
What the integrator wants (lock/unlock automation, alarm arm/disarm modes, access schedules, notifications).
- _(unset)_

## Conventions
House-specific rules (who/when, fail-safe defaults, never auto-unlock conditions, naming).
- _(unset; inherit from [01-conventions.md](../01-conventions.md))_

## Entities involved
Key `lock.*`, `alarm_control_panel.*`, `cover.*` (gates/garage), related sensors.
Query ha-mcp live for the full set.
- _(unset)_

## As-built
Programmed automations/scripts/scenes/dashboard cards, with ha-mcp object ids.
- _(none yet)_

## Open items
- _(none yet)_
