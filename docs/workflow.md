# How Sintrix works

This explains the model behind Sintrix so the integrator knows what to expect — and so the
agent's behaviour is documented in one place. Sintrix is built for **system integrators**: the
person it works with is a professional integrator, and it talks to them peer-to-peer.

## The core idea

Sintrix is **not an app**. It's a structured Claude Code workspace that sits **on top of
[ha-mcp](https://github.com/homeassistant-ai/ha-mcp)**. ha-mcp gives the agent full control of a
house's Home Assistant (84–95+ tools for dashboards, automations, scripts, scenes, entities,
templates, history, backups, integrations). Sintrix adds the **operating layer**: an agent
persona (`CLAUDE.md`), a per-project memory (`project/`), and a repeatable loop (slash commands).

## The self-learning loop

```
clone template ─▶ /onboard ─▶ Sintrix learns who the integrator is + discovers the house
                              └─▶ Sintrix writes project/ profile, conventions, curated inventory
                                       │
   integrator asks (chat) ─▶ Sintrix READS the relevant project/ file (how to act)
                            ─▶ programs HA via ha-mcp
                            ─▶ Sintrix WRITES back: as-built + decision + any new convention
                                       │
   integrator gives feedback (chat) ◀─┘   (loop repeats; memory compounds)
```

**The integrator only talks. Sintrix owns every markdown change.** Disciplines enforced by `CLAUDE.md`:

1. **Read before acting** — the relevant `project/` spec + the always-loaded conventions/guardrails.
2. **Write after acting** — as-built ids and a `decisions/` entry.
3. **Capture at the right altitude** — a standing rule ("whenever/always/every…") goes into the
   always-loaded `01-conventions.md`, not just a per-instance decision, so it applies to all
   future work. When scope is ambiguous, Sintrix asks once.

That's what makes the repo self-learning and the memory everlasting: it all lives in versioned
markdown that's reloaded every session.

## Who the integrator is

Sintrix always knows it's serving a **system integrator** (whoever it is). On the first
`/onboard` of a clone it captures an **Integrator profile** at the top of `01-conventions.md` —
name/company plus the integrator's house-agnostic standards (naming, preferred dashboards,
default behaviours). Because one integrator runs many houses, those standards give their projects
consistency. This is factual identity, not a fictional persona.

## Why markdown (and what's where)

- `00-overview.md`, `01-conventions.md`, `02-guardrails.md` are **always loaded** (imported by
  `CLAUDE.md`) — Sintrix's ground truth each session.
- `domains/*.md` are per-domain spec + as-built. Read before programming a domain; updated after.
- `inventory/` is a **curated summary** — areas, device classes, a naming map, key ids. It is
  deliberately *not* a full entity dump; for current/full detail Sintrix queries ha-mcp live, so
  the memory stays compact and never goes stale.
- `dashboards/ automations/ scripts/` hold richer specs when something warrants its own file.
- `decisions/` is an ADR-style log — the durable record of *why*.

## Capability, grounded

Sintrix runs ha-mcp as a **full builder** (YAML editing, filesystem, HACS/custom-component
install enabled). That power is governed by `project/02-guardrails.md`, which Sintrix must
follow: backup-first on risky changes, stop-and-ask on integrations and safety-critical devices,
and a never-touch list. Write/remove tools also prompt for the integrator's approval as an
in-the-loop gate.

## Access & handover (ATM principles)

Sintrix stays on ha-mcp but borrows the access discipline from
[sfox38/atm](https://github.com/sfox38/atm): a **dedicated, least-privilege token per house**,
**revoked at handover**. (ATM itself is a native-MCP-compatible replacement and lacks ha-mcp's
rich dashboard/automation config tools, so it is intentionally not used as the server — only its
principles are adopted.) `/handoff` reminds the integrator to revoke the token.

## What Sintrix does NOT do

- It does **not** ask the integrator to edit files — that's the agent's job.
- It does **not** auto-commit to git — the integrator owns version control.
- It does **not** store secrets in tracked files — connection details live in `.env` (gitignored).
