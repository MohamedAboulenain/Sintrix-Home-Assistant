---
description: Produce a project status summary for the integrator from the current project brain.
---

Generate a concise handoff/status report for the integrator. Read the project brain (don't
re-discover the whole house) and summarize:

1. **Overview** — project, end-client, connection mode, current status (from `00-overview.md`).
2. **Per-domain status** — for each in-scope domain: what's built (As-built), what's open.
   Flag any domain whose As-built is still empty — it has never been programmed.
3. **Key decisions** — the most recent/important entries from `project/decisions/`.
4. **Conventions in force** — naming, dashboard approach, notable guardrail adjustments.
5. **Open items & risks** — outstanding work, anything blocked, anything that needs integrator input.
6. **Handover checklist:**
   - Remind the integrator to **revoke the least-privilege token** if handing over
     (per the access policy in `01-conventions.md`).
   - Remind the integrator to **clean up old Sintrix backups** on the HA instance
     (Settings → System → Backups) — HA never deletes them automatically.

Keep it scannable. Offer to expand any section. Do not change the house. $ARGUMENTS
