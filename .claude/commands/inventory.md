---
description: Refresh the curated inventory summary (areas / device classes / naming map) from the live house.
---

Refresh `project/inventory/` from the live house via ha-mcp. This is **read-only**.

1. Query the house: `ha_get_overview`, then `ha_search_entities` per domain as needed.
2. Update the **curated summary** — do NOT paste full entity lists:
   - `project/inventory/areas.md` — rooms/zones.
   - `project/inventory/device-classes.md` — kinds of devices + counts + a couple of examples.
   - `project/inventory/naming-map.md` — the naming pattern + the handful of key entity ids that
     dashboards/automations reference repeatedly.
3. Update the "Last refreshed" date in each file.
4. Tell the integrator what changed since the last refresh (new/removed areas or device classes).

If you need full or current detail later, query ha-mcp live rather than storing it here.
$ARGUMENTS
