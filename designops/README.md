# DesignOps

**Your setup assistant for agentic design — by Design Agent Lab**

DesignOps is a Claude skill that checks what you have installed, installs what you need, and walks you through adding the tools that power agentic design. Step by step, no jargon, no guesswork.

---

## Before You Start

You will need:

- **Claude Desktop app** — not the browser version. [Download here](https://claude.ai/download)
- **Claude Pro, Max, Team or Enterprise** — a paid plan is required

DesignOps will automatically install:
- **Homebrew** — Mac only
- **Node.js** — required for all tools

---

## Install DesignOps

**If you have Node.js**, ask Claude:

```
Install the designops skill from github.com/designagentlab/skills/designops
```

**If you have no idea what Node.js is**, paste this into Claude Desktop:

```
Read and follow the setup at raw.githubusercontent.com/designagentlab/skills/main/designops/SKILL.md
```

Claude handles the rest.

---

## What DesignOps Does

After checking your system and installing the required tools, DesignOps will offer to set up:

**Playwright** — free, no account needed
Lets Claude browse the web. Great for competitor research, SEO audits, and reading any website.

**Gemini Image Generation** — requires a paid Google AI Studio account
Generate images directly inside Claude using Google's AI. Note: not free — Google charges per image.

**Figma Console MCP** — requires Figma Professional or above
Connect Claude directly to your Figma Desktop for design automation.
Powered by the [figma-mcp-console-setup](../figma-mcp-console-setup) skill.

---

## Platform Support

| Feature | macOS | Windows |
|---|---|---|
| Homebrew install | ✅ | — |
| Node.js install | ✅ | ✅ |
| Playwright MCP | ✅ | ✅ |
| Gemini Image Generation | ✅ | ✅ |
| Figma Console MCP | ✅ | ✅ |

---

## Part of Design Agent Lab

DesignOps is part of the [Design Agent Lab](https://designagentlab.com) open source skills library — a collection of Claude skills built for designers.

*Automate routine. Craft exceptional.*
