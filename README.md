# Sintrix

**A GitHub template for system integrators delivering smart-home projects on Home Assistant.**

Sintrix turns Claude Code into a smart-home programming agent that builds and maintains a single
house's Home Assistant — **dashboards, automations, scripts, scenes, helpers and integrations** —
through the [ha-mcp](https://github.com/homeassistant-ai/ha-mcp) server, while keeping a durable,
per-project memory in markdown that survives across sessions.

You — the system integrator — talk to Sintrix in chat. **You never edit markdown** — Sintrix
writes and maintains the project brain (`project/`) for you, recording who you are, every
convention, decision, and as-built detail.

---

## Quick start (per house)

1. **Use this template** → "Use this template" on GitHub → create a private repo for the house
   (e.g. `villa-rossi`). Clone it and open in your IDE with Claude Code (paid plan).

2. **Connect to the house's Home Assistant.** `.mcp.json` defaults to a **local stdio** ha-mcp
   server (`uvx ha-mcp`) that connects over the network via `HOMEASSISTANT_URL` +
   `HOMEASSISTANT_TOKEN` — this works for both **remote** and **on-site** houses; just point the URL
   at the right HA. Copy `.env.example` → `.env`, set a dedicated least-privilege token, and make
   sure the vars are in your environment when you launch Claude Code (the file explains how).
   Requires [`uv`/`uvx`](https://docs.astral.sh/uv/) installed. Prefer the **ha-mcp add-on**
   (remote HTTP) instead? Swap the server block per the comments in `.mcp.json` and use the
   [ha-mcp setup wizard](https://homeassistant-ai.github.io/ha-mcp/setup/).

3. **HA best-practices skill — already built in.** The `home-assistant-best-practices` skill
   ships inside this template at `.claude/skills/` and loads automatically — there is nothing to
   install, and it costs almost no context (only its trigger description is always loaded; the
   rest loads on demand). To refresh it from upstream, re-copy `skills/home-assistant-best-practices/`
   from [homeassistant-ai/skills](https://github.com/homeassistant-ai/skills) (MIT).

4. **Start the project:** run `/onboard`. Sintrix connects, interviews you, discovers the house,
   and fills in `project/`. From there, drive it with `/program <domain>`.

5. **Verify:** `/mcp` shows server `ha` connected; `ha_get_overview` returns the house.

---

## How it works (the loop)

```
clone ─▶ /onboard ─▶ Sintrix interviews you + discovers the house ─▶ writes project/
   you ask (chat) ─▶ Sintrix reads the spec ─▶ programs HA via ha-mcp ─▶ writes back
                     as-built + decision ◀─ you give feedback (chat) ─▶ loop repeats
```

- **You only talk.** Sintrix translates every preference/decision into the right `project/` file.
- **Read before / write after.** Sintrix reads the relevant spec before acting and records the
  as-built result + a decision after.
- **Memory is the repo.** `project/` is both the spec ("how to act") and the memory ("what exists
  and why"). It's reloaded every session, so context is everlasting per project.

See [docs/workflow.md](docs/workflow.md) for the full picture.

---

## Commands

| Command | What it does |
|---------|--------------|
| `/onboard` | Start a new house: connect, interview, discover, populate `project/`. |
| `/inventory` | Refresh the curated inventory summary from the live house. |
| `/program <domain\|feature>` | Program it via ha-mcp, then write as-built + a decision. |
| `/remember` | Capture a convention/decision you just stated into the right file. |
| `/handoff` | Produce a project status summary (and handover checklist). |

---

## Capability & safety

- **Full builder.** ha-mcp's advanced tools (YAML editing, filesystem, HACS / custom-component
  install) are enabled, so Sintrix can install integrations and custom dashboard cards. These
  powers are **governed by [`project/02-guardrails.md`](project/02-guardrails.md)**.
- **Backup-first** on bulk/destructive changes; **write actions prompt** for your approval
  (`.claude/settings.json`); **read actions** run freely.
- **Least-privilege access.** Use a dedicated token per house and **revoke it at handover**
  (inspired by [sfox38/atm](https://github.com/sfox38/atm)).
- **No auto-commit.** Sintrix edits files; you own git.

---

## Repository layout

```
CLAUDE.md            Sintrix's operating manual (auto-loaded)
.mcp.json            ha-mcp wired in (advanced flags on)
.env.example         connection secrets template (copy to .env)
.claude/
  settings.json      read-allow / write-prompt permission gate
  commands/          the slash commands above
  skills/            built-in home-assistant-best-practices skill (mandatory, auto-loaded)
project/             THE PROJECT BRAIN (spec + everlasting memory)
  00-overview.md     house, scope, status            (always loaded)
  01-conventions.md  integrator profile + conventions (always loaded)
  02-guardrails.md   rules grounding powerful tools  (always loaded)
  inventory/         curated house summary
  domains/           one file per domain (lighting, hvac, cctv, …)
  dashboards/ automations/ scripts/ decisions/
docs/workflow.md     the loop, explained
```
