# prompt-focus

A [Claude Code](https://claude.com/claude-code) plugin marketplace hosting the **prompt-focus** skill:
review and optimize LLM prompts so they stay focused, clear, contradiction-free, and keep every output
contract.

> 中文说明见下方 [中文](#中文)。

## What's inside

| Plugin | Skill | What it does |
| --- | --- | --- |
| `prompt-focus` | `/prompt-focus` | Reviews a prompt across seven dimensions (focus, de-dup, drop noise, disambiguate, fix contradictions, show don't tell, structure), fixes the six common drifts users introduce when editing prompts, and never cuts hard constraints. |

## Install

```
/plugin marketplace add bianzhonglin/prompt-focus
/plugin install prompt-focus@prompt-focus-marketplace
```

Then invoke in any session:

```
/prompt-focus
```

and point it at the prompt you want optimized.

## Identity

Maintainer / author: **Absen-Colin** ([@bianzhonglin](https://github.com/bianzhonglin)).
Repository: `https://github.com/bianzhonglin/prompt-focus`.

If you fork this marketplace, update the identity fields in
`.claude-plugin/marketplace.json`, `plugins/prompt-focus/.claude-plugin/plugin.json`, `LICENSE`,
and the install command above.

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

---

## 中文

一个 [Claude Code](https://claude.com/claude-code) 插件市场,托管 **prompt-focus** 技能:审查并优化
写给 LLM 的提示词,使其聚焦、清晰、无矛盾,并完整保留输出契约。

### 内容

| 插件 | 技能 | 作用 |
| --- | --- | --- |
| `prompt-focus` | `/prompt-focus` | 从七个维度审查提示词(聚焦、去重、删噪音、消歧义、修矛盾、给示例、结构化),修正用户改写提示词后最常见的六类偏差,且绝不删除硬约束。 |

### 安装

```
/plugin marketplace add bianzhonglin/prompt-focus
/plugin install prompt-focus@prompt-focus-marketplace
```

随后在任意会话中调用:

```
/prompt-focus
```

并指明要优化的那段提示词即可。

### 署名

维护者 / 作者:**Absen-Colin**([@bianzhonglin](https://github.com/bianzhonglin))。
仓库:`https://github.com/bianzhonglin/prompt-focus`。

若 fork 本市场,请同步更新 `.claude-plugin/marketplace.json`、
`plugins/prompt-focus/.claude-plugin/plugin.json`、`LICENSE` 中的署名字段,以及上面的安装命令。

### 目录结构

```
.claude-plugin/marketplace.json          # 市场清单(列出插件)
plugins/prompt-focus/
  .claude-plugin/plugin.json             # 插件清单
  skills/prompt-focus/SKILL.md           # 技能本体
LICENSE
README.md
```

### 许可

MIT,见 [LICENSE](LICENSE)。
