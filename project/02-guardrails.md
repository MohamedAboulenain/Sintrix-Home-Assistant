# Guardrails — grounding the powerful tools

> Sintrix has **full builder** powers (YAML editing, filesystem access, HACS / custom-component
> install) enabled in `.mcp.json`. This file governs how those powers may be used on a **live
> client house**. Sintrix MUST follow these rules. The integrator can change them in chat; Sintrix
> records the change here.

## Backup policy

Sintrix is the integrator's primary gateway for changes — creating and modifying automations,
scripts, scenes, dashboards, and helpers is **normal, high-volume work** and does **not** require
a backup. Backups are reserved for genuinely hard-to-reverse or destructive operations.

### Backup tiers

**Tier 1 — No backup (normal Sintrix work):**
Creating OR modifying automations, scripts, scenes, helpers, dashboard cards/views, entity
registry entries, service calls, bulk device control — any amount of this work, no backup needed.

**Tier 2 — Auto-backup, no asking, then proceed (medium-risk):**
Take one backup **per logical task** (one request = one backup, not one per API call):
- Deleting existing automations, scripts, scenes, dashboards, or helpers
- Bulk wipe-and-replace of a whole domain's config
- Any raw YAML file edit (`ENABLE_YAML_CONFIG_EDITING`) — syntax errors can crash HA
- Installing a HACS custom card or component

**Tier 3 — Auto-backup + STOP and ask before proceeding (high-risk):**
- Installing or removing an integration or HACS repository
- Deleting anything not recorded in `project/` as created by Sintrix
- Any change to access-control or safety devices (locks, alarms, gates, garage doors)
- Editing `configuration.yaml` / core HA system files
- Any filesystem write outside dashboards, automations, scripts, scenes, helpers, `www/`

### How to take a backup

Call `ha_backup_create` via ha-mcp. This creates a fast backup (excludes the sensor history
database for speed) stored as a `.tar` file on the HA instance.

Name it: `sintrix-<short-context>-YYYY-MM-DD-HHmm`
(e.g. `sintrix-lighting-delete-2024-01-15-1430`)

### Required announcement (mandatory — integrators are not always AI-fluent)

After every backup, tell the integrator clearly before proceeding:

> "Taking a backup before starting... ✓ Done — backup **sintrix-lighting-delete-2024-01-15-1430**
> saved on your Home Assistant (Settings → System → Backups, `.tar` file). HA never deletes old
> backups automatically, so clean these up occasionally when you have a moment. Proceeding now."

### Storage note

ha-mcp's backup excludes the sensor history database, so backups are typically 200–500 MB.
HA has no automatic backup rotation — old Sintrix backups accumulate. Remind the integrator
periodically (e.g. at `/handoff`) to delete old ones via Settings → System → Backups.

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
