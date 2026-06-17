# prompt-focus

A [Claude Code](https://claude.com/claude-code) plugin marketplace hosting the **prompt-focus** skill:
review and optimize LLM prompts so they stay focused, clear, contradiction-free, and keep every output
contract.

> 中文说明见下方 [中文](#中文)。

## What's inside

| Plugin | Skill | What it does |
| --- | --- | --- |
| `prompt-focus` | `/prompt-focus:prompt-focus` | Reviews a prompt across seven dimensions (focus, de-dup, drop noise, disambiguate, fix contradictions, show don't tell, structure), fixes the six common drifts users introduce when editing prompts, and never cuts hard constraints. |

## Install

```
/plugin marketplace add bianzhonglin/prompt-focus
/plugin install prompt-focus@prompt-focus
```

Then invoke in any session:

```
/prompt-focus:prompt-focus
```

and point it at the prompt you want optimized.

## Runtimes

The skill is written to run under both **Claude Code** and **OpenAI Codex**. The skill body
(`SKILL.md`) is shared; only the frontmatter/metadata differs per runtime:

- **Claude Code** — installed as the plugin above. Discovers the skill from `SKILL.md`.
- **Codex** — reads the same `SKILL.md` plus the optional `agents/openai.yaml` UI metadata next to it.
  Copy the `skills/prompt-focus/` folder into your Codex skills directory (see your Codex CLI version's
  docs for the exact path), then validate with Codex's `quick_validate.py`.

> On Windows, run Codex's validator in UTF-8 mode (`set PYTHONUTF8=1`) — see below. The files in this
> repo are clean UTF-8; a GBK-default shell will otherwise misread the non-ASCII characters.

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
  skills/prompt-focus/
    SKILL.md                             # the skill itself (shared by both runtimes)
    agents/openai.yaml                   # Codex UI metadata (ignored by Claude Code)
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
| `prompt-focus` | `/prompt-focus:prompt-focus` | 从七个维度审查提示词(聚焦、去重、删噪音、消歧义、修矛盾、给示例、结构化),修正用户改写提示词后最常见的六类偏差,且绝不删除硬约束。 |

### 安装

```
/plugin marketplace add bianzhonglin/prompt-focus
/plugin install prompt-focus@prompt-focus
```

随后在任意会话中调用:

```
/prompt-focus:prompt-focus
```

并指明要优化的那段提示词即可。

### 运行时

该技能同时面向 **Claude Code** 与 **OpenAI Codex** 编写。技能正文(`SKILL.md`)两端共用,仅每个运行时
的 frontmatter/元数据不同:

- **Claude Code** —— 即上面的插件安装方式,从 `SKILL.md` 识别技能。
- **Codex** —— 读取同一个 `SKILL.md`,外加同目录下可选的 `agents/openai.yaml` UI 元数据。把
  `skills/prompt-focus/` 整个目录拷进 Codex 的 skills 目录(确切路径见你所用 Codex CLI 版本的文档),
  再用 Codex 的 `quick_validate.py` 校验。

> Windows 下运行 Codex 校验器请开启 UTF-8 模式(`set PYTHONUTF8=1`),见下文。本仓库文件均为干净
> UTF-8;若用默认 GBK 的终端读取,非 ASCII 字符会被误读成乱码。

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
  skills/prompt-focus/
    SKILL.md                             # 技能本体(两个运行时共用)
    agents/openai.yaml                   # Codex UI 元数据(Claude Code 会忽略)
LICENSE
README.md
```

### 许可

MIT,见 [LICENSE](LICENSE)。
