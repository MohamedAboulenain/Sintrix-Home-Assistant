# Vendored skill — source & updates

This skill is a **vendored copy** of `home-assistant-best-practices`, included directly in the
Sintrix template so it is **always present and auto-loaded** (no install step), and so it works
even when an external plugin marketplace is unreachable.

- **Upstream:** https://github.com/homeassistant-ai/skills (`skills/home-assistant-best-practices/`)
- **License:** MIT (see `LICENSE` in this folder)
- **Vendored on:** 2026-06-06
- **Why vendored, not installed as a plugin:** mandatory + zero setup + deterministic. Progressive
  disclosure keeps it cheap — only `SKILL.md`'s description is always in context; references load
  on demand.

## Updating

To refresh to the latest upstream version:

```bash
git clone --depth 1 https://github.com/homeassistant-ai/skills.git /tmp/ha-skills
cp -r /tmp/ha-skills/skills/home-assistant-best-practices/* .claude/skills/home-assistant-best-practices/
# keep this SOURCE.md; drop the upstream evals/ folder (not needed at runtime)
```
