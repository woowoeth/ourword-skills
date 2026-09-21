# ourword skills

Two Claude Agent Skills for **[ourword.ai](https://ourword.ai)** — 403 deep reads on
171 figures and classic texts across 2,600 years. There are author and topic pages
too, but the front door is **the situation you are actually in**.

| skill | for |
|---|---|
| [`ourword-en`](ourword-en/) | English. 121 situation groups. |
| [`ourword`](ourword/) | 中文。112 组处境。 |

The Chinese and English sides are **not translations of each other**. Same 403
chapters, two separately written situation layers — what an English speaker says to
themselves at 2am is not a translation of what a Chinese speaker says.

## Install

```bash
npx skills add https://github.com/woowoeth/ourword-skills/tree/main/ourword-en
```

Or by hand:

```bash
git clone https://github.com/woowoeth/ourword-skills
cp -R ourword-skills/ourword-en ~/.claude/skills/
```

Doing it by hand, the folder name must match the `name` in the frontmatter. Use `.claude/skills/` inside
a project instead of `~/.claude/skills/` to scope it to that project.

The skill works on its own: it reads `https://ourword.ai/en/llms.txt`, no configuration.
For real retrieval instead of a flat index, add the companion MCP server:

```bash
claude mcp add ourword -- uvx ourword-mcp
```

## Why it tells the model *not* to search

Someone types *"my boss keeps changing priorities."* The entry that answers it reads
*"Five things are on fire and I am spread across all five."* **Zero words in common.**
Literal search was measured at **0 hits, best score 0.11** before it was removed.
So the skill browses the situation taxonomy and lets the model do the matching it is
already better at.

It also says no: if the situation is not in the library it returns zero and says so,
and the skill forbids filling the gap with general advice.

## This repo is a mirror

The source of truth is
[`tools/skill/`](https://github.com/woowoeth/woowoeth.github.io/tree/main/tools/skill)
in the main repo, where both files are covered by a gate
(`scripts/check_tools.py`: the name must equal the folder name, the hard boundaries
must still be there, and **the English file may not contain a single Chinese
character** — a translated-over English skill breaks its own last rule).
A workflow here pulls any change hourly. Open issues and PRs against the main repo.

MIT.
