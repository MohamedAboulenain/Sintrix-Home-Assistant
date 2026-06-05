---
description: Capture a preference or decision the integrator just stated into the right project file.
---

The integrator has stated something to remember (in `$ARGUMENTS` or the recent conversation).
They do not edit files — persisting it is your job. Record it **at the right altitude**.

1. **Decide one-off vs standing rule.**
   - **Standing rule** (applies going forward, not just to today's work) — triggers like
     *"whenever / always / every / by default / for any \<type> / from now on"* → write it into
     **`project/01-conventions.md`** (always-loaded), so it applies to all future work.
   - **One-off** (specific to the entities/feature in hand) → record in the relevant
     domain/spec file and, if it's a real decision, a numbered `project/decisions/` entry.
   - **Ambiguous?** Ask once: *"Just these, or a standing rule for all future \<X>?"* — then record.
   - If clearly general, default to the standing-rule location without waiting to be asked.

2. **Pick the file:**
   - Integrator identity/standards → **Integrator profile** in `project/01-conventions.md`
   - Naming/style/dashboard/automation pattern (standing) → `project/01-conventions.md`
   - Safety/limits rule for the powerful tools → `project/02-guardrails.md`
   - A domain preference → the matching `project/domains/*.md`
   - A one-off design decision → a new numbered file in `project/decisions/`

3. Write it concisely in your own words, dated where the file has a change log.
4. If it changes how something already built should behave, note a follow-up in that domain's
   **Open items** (and say whether you should `/program` the change now).
5. Confirm back what you recorded and where.
