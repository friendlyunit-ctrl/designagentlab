# claude-to-figma

**v1.2.0 — Your AI design partner for Figma — by Design Agent Lab**

claude-to-figma connects Claude directly to your Figma Desktop. It reads your component library, learns your design patterns, builds layouts from your components, and troubleshoots when something breaks.

---

## Before You Start

You will need:

- **Claude Desktop app** — not the browser version. [Download here](https://claude.ai/download)
- **Claude Pro, Max, Team or Enterprise** — a paid plan is required
- **Figma Professional or above**
- **Figma Desktop app** — not the web version. [Download here](https://www.figma.com/downloads/)
- **Figma Console MCP** — configured and connected

**Not set up yet?**

→ Install all tools at once with [DesignOps](../designops)
→ Set up Figma connection with [figma-mcp-console-setup](../figma-mcp-console-setup)

---

## Install claude-to-figma

**If you have Node.js**, ask Claude:

```
Install the claude-to-figma skill from github.com/designagentlab/skills/claude-to-figma
```

**No Node.js?** Paste this into Claude Desktop:

```
Read and follow the setup at raw.githubusercontent.com/designagentlab/skills/main/claude-to-figma/SKILL.md
```

---

## What You Can Do

### 1. Build context of your component library
Claude reads your Figma component file — every component name, key, node ID, variant, size, and functional role. Saves everything as `FIGMA_COMPONENTS_LIBRARY.md`. Attach this file to future Claude sessions so Claude can find and insert your components correctly.

### 2. Build context of your design patterns
Claude analyzes your actual product layouts — which components appear together, in what order, and why. Understands the design logic behind your system. Saves as `FIGMA_PATTERNS.md`. Takes 2–3 rounds of iteration as you guide and correct Claude's understanding.

### 3. Design in Figma — let's build something
With your context files attached, Claude can:
- Assemble full-page layouts from your component library
- Populate components with real content
- Map a content brief or Research Agent output to your components and build the design
- Build a Figma design system from your codebase or Storybook
- Create variables, styles, and structure files for handoff
- Ideate freely when you just need to explore

### 4. Troubleshoot Figma Console MCP
Step-by-step diagnostics for connection issues, port conflicts, font errors, component import errors, and token problems. Based on real issues encountered during the Kyoto landing page experiment.

---

## How Context Files Work

After running sub-skills 1 and 2, you get two markdown files:

```
FIGMA_COMPONENTS_LIBRARY.md   — what components exist and how to use them
FIGMA_PATTERNS.md             — how components work together in your product
```

Attach both files to any Claude conversation. Claude will use them to design with your exact components, in your exact style — without needing to re-read your Figma file every time.

---

## Real Example: Visit Kyoto Landing Page

Built in **~15 minutes** using the claude-to-figma approach:

- 9 components instantiated from library
- Full 1920 × 5601px landing page assembled
- Section titles, subtitles, and 7 FAQ questions populated
- Component stack: Header → H1 Display → Stage → 3 Carousels → Promo → FAQ → Footer

The component library (14 components) and patterns (3 layout templates) were documented first — then Claude built the full page from that context.

---

## Platform Support

| Feature | macOS | Windows |
|---|---|---|
| Pre-flight connection check | ✅ | ✅ |
| Component library context | ✅ | ✅ |
| Design patterns context | ✅ | ✅ |
| Design in Figma | ✅ | ✅ |
| Troubleshooting | ✅ | ✅ |

---

## Changelog

**v1.2.0**
- Fixed Windows troubleshooting — replaced `taskkill /F /IM node.exe` with a targeted command that only kills figma-console-mcp
- Updated multi-instance note — no need to limit Claude sessions, supported since Figma Console MCP v1.10.0
- Added official Figma Console MCP docs to resources

**v1.1.0**
- Added Figma branch recommendation to opening message — suggests creating a branch before working on live files

**v1.0.0**
- Initial release — component library context, design patterns context, design in Figma, troubleshooting

---

## Part of Design Agent Lab

claude-to-figma is part of the [Design Agent Lab](https://designagentlab.com) open source skills library — a collection of Claude skills built for designers.

*Automate routine. Craft exceptional.*
