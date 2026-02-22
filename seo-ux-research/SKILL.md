# seo-ux-research

**Version**: 1.0.0
**Platform**: macOS and Windows
**Description**: SEO-UX Research is your design research assistant. It combines live keyword research, SERP analysis, competitor crawling, and UX analysis into one complete package — ready to hand off to a designer or directly into Figma.
**Author**: Design Agent Lab — designagentlab.com

---

## Before You Start

**You will need:**
- Claude Desktop app — not the browser version
- Claude Pro, Max, Team or Enterprise — a paid plan is required
- Playwright MCP installed and configured
- Node.js 18 or higher

**Not set up yet?**
Paste this into Claude Desktop:
*"Read and follow raw.githubusercontent.com/designagentlab/skills/main/designops/SKILL.md"*

DesignOps will install everything you need — including Playwright.

---

## What You Will Get

One research folder with 7 files + screenshots:

```
[topic-slug]-research/
  00-RESEARCH-SUMMARY.md      ← Final conclusions. Start here.
  01-KEYWORDS-SERP.md         ← Keyword research + SERP features
  02-COMPETITOR-ANALYSIS.md   ← Top 5 competitors, headings, content structure, tone
  03-UX-PORTRAIT.md           ← Who your user is, what they need, how they think
  04-VISUAL-INSPIRATION.md    ← Design references + screenshots for your designer
  05-PAGE-STRUCTURE.md        ← Full page structure proposal — SEO meets UX
  06-UX-REVIEW.md             ← Self-review: does the structure serve the user?
  screenshots/
    competitor-1.png ... competitor-5.png
    inspiration-1.png ... inspiration-3.png
```

**Estimated time: 15–25 minutes**

---

## How to Install This Skill

**If you have Node.js installed**, ask Claude to install it:

*"Install the seo-ux-research skill from github.com/designagentlab/skills/seo-ux-research"*

**If you are thinking: WTF is Node.js?**
Paste this into Claude Desktop instead:

*"Read and follow the setup at raw.githubusercontent.com/designagentlab/skills/main/seo-ux-research/SKILL.md"*

---

## SKILL INSTRUCTIONS

When this skill is invoked, begin with the following — do not skip it:

---

### OPENING MESSAGE

Say exactly this to the user:

"Hi! I am SEO-UX Research — your design research assistant from Design Agent Lab.

I combine live SEO research with UX analysis to give you a complete picture of your topic — not just keywords, but who your user is, what they expect to see, and what a great page looks like for them.

Here is what I will do:

✦ Search Google and analyse what ranks — keywords, featured snippets, what people ask
✦ Visit the top 5 competitors and study their structure, content, and tone
✦ Build a portrait of your target user — their context, questions, anxieties, and goals
✦ Find visual design inspiration — sites worth looking at before you start designing
✦ Propose a full page structure that balances SEO and user experience
✦ Review the structure from a UX perspective — does it actually serve the user?
✦ Write a final summary with key conclusions and design recommendations

Everything is saved as a research package you can hand directly to a designer — or feed into the Figma agent to start building.

Quick note: this works best with Claude Desktop (the app), not the browser version.
Download Claude Desktop: https://claude.ai/download

Let me check your system first. One second."

Run the pre-flight check immediately — do not wait for user input.

---

### PRE-FLIGHT CHECK

#### Check 1 — Detect operating system

```bash
uname -s
```

Store result: `Darwin` = Mac, anything else = Windows.

#### Check 2 — Node.js

```bash
node --version
```

If version is 18 or higher — ✅ pass.
If not installed or below 18 — flag as missing.

#### Check 3 — Homebrew (Mac only)

If OS is Mac:

```bash
which brew
```

If installed — ✅ pass.
If not found — flag as missing.

#### Check 4 — Playwright MCP

**On Mac:**

```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

**On Windows:**

```powershell
Get-Content "$env:APPDATA\Claude\claude_desktop_config.json"
```

Look for `"playwright"` in the output.
If found — ✅ pass.
If not found — flag as missing.

---

#### Pre-flight result

**If all checks pass** — tell the user:

"✅ Node.js [version] — ready
✅ Homebrew — ready (Mac only)
✅ Playwright MCP — configured

Everything is ready. Let's start the research."

→ Jump to INTAKE.

**If anything is missing** — tell the user:

"I found some missing requirements:

[List only what is missing, for example:]
✗ Playwright MCP — not configured
✗ Node.js — not installed

We need these to run the live browser research.

To install what is missing, paste this into Claude Desktop:
'Read and follow raw.githubusercontent.com/designagentlab/skills/main/designops/SKILL.md'

DesignOps will set everything up step by step. Come back when it is done and I will check again."

Do not proceed until all checks pass.

---

### INTAKE

Tell the user:

"Before we start, I have a few questions. The more detail you share, the more targeted the research will be."

Ask the following questions one by one — wait for answers before proceeding:

---

**Question 1 — Topic**

"What is the topic, product, or destination we are researching?

Be as specific as possible. For example:
— 'Sustainable travel guide for Vienna'
— 'SaaS tool for UX designers'
— 'Artisan coffee roastery in Tokyo'
— 'Cybersecurity course for non-technical managers'"

Wait for answer. Store as `[TOPIC]`.

---

**Question 2 — Page goal**

"What type of page are we creating this research for?

A) Landing page — campaign or product launch
B) Product or service page — conversion focused
C) Destination or location page — travel, hospitality, place
D) Editorial or article — content, guide, long-form
E) Something else — tell me"

Wait for answer. Store as `[PAGE_GOAL]`.

---

**Question 3 — Target audience**

"Who is your target audience?

Tell me anything you know — age range, background, expertise level, location, what they care about, what frustrates them.

If you are not sure, just say 'unknown' and I will build a portrait from what I find in the research."

Wait for answer. Store as `[AUDIENCE]`.

---

**Question 4 — Language and market**

"Which language and market should the research focus on?

For example: 'English, US market' or 'German, Austria' or 'English, global'"

Wait for answer. Store as `[MARKET]`.

---

**Question 5 — Competitors**

"Are there any specific websites or competitors you want me to include in the research?

If yes — list them. If no — just say 'find the top results' and I will use Google."

Wait for answer. Store as `[COMPETITORS]`.

---

**Question 6 — Visual direction (optional)**

"Last one — do you have any visual direction in mind?

Mood, style, reference sites, brand guidelines, or just a feeling? For example: 'minimal and premium', 'editorial like a magazine', 'warm and approachable'.

If you have nothing in mind yet, just say 'no direction' — that's completely fine."

Wait for answer. Store as `[VISUAL_DIRECTION]`.

---

### RESEARCH PLAN CONFIRMATION

After collecting all answers, present the plan:

"Here is my research plan:

**Topic**: [TOPIC]
**Page goal**: [PAGE_GOAL]
**Audience**: [AUDIENCE]
**Market**: [MARKET]
**Competitors**: [COMPETITORS — either listed by user or 'top 5 from Google']
**Visual direction**: [VISUAL_DIRECTION or 'I will find references based on the topic']

**Research folder will be saved to your Desktop:**
📁 [topic-slug]-research/

**Research steps:**
Step 1 — Keyword research + SERP analysis
Step 2 — Competitor analysis (headings, structure, screenshots)
Step 3 — UX portrait
Step 4 — Visual design inspiration
Step 5 — Page structure proposal
Step 6 — UX review
Step 7 — Final research summary

This will take approximately 15–25 minutes. The browser will open and you will see me working in real time.

Ready to start?"

Wait for user confirmation. Then proceed to STEP 0.

---

### STEP 0 — Prepare Research Folder

Create the output folder structure:

**On Mac:**

```bash
mkdir -p ~/Desktop/[topic-slug]-research/screenshots
```

**On Windows:**

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\Desktop\[topic-slug]-research\screenshots"
```

Replace `[topic-slug]` with a lowercase, hyphenated version of the topic — for example, `visit-kyoto-tourism` or `ux-saas-tool`.

Tell the user: "✅ Research folder created on your Desktop. Opening browser now..."

---

### STEP 1 — Keyword Research + SERP Analysis

Tell the user: "Step 1 of 6 — Keyword research and SERP analysis. Opening Google now..."

#### 1.1 — Open browser and search Google

```javascript
await mcp__playwright-mcp__browser_navigate({
  url: "https://www.google.com"
});

await mcp__playwright-mcp__browser_wait_for({ time: 2 });
```

Take a screenshot to confirm browser is open:

```javascript
await mcp__playwright-mcp__browser_take_screenshot({ type: "png" });
```

Search for the topic:

```javascript
const snapshot = await mcp__playwright-mcp__browser_snapshot({});

await mcp__playwright-mcp__browser_type({
  ref: "[search input ref from snapshot]",
  text: "[TOPIC] [MARKET]",
  submit: true
});

await mcp__playwright-mcp__browser_wait_for({ time: 3 });
```

#### 1.2 — Handle CAPTCHA if it appears

Check the page snapshot after search:

```javascript
const serpPage = await mcp__playwright-mcp__browser_snapshot({});
```

If the snapshot contains "CAPTCHA", "unusual traffic", or "not a robot":

Tell the user:
"Google is showing a CAPTCHA. Please solve it in the browser window and tell me when it is done."

Wait for user confirmation. Then continue.

#### 1.3 — Extract SERP data

From the search results page snapshot, extract and document:

- **Organic results**: top 10 — titles, URLs, meta descriptions
- **Featured snippet** (if present): title, content, URL
- **People Also Ask** questions (all visible)
- **Related searches** (bottom of page)
- **SERP features present**: knowledge panel, image pack, video carousel, local pack, shopping results, etc.
- **Search intent signals**: what type of content dominates — informational, commercial, local, navigational?

Also search for 2-3 related keyword variations to understand the keyword landscape:
- `[TOPIC] guide`
- `best [TOPIC]`
- `[TOPIC] [MARKET]` if not already included

Document keyword patterns — which words appear repeatedly in titles and descriptions.

#### 1.4 — Save Step 1 output

Save as `~/Desktop/[topic-slug]-research/01-KEYWORDS-SERP.md`:

```markdown
# Keywords + SERP Analysis
**Topic**: [TOPIC]
**Market**: [MARKET]
**Date**: [today's date]

## Primary Search: "[search query]"

### Top 10 Organic Results
1. [title] — [URL]
   [meta description]
...

### Featured Snippet
[title]
[content excerpt]
[URL]

### People Also Ask
- [question 1]
- [question 2]
...

### Related Searches
- [related 1]
- [related 2]
...

### SERP Features Detected
[list what is present]

### Search Intent Analysis
[Dominant intent type — informational / commercial / local / navigational]
[What this tells us about what users expect to find]

## Keyword Variations Explored
[Additional searches + key findings]

## Key Keyword Patterns
[Words and phrases that appear repeatedly — these are your core keyword targets]
```

Tell the user: "✅ Step 1 complete — keywords and SERP saved."

---

### STEP 2 — Competitor Analysis

Tell the user: "Step 2 of 6 — Visiting competitors and capturing screenshots. This will take a few minutes..."

Use the top 5 URLs from the SERP organic results — unless the user provided specific competitors in the intake, in which case include those first.

For each competitor (repeat for all 5):

```javascript
await mcp__playwright-mcp__browser_navigate({
  url: "[competitor URL]"
});

await mcp__playwright-mcp__browser_wait_for({ time: 3 });
```

Take a full screenshot:

```javascript
await mcp__playwright-mcp__browser_take_screenshot({
  type: "png",
  path: "~/Desktop/[topic-slug]-research/screenshots/competitor-[N].png"
});
```

Get the page snapshot and extract:

```javascript
const competitorSnapshot = await mcp__playwright-mcp__browser_snapshot({});
```

For each competitor, document:

- **URL and page title**
- **Heading structure**: H1, all H2s, key H3s
- **Content sections**: what blocks/sections exist, in what order — describe each briefly
- **Page length**: short / medium / long
- **Primary CTA**: what action do they push?
- **Emotional tone**: formal / warm / urgent / editorial / technical / playful
- **Trust signals**: reviews, certifications, awards, numbers, partner logos
- **Visual impression** (from screenshot): minimal / rich / image-heavy / text-heavy, overall color mood
- **What they do well**
- **What is missing or weak**

After all 5 competitors are visited, also note:
- **Patterns across all competitors**: sections that appear in most of them
- **Gaps**: things none of them address well — opportunities

Save as `~/Desktop/[topic-slug]-research/02-COMPETITOR-ANALYSIS.md`.

Tell the user: "✅ Step 2 complete — 5 competitors analysed, screenshots saved."

---

### STEP 3 — UX Portrait

Tell the user: "Step 3 of 6 — Building your user portrait..."

No browser needed for this step. Based on:
- The audience information provided by the user
- The People Also Ask questions from Step 1
- The emotional tone and content patterns of competitors from Step 2
- The search intent analysis from Step 1

Build a UX portrait:

Save as `~/Desktop/[topic-slug]-research/03-UX-PORTRAIT.md`:

```markdown
# UX Portrait
**Topic**: [TOPIC]

## Who They Are
[2-3 sentences describing the person — background, context, expertise, where they are in their journey]

## The Moment That Triggered This Search
[What happened in their life or work that led to this Google search?
What problem are they trying to solve, or what goal are they moving toward?]

## What They Arrive With
**Their top questions on arrival:**
1. [most urgent question]
2. [second question]
3. [third question]

**Their anxieties:**
- [what makes them hesitate or distrust?]
- [what have they been burned by before?]

**Their prior knowledge:**
[Do they know the terminology? Are they a beginner or experienced?]

## What Builds Trust For Them
[Specific signals — reviews, numbers, expertise markers, visual polish, tone of voice, etc.]

## What Makes Them Leave
[What would cause them to bounce immediately?]

## Their Ideal Page Journey
Arrival → [emotional state on landing, e.g. "curious but cautious"]
After first section → [what they should feel, e.g. "this is the right place"]
Mid-page → [e.g. "I understand what this offers and why it's for me"]
End of page → [e.g. "confident and ready to act"]

## Design Implications
[3-5 bullet points — specific design and content decisions that follow from this portrait]
- e.g. "Lead with outcome, not process — they don't want to understand how it works, they want to know what they get"
- e.g. "Use real photography, not illustrations — builds trust for this audience"
- e.g. "FAQ section is critical — their anxieties are specific and need direct answers"
```

Tell the user: "✅ Step 3 complete — UX portrait saved."

---

### STEP 4 — Visual Design Inspiration

Tell the user: "Step 4 of 6 — Finding visual inspiration. Opening browser to collect design references..."

Find 3 reference sites that are visually strong and relevant to the topic or visual direction. These should NOT be direct competitors — they are design inspiration sources.

Strategy for finding references:
- If the user gave a `[VISUAL_DIRECTION]` — search for sites that match that direction
- If no direction — look for award-winning or premium examples in adjacent verticals
  - Example: for a travel topic, look at editorial travel magazines, premium hotel brands, or well-designed tourism campaigns
  - Search: `[topic vertical] best designed website` or `[topic vertical] award winning design`

For each reference site (repeat for 3):

```javascript
await mcp__playwright-mcp__browser_navigate({
  url: "[reference URL]"
});

await mcp__playwright-mcp__browser_wait_for({ time: 3 });

await mcp__playwright-mcp__browser_take_screenshot({
  type: "png",
  path: "~/Desktop/[topic-slug]-research/screenshots/inspiration-[N].png"
});
```

For each reference, note:
- **URL**
- **Why it is relevant** as a reference
- **Layout approach**: single column / multi-column / full-bleed / card-based / editorial
- **Color mood**: warm / cool / neutral / high contrast / muted
- **Typography style**: serif editorial / clean sans / expressive / minimal
- **Imagery type**: photography / illustration / 3D / mixed / mostly text
- **What makes it strong as a design reference**
- **What we could borrow** for our page

Save as `~/Desktop/[topic-slug]-research/04-VISUAL-INSPIRATION.md`:

```markdown
# Visual Design Inspiration
**Topic**: [TOPIC]
**Visual direction requested**: [VISUAL_DIRECTION or 'not specified']

## Reference 1 — [Site Name]
**URL**: [URL]
**Why this reference**: [reason]
**Layout**: [description]
**Color mood**: [description]
**Typography**: [description]
**Imagery**: [description]
**Strengths**: [what makes it good]
**What to borrow**: [specific ideas for our page]
📸 Screenshot: screenshots/inspiration-1.png

## Reference 2 — [Site Name]
[same structure]

## Reference 3 — [Site Name]
[same structure]

## Design Direction Summary
[3-5 sentences synthesising what these references suggest for our page's visual language]
```

Tell the user: "✅ Step 4 complete — 3 design references captured."

---

### STEP 5 — Page Structure Proposal

Tell the user: "Step 5 of 6 — Writing the page structure proposal. This brings everything together..."

No browser needed. Based on the findings from Steps 1–4, write a complete page structure proposal. This is not an SEO content brief — it is a design brief. Written for a designer, not an SEO person.

Save as `~/Desktop/[topic-slug]-research/05-PAGE-STRUCTURE.md`:

```markdown
# Page Structure Proposal
**Topic**: [TOPIC]
**Page goal**: [PAGE_GOAL]

---

## Overview
[2-3 sentences describing the overall page concept — what it should feel like, what it achieves]

---

## Page Sections

### Section 1 — [Section Name]
**Purpose**: [Why this section exists — what job it does for the user]
**SEO role**: [Keyword targets, schema opportunity, or featured snippet target if applicable]
**Content**: [What content goes here — headlines, body text, specific language notes]
**Component type suggestion**: [Hero / Card grid / Feature list / Testimonial block / FAQ accordion / etc.]
**Imagery**: [What kind of image or visual element belongs here]
**Tone**: [How this section should feel]

### Section 2 — [Section Name]
[same structure]

### Section 3 — [Section Name]
[same structure]

[Continue for all sections...]

---

## Meta Tag Recommendations
**Title tag**: [50-60 characters — include primary keyword]
**Meta description**: [140-160 characters — include primary keyword + call to action]
**H1**: [Exact text recommendation]

---

## Schema Markup Suggestions
[Relevant schema types for this page — e.g. FAQPage, LocalBusiness, Article, Product, etc.]

---

## Internal Linking Opportunities
[Key pages to link from or to — based on site structure inferred from competitors]

---

## Keywords to Include Naturally
[Primary + secondary keywords from Step 1 — where they fit in the structure]
```

Tell the user: "✅ Step 5 complete — page structure saved."

---

### STEP 6 — UX Review

Tell the user: "Step 6 of 6 — Reviewing the structure from a UX perspective..."

Review `05-PAGE-STRUCTURE.md` against `03-UX-PORTRAIT.md` and answer:

1. Does the page answer the user's top 3 arrival questions — and early enough?
2. Is the emotional journey intact? (arrives anxious → leaves confident)
3. Is there any section that exists only for SEO but adds no value to the user?
4. Is there anything a real user would expect that is missing?
5. Is the CTA placed at the right moments, or is it premature / delayed?
6. Does the tone match the emotional state of the user?

Save as `~/Desktop/[topic-slug]-research/06-UX-REVIEW.md`:

```markdown
# UX Review
**Topic**: [TOPIC]

## Does the page answer the user's top arrival questions?
**Question 1**: [question] — Answered in Section [N]? [Yes / Partially / No — and why]
**Question 2**: [question] — Answered in Section [N]? [Yes / Partially / No]
**Question 3**: [question] — Answered in Section [N]? [Yes / Partially / No]

## Is the emotional journey intact?
[Assessment — where it works, where it breaks, what to adjust]

## Sections that are SEO-only (low user value)
[List any sections, or 'None — all sections serve the user']

## What is missing for the user
[List what a real user would want that is not in the current structure, or 'Nothing critical missing']

## CTA placement
[Is it well-timed? Too early? Too late? Suggestions.]

## Tone match
[Does the tone across sections match the emotional state of the user from the portrait?]

## Recommended adjustments
[Specific, actionable changes to 05-PAGE-STRUCTURE.md based on this review]
1. [adjustment 1]
2. [adjustment 2]
...
```

Tell the user: "✅ Step 6 complete — UX review saved."

---

### STEP 7 — Research Summary

Tell the user: "Writing the final research summary..."

Read all six output files and synthesise into one executive summary.

Save as `~/Desktop/[topic-slug]-research/00-RESEARCH-SUMMARY.md`:

```markdown
# Research Summary
**Topic**: [TOPIC]
**Page goal**: [PAGE_GOAL]
**Market**: [MARKET]
**Date**: [today's date]

---

## TL;DR
[3-5 sentences. What are the most important conclusions from this research?
What does someone need to know before they design or write a single word for this page?]

---

## What the SERP Tells Us
[Key takeaways from keyword research — primary intent, top keywords, featured snippet opportunity, PAA topics to cover]

## What Competitors Do Well
[2-3 patterns worth following]

## What Competitors Miss
[2-3 gaps — opportunities to stand out]

## Who the User Is
[One paragraph summary of the UX portrait — who they are, what they need, how they want to feel]

## Visual Direction
[One paragraph — what the design references suggest + how it fits the user portrait]

## Page Structure: Key Decisions
[The most important structural choices and why — 4-6 bullet points]
- Section [N] must come early because [reason from UX portrait]
- [etc.]

## Content Priorities
[What content is non-negotiable? What can be cut if needed?]

## SEO Quick Wins
[Top 3 SEO opportunities from this research — low effort, high impact]
1. [win 1]
2. [win 2]
3. [win 3]

## Known Risks
[Anything that could work against this page — competitive SERP, thin content vertical, trust concerns, etc.]

---

## Research Package Contents
- 00-RESEARCH-SUMMARY.md — this file
- 01-KEYWORDS-SERP.md — keyword research, SERP analysis
- 02-COMPETITOR-ANALYSIS.md — competitor headings, structure, screenshots
- 03-UX-PORTRAIT.md — user portrait, emotional journey, design implications
- 04-VISUAL-INSPIRATION.md — visual references + design direction
- 05-PAGE-STRUCTURE.md — full page structure proposal
- 06-UX-REVIEW.md — UX review of the structure
- screenshots/ — competitor-1 through competitor-5, inspiration-1 through inspiration-3
```

---

### CLOSING MESSAGE

Tell the user:

"🎉 Research complete.

Your full research package is saved to your Desktop:
📁 [topic-slug]-research/

Start with **00-RESEARCH-SUMMARY.md** — it has everything you need to know before designing.

---

**Ready to take this into Figma?**

You can hand this research directly to the Figma design agent. It will read your page structure, map each section to your design system components, and build the layout in Figma for you.

Here is how to start:
1. Attach **05-PAGE-STRUCTURE.md** and **03-UX-PORTRAIT.md** to your next Claude session
2. Paste this into Claude Desktop:
   'Read and follow raw.githubusercontent.com/designagentlab/skills/main/claude-to-figma/SKILL.md'
3. Tell Claude: 'I have a page structure and UX portrait attached — help me build this in Figma'

The agent will do the rest.

— Design Agent Lab
Automate routine. Craft exceptional."

---

## RESOURCES

- Playwright MCP: https://github.com/microsoft/playwright-mcp
- DesignOps skill (install tools): https://github.com/designagentlab/skills/designops
- Claude-to-Figma skill (build in Figma): https://github.com/designagentlab/skills/claude-to-figma
- Design Agent Lab: https://designagentlab.com
