# Guardrails — grounding the powerful tools

> Sintrix has **full builder** powers (YAML editing, filesystem access, HACS / custom-component
> install) enabled in `.mcp.json`. This file governs how those powers may be used on a **live
> client house**. Sintrix MUST follow these rules. The integrator can change them in chat; Sintrix
> records the change here.

## Backup-first rule

Trigger a Home Assistant backup via ha-mcp **before** any of these:

- Deleting or bulk-replacing automations, scripts, scenes, or dashboards.
- Editing raw YAML configuration (`ENABLE_YAML_CONFIG_EDITING`).
- Installing/removing an integration or HACS custom component.
- Any filesystem write outside the normal dashboard/automation/script config.

For a single, easily-reversible change (e.g. one new automation), a backup is not required —
but the change still goes through the normal write-approval prompt.

## When to STOP and ask the integrator

- Installing a **new integration** or **HACS repository** the project hasn't approved.
- Anything that affects **safety/security devices**: locks, alarms, garage doors, gates
  (access-control domain).
- Deleting anything you did not create, or that isn't recorded in `project/` as-built.
- Editing `configuration.yaml` / core HA system files, or touching the recovery/backup config.
- Any change you can't cleanly reverse.

## Never touch

- Secrets, tokens, `secrets.yaml`, credentials, or the HA user/auth configuration.
- The ha-mcp add-on / integration's own configuration.
- Network, supervisor, or OS-level settings.

## Filesystem / YAML scope

- Stay within dashboards, automations, scripts, scenes, helpers, themes, and `www/` assets
  needed for the project.
- Prefer ha-mcp's structured config tools (`ha_config_set_*`) over raw YAML when both work —
  see the best-practices skill.

## Record of guardrail changes

_(Sintrix appends here when the integrator adjusts a rule, with the date and reason.)_

- _(none yet)_
