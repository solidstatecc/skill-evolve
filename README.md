# skill-evolve

Evolve any agent's skills. Not just one agent's.

Nous Research built a real thing: [hermes-agent-self-evolution](https://github.com/NousResearch/hermes-agent-self-evolution) — DSPy + GEPA evolutionary search that rewrites SKILL.md files and proves the new version is better. It targets Hermes Agent.

But SKILL.md is not a Hermes format. It's the [agentskills.io](https://agentskills.io) spec — Claude Code, Hermes, OpenClaw, Cursor, ~40 runtimes read the same file.

So the engine deserves a wider target. This is that.

## What it does

Point it at any skills directory. It evolves what it finds.

```bash
skill-evolve --skills-dir ~/.claude/skills --skill my-skill --iterations 10
```

- Works on `~/.claude/skills`, `~/.hermes/skills`, any repo `skills/` tree.
- Mutates, evaluates, selects — GEPA reads execution traces to learn *why* variants fail.
- Every candidate passes Solid State's constraint gates before it survives.
- Output is a PR. Never a direct write. You review, you merge.

No GPU. API calls only. ~$2–10 per run, on your keys.

## What's ours, what's theirs

The engine is Nous Research's, pinned as a dependency. Not forked, not vendored.

Ours is the part that makes it general:

- **The target adapter.** Any agentskills.io layout, one flag.
- **The SKILL.md driver.** An agent can run this on its own skills.
- **The gates.** Opinionated pass/fail criteria from [publish-audit](https://solidstate.cc/skills/publish-audit) and field-tested skill-quality heuristics. Evolution against weak evals produces reward-hacked skills. The gates are the product.

See [NOTICE](NOTICE). Star their repo too.

## Status

Pre-release. Scaffold + gate spec public; code lands the week of June 16, 2026.

Free. MIT.

## The loop

Audit tells you what's wrong. Evolution fixes it. Audit checks the fix.

```
publish-audit ──► skill-evolve ──► publish-audit ──► ship
```

One tool judges. One tool improves. Both free at [solidstate.cc](https://solidstate.cc).
