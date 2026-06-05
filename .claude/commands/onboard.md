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

2. **Verify connection.** Confirm ha-mcp is reachable (`/mcp` should show server `ha`). If not,
   point them to `README.md` setup (fill `.env` from `.env.example`, pick remote vs add-on mode).
   Once connected, run `ha_get_overview` to confirm access.

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
