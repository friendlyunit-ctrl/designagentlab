# seo-ux-research

**SEO meets UX. Research that is ready to design from.**

SEO-UX Research is an AI skill for designers and design teams. It runs live browser research — keyword analysis, competitor crawling, visual inspiration — and combines it with a UX portrait of your target user. The output is a complete research package you can hand directly to a designer, or feed into the Figma design agent to start building.

---

## What It Does

One command. One research folder. Seven files.

| File | Contents |
|------|----------|
| `00-RESEARCH-SUMMARY.md` | Final conclusions — start here |
| `01-KEYWORDS-SERP.md` | Keyword landscape, SERP features, People Also Ask |
| `02-COMPETITOR-ANALYSIS.md` | Top 5 competitors — headings, structure, tone, screenshots |
| `03-UX-PORTRAIT.md` | Who your user is, what they need, their emotional journey |
| `04-VISUAL-INSPIRATION.md` | Design references with screenshots |
| `05-PAGE-STRUCTURE.md` | Full page structure — SEO and UX aligned |
| `06-UX-REVIEW.md` | Self-review: does the structure serve the user? |
| `screenshots/` | Competitor and inspiration screenshots |

---

## Prerequisites

- **Claude Desktop** — [download here](https://claude.ai/download)
- **Claude Pro, Max, Team or Enterprise**
- **Node.js 18+**
- **Playwright MCP** — for live browser research

Don't have these? Run the DesignOps skill first — it installs everything:

```
"Read and follow raw.githubusercontent.com/designagentlab/skills/main/designops/SKILL.md"
```

---

## Install

**With Node.js:**

```bash
npx degit designagentlab/skills/seo-ux-research ~/.claude/skills/seo-ux-research
```

**Without Node.js** — paste into Claude Desktop:

```
"Read and follow the setup at raw.githubusercontent.com/designagentlab/skills/main/seo-ux-research/SKILL.md"
```

---

## How It Works

1. You provide the topic, page goal, target audience, and market
2. Claude opens a browser (you watch it work in real time)
3. It searches Google, analyses the SERP, visits competitors, takes screenshots
4. It builds a UX portrait of your user from the research findings
5. It finds visual design inspiration — sites worth looking at before you design
6. It writes a page structure that balances SEO and UX
7. It reviews that structure from the user's perspective
8. Everything is saved to a research folder on your Desktop

**Time: approximately 15–25 minutes**

---

## Works Best With

**claude-to-figma** — Feed the research package into the Figma design agent. It reads your page structure, maps sections to your component library, and builds the layout directly in Figma.

```
"Read and follow raw.githubusercontent.com/designagentlab/skills/main/claude-to-figma/SKILL.md"
```

---

## Platform Support

| Feature | macOS | Windows |
|---------|-------|---------|
| Live browser research | ✅ | ✅ |
| Competitor screenshots | ✅ | ✅ |
| Visual inspiration | ✅ | ✅ |
| Auto folder creation | ✅ | ✅ |

---

## Part of the Design Agent Lab Skills Library

| Skill | What it does |
|-------|-------------|
| [designops](../designops) | Installs Homebrew, Node.js, Playwright, Gemini, Figma MCP |
| [figma-mcp-console-setup](../figma-mcp-console-setup) | Connects Claude to Figma Desktop |
| [claude-to-figma](../claude-to-figma) | Reads your Figma library and builds layouts |
| **seo-ux-research** | **Researches topics — SEO + UX + visual inspiration** |

---

**Design Agent Lab**
Automate routine. Craft exceptional.
[designagentlab.com](https://designagentlab.com)
