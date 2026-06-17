# prompt-focus-marketplace

A [Claude Code](https://claude.com/claude-code) plugin marketplace hosting the **prompt-focus** skill:
review and optimize LLM prompts so they stay focused, clear, contradiction-free, and keep every output
contract.

## What's inside

| Plugin | Skill | What it does |
| --- | --- | --- |
| `prompt-focus` | `/prompt-focus` | Reviews a prompt across seven dimensions (focus, de-dup, drop noise, disambiguate, fix contradictions, show don't tell, structure), fixes the six common drifts users introduce when editing prompts, and never cuts hard constraints. |

## Install

```
/plugin marketplace add bianzhonglin/prompt-focus-marketplace
/plugin install prompt-focus@prompt-focus-marketplace
```

Then invoke in any session:

```
/prompt-focus
```

and point it at the prompt you want optimized.

## Identity

Maintainer / author: **Absen-Colin** ([@bianzhonglin](https://github.com/bianzhonglin)).
Repository: `https://github.com/bianzhonglin/prompt-focus-marketplace`.

If you fork this marketplace, update the identity fields in
`.claude-plugin/marketplace.json`, `plugins/prompt-focus/.claude-plugin/plugin.json`, `LICENSE`,
and the install command below.

## Layout

```
.claude-plugin/marketplace.json          # marketplace manifest (lists plugins)
plugins/prompt-focus/
  .claude-plugin/plugin.json             # plugin manifest
  skills/prompt-focus/SKILL.md           # the skill itself
LICENSE
README.md
```

## License

MIT — see [LICENSE](LICENSE).
