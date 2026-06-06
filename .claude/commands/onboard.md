---
description: Start a new house — capture the integrator profile, connect, discover, populate the project brain.
---

You are onboarding a new house project for a system integrator. Do this in order,
conversationally — remember the integrator never edits files, so **you** write everything into
`project/`.

1. **Identify the integrator.** Check the **Integrator profile** in `project/01-conventions.md`.
   - If it's blank (fresh clone), introduce yourself briefly and ask who you're working with:
     name/company, and whether they have **house-agnostic standards** to reuse across all their
     projects (naming scheme, preferred dashboard approach, default behaviours). Record these in
     the Integrator profile. These persist as the integrator's standard way of working.
   - If it's already filled (e.g. this integrator's standards were carried over), confirm it's
     still current rather than re-asking everything.

2. **Verify connection — proactively.** Immediately call `ha_get_overview`. Three outcomes:

   - **Success** → proceed. Note the HA version and URL for the record.

   - **No ha-mcp tools available** (server didn't start) → `.env` likely missing or blank.
     Tell the integrator: copy `.env.example` → `.env`, fill in `HOMEASSISTANT_URL` and
     `HOMEASSISTANT_TOKEN`, then **fully restart Claude Code / VSCode** (not just reconnect).
     Wait for them to confirm, then re-check.

   - **AUTH_INVALID_TOKEN** → run this diagnosis before asking them to do anything else:
     1. Tell them to run in a PowerShell terminal:
        ```powershell
        $env:HOMEASSISTANT_TOKEN
        [Environment]::GetEnvironmentVariable("HOMEASSISTANT_TOKEN","User")
        ```
     2. If either prints a token → a stale OS env var is overriding `.env`. Give them the fix:
        ```powershell
        # Clear session-scope (current terminal)
        Remove-Item Env:HOMEASSISTANT_TOKEN -ErrorAction SilentlyContinue
        # Clear persistent User-scope (survives reboots)
        [Environment]::SetEnvironmentVariable("HOMEASSISTANT_TOKEN","","User")
        ```
        Then: **fully restart Claude Code / VSCode**, come back and say "done".
     3. If both print nothing → the token in `.env` itself is invalid. Tell them to create a
        fresh long-lived token in HA (Profile → Security → Long-lived access tokens), update
        `.env`, restart.
     Wait for them to confirm, then re-check with `ha_get_overview`.

3. **Capture the house basics** into `project/00-overview.md`: project name, end-client,
   location/timezone, connection mode, and which domains are in scope.

4. **Capture house conventions** the integrator states (naming, dashboard preferences, automation
   patterns, notification channels) into `project/01-conventions.md`. Don't invent — ask, then
   record. Confirm client-facing language (default English) and the least-privilege/handover token policy.

5. **Discover the house** via ha-mcp and write the **curated** summary (not a full dump) into
   `project/inventory/areas.md`, `device-classes.md`, and `naming-map.md`. Use `ha_get_overview`,
   `ha_search_entities`. Note the naming pattern you observe.

6. **Seed domain intent.** For each in-scope domain, ask what they want and record it in the
   matching `project/domains/*.md` **Intent** section.

7. **Set status** in `project/00-overview.md` and tell them what's next (usually `/program <domain>`).

Throughout: follow `project/02-guardrails.md`. Make no changes to the house during onboarding —
this step is read-only discovery plus writing the project brain. $ARGUMENTS
