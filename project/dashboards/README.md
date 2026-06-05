# Dashboards

> Sintrix maintains this folder. One file per dashboard/view. Record the chosen card approach
> (native Lovelace vs specific HACS cards) here, since there is **no fixed stack** — Sintrix
> recommends per project and the integrator confirms in chat.

## How to add a dashboard spec

Copy the template below into a new file, e.g. `home.md`, `lighting-view.md`.

```markdown
# Dashboard — <name>

## Intent
Who uses it, on what device, what it must show/control.

## Card approach (decided)
- Native Lovelace / HACS card(s): <which, and why>
- HACS resources required: <list, if any — install per guardrails>

## Layout
Views, sections, cards. Reference entities from inventory/domains.

## As-built
ha-mcp dashboard id(s) + resource ids actually created/updated.

## Open items
```
