# figma-mcp-console-setup

**Version**: 1.1.0
**Platform**: macOS and Windows
**Description**: Step-by-step guided setup of Figma Console MCP for designers. Walks the user through the full installation flow — from package manager to a verified Figma connection.
**Author**: Design Agent Lab — designagentlab.com

---

## Before You Start

**You will need:**
- Claude Pro, Max, Team or Enterprise
- Figma Professional or above
- Figma Desktop app — the web version will not work

If you have all three — you are ready. Let's go.

---

## What This Skill Does

This skill is a guided onboarding companion. It walks designers through connecting Claude Desktop to Figma Console MCP — step by step, checking each stage before moving to the next.

Some steps run automatically. Some require you to act in Terminal or Figma. The skill explains what to do clearly at every stage — no assumptions, no jargon.

**Total steps: 9**
**Estimated time: ~10 minutes**

---

## How to Install This Skill

**If you have Node.js installed**, ask Claude to install it:

*"Install the figma-mcp-console-setup skill from github.com/designagentlab/skills/figma-mcp-console-setup"*

**If you are thinking: WTF is Node.js?**
Paste this into Claude Desktop instead:

*"Read and follow the setup at raw.githubusercontent.com/designagentlab/skills/main/figma-mcp-console-setup/SKILL.md"*

Claude handles the rest. No Terminal needed.

---

## SKILL INSTRUCTIONS

When this skill is invoked, begin with the following introduction — do not skip it:

---

### OPENING MESSAGE

Say exactly this to the user:

"Welcome to the Figma Console MCP setup guide.

Before we start — three quick things you will need:

✦ Claude Pro, Max, Team or Enterprise
✦ Figma Professional or above
✦ Figma Desktop app — the web version will not work

Got all three? Then we are ready to go.

We will go through the installation together — 9 steps in total. Some I will handle automatically. Some will ask you to click something in Figma. I will tell you clearly what to do at each stage.

The whole process takes about 10 minutes.

Let me check your system now. One second."

Run Step 0 immediately — do not wait for user input.

---

## STEP 0 — System Check

Run automatically:

```bash
uname -s
```

- If result is `Darwin` — tell the user: "✅ macOS detected. Starting Mac setup." — follow the **MAC FLOW** below.
- If result is `Windows_NT` or command fails — tell the user: "✅ Windows detected. Starting Windows setup." — jump to **WINDOWS FLOW** section.
- If result is anything else — tell the user: "Your operating system could not be identified. This guide supports macOS and Windows. Please let me know which you are using."

---

---

# MAC FLOW

---

## STEP 0.5 — Enable Claude Code

Tell the user:

Run this test command automatically:

```bash
echo "claude-code-enabled"
```

**If the command runs successfully** — tell the user: "✅ Code execution is enabled. Moving on." — proceed to Step 1.

**If the command fails** — tell the user:

"I need one permission before we start. Claude needs to be allowed to run code on your machine — without this I cannot handle the automatic steps.

Here is how to enable it:

1. Click the **Claude menu** in the top left
2. Go to **Settings**
3. Click **Capabilities**
4. Toggle on **'Code execution and file creation'**

Come back when it is on — I will check again automatically."

Then re-run the test command to verify. Proceed to Step 1 when confirmed.

---

## STEP 1 — Welcome and Overview

Tell the user:

"Great, we are good to go. Here is what we will do together:

Step 1 — ✅ You are here
Step 2 — Check and install Homebrew
Step 3 — Check and install Node.js
Step 4 — Confirm Figma Desktop is installed
Step 5 — Get your Figma Personal Access Token
Step 6 — Write the MCP config file automatically
Step 7 — Import the Figma Desktop Bridge plugin
Step 8 — Launch the Desktop Bridge plugin in Figma
Step 9 — Verify the connection

Let's go."

---

## STEP 2 — Homebrew

### What is Homebrew?
Tell the user: "Homebrew is a package manager for Mac — it helps us install developer tools like Node.js easily. Think of it as an app store for the Terminal."

### Check if Homebrew is installed:

```bash
which brew
```

**If installed** — tell the user: "✅ Homebrew is already installed. Moving on." — proceed to Step 3.

**If not installed** — tell the user:

"Homebrew is not installed. We need to install it. Here is how:

1. Press **Cmd + Space** to open Spotlight
2. Type **Terminal** and press Enter
3. A window will appear with a blinking cursor
4. Copy and paste this command, then press Enter:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

The script will pause and ask for your Mac password before it starts — this is normal. This is the same password you use to unlock your Mac or install software. Type it and press Enter — you won't see any characters appear as you type, that's expected. Just type it and hit Enter.

The installation takes 2-3 minutes. Come back when it is done and tell me."

Wait for user confirmation. Then verify:

```bash
which brew
```

If confirmed — proceed to Step 3.
If still failing — direct user to: https://docs.brew.sh/Manpage

---

## STEP 3 — Node.js

### Check if Node.js is installed:

```bash
node --version
```

**If installed and version is 18 or higher** — tell the user: "✅ Node.js [version] is installed. Moving on." — proceed to Step 4.

**If not installed or version is below 18** — tell the user:

"We need to install Node.js. I will do this automatically for you now."

Run automatically:

```bash
brew install node
```

Then verify:

```bash
node --version
```

Proceed to Step 4.

---

## STEP 4 — Figma Desktop App

First, check automatically:

```bash
mdfind "kMDItemKind == 'Application'" | grep -i "Figma"
```

**If Figma.app is found** — tell the user: "✅ Figma Desktop is installed. Moving on." — proceed to Step 5.

**If not found** — tell the user:

"Figma Console MCP requires the Figma Desktop app — the web version will not work, and it does not appear to be installed on your machine.

Please download and install it from: https://www.figma.com/downloads/

Come back when it is installed and you have signed in."

Wait for confirmation. Proceed to Step 5.

---

## STEP 5 — Figma Personal Access Token

Tell the user:

"Now we need a Figma Personal Access Token. This allows Claude to connect to your Figma files.

Here is how to get one:

1. Open Figma Desktop and go to your account menu (top left, your avatar)
2. Click **Settings**
3. Go to the **Security** tab
4. Scroll down to **Personal access tokens**
5. Click **Generate new token**
6. Give it a name — for example: 'Claude MCP'
7. Set the expiration as you prefer
8. Click **Generate token**

⚠️ Important: Copy the token immediately — it starts with 'figd_' and you will not be able to see it again after leaving the page.

Paste your token here when ready:"

Wait for the user to paste their token. Validate that it starts with `figd_`.

If valid — store as `FIGMA_ACCESS_TOKEN` and tell the user: "✅ Token received. Moving on."
If invalid — ask the user to check and try again.

Reference: https://help.figma.com/hc/en-us/articles/8085703771159-Manage-personal-access-tokens

---

## STEP 6 — Write MCP Config File

Tell the user: "Now I will write the MCP config file automatically. You do not need to do anything."

Check if config file exists:

```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

**If file exists** — read the content and merge the new server entry carefully, preserving any existing mcpServers entries.

**If file does not exist** — create it:

```bash
mkdir -p ~/Library/Application\ Support/Claude
```

Write the following config to `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "[USER_TOKEN_HERE]",
        "ENABLE_MCP_APPS": "true"
      }
    }
  }
}
```

Replace `[USER_TOKEN_HERE]` with the token provided in Step 5.

Verify the file was written correctly:

```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

Tell the user: "✅ Config file written successfully."

Then tell the user: "Please restart Claude Desktop now. Come back when it has reopened."

Wait for confirmation before proceeding to Step 7.

---

## STEP 7 — Import Desktop Bridge Plugin

Tell the user: "Now we need to import the Figma Desktop Bridge plugin. This is what connects Figma and Claude.

First, I will find the plugin path on your machine."

Run:

```bash
npx figma-console-mcp@latest --print-path
```

Take the output path and append `/figma-desktop-bridge/manifest.json` to it.

Tell the user:

"Your Desktop Bridge plugin manifest is located at:

[FULL PATH TO MANIFEST.JSON]

Now do the following in Figma Desktop:

1. Open any Figma file
2. Go to the menu: **Plugins → Development → Import plugin from manifest...**
3. In the dialog, paste this path or navigate to it:

[FULL PATH TO MANIFEST.JSON]

4. Figma will open a Finder window — press **Cmd + Shift + G** to open the 'Go to Folder' dialog, paste the path above and press Enter
5. Select the **manifest.json** file and click **Open**
6. The plugin 'Figma Desktop Bridge' will appear in your Development plugins

Tell me when it is imported."

Wait for confirmation. Proceed to Step 8.

---

## STEP 8 — Launch Desktop Bridge Plugin

Tell the user:

"Almost there! Now we need to run the Desktop Bridge plugin in Figma.

1. In Figma Desktop, go to: **Plugins → Development → Figma Desktop Bridge**
2. The plugin window will open
3. You should see a connection status — look for:
   - ✅ 'MCP ready'
   - ✅ 'Connected to ws://localhost:[port]'

If you see either of these — you are connected. Tell me what you see."

**If connection confirmed** — proceed to Step 9.

**If not connecting** — run troubleshooting:

Tell the user: "Let's fix the connection. Please run this in Terminal:"

```bash
pkill -f figma-console-mcp
```

Then:

```bash
lsof -i :9223
```

If a process is still on the port, tell the user to run:

```bash
kill -9 [PID]
```

Then ask the user to close and reopen the Desktop Bridge plugin in Figma.

Ports used by Figma Console MCP: **9223–9232**. If the default port is taken, the server falls back through this range automatically.

---

## STEP 9 — Verify Connection

Tell the user: "Last step. Let's confirm everything is working."

Run:

```
Check Figma status
```

Using tool: `mcp__figma-console__figma_get_status`

**If response shows** `"active": "websocket"` — tell the user:

"🎉 You are connected! Figma Console MCP is live on port [port number].

You are ready to start working with the agent in Figma.

Welcome to agentic design.

— Design Agent Lab
Automate routine. Craft exceptional."

**If connection fails** — run full troubleshooting checklist:

```bash
# Kill old processes
pkill -f figma-console-mcp

# Check port status
lsof -i :9223
lsof -i :9224
lsof -i :9225
```

Then reconnect:

```
mcp__figma-console__figma_reconnect
```

Ask user to close and reopen Desktop Bridge plugin in Figma and try again.

---

---

# WINDOWS FLOW

---

## WIN STEP 0.5 — Enable Claude Code

Tell the user:

"One more thing before we start. Claude needs permission to run code on your machine — without this, I cannot handle the automatic steps.

Here is how to enable it:

1. Click the **Claude menu** in the top left
2. Go to **Settings**
3. Click **Capabilities**
4. Toggle on **'Code execution and file creation'**

Come back when it is on."

Wait for user confirmation. Then proceed to WIN Step 1.

---

## WIN STEP 1 — Welcome and Overview

Tell the user:

"Great, we are good to go. Here is what we will do together on Windows:

Step 1 — ✅ You are here
Step 2 — Check and install Node.js
Step 3 — Confirm Figma Desktop is installed
Step 4 — Get your Figma Personal Access Token
Step 5 — Write the MCP config file automatically
Step 6 — Import the Figma Desktop Bridge plugin
Step 7 — Launch the Desktop Bridge plugin in Figma
Step 8 — Verify the connection

Let's go."

---

## WIN STEP 2 — Node.js

### Check if Node.js is installed:

```powershell
node --version
```

**If installed and version is 18 or higher** — tell the user: "✅ Node.js [version] is installed. Moving on." — proceed to WIN Step 3.

**If not installed or below version 18:**

First try winget automatically (available on Windows 10/11):

```powershell
winget install OpenJS.NodeJS
```

**If winget succeeds** — verify:

```powershell
node --version
```

Tell the user: "✅ Node.js installed successfully." — proceed to WIN Step 3.

**If winget is not available** — tell the user:

"We need to install Node.js manually. Here is how:

1. Press **Windows key**, type **PowerShell** and press Enter
2. Go to: https://nodejs.org/en/download
3. Download the **Windows Installer (.msi)** — LTS version
4. Run the installer and follow the steps — click Next through all defaults
5. Come back when it is done and tell me."

Wait for confirmation. Verify:

```powershell
node --version
```

Proceed to WIN Step 3.

---

## WIN STEP 3 — Figma Desktop App

Check automatically:

```powershell
Test-Path "$env:LOCALAPPDATA\Figma\Figma.exe"
```

**If found** — tell the user: "✅ Figma Desktop is installed. Moving on." — proceed to WIN Step 4.

**If not found** — tell the user:

"Figma Console MCP requires the Figma Desktop app — the web version will not work, and it does not appear to be installed on your machine.

Please download and install it from: https://www.figma.com/downloads/

Come back when it is installed and you have signed in."

Wait for confirmation. Proceed to WIN Step 4.

---

## WIN STEP 4 — Figma Personal Access Token

Tell the user:

"Now we need a Figma Personal Access Token. This allows Claude to connect to your Figma files.

Here is how to get one:

1. Open Figma Desktop and go to your account menu (top left, your avatar)
2. Click **Settings**
3. Go to the **Security** tab
4. Scroll down to **Personal access tokens**
5. Click **Generate new token**
6. Give it a name — for example: 'Claude MCP'
7. Set the expiration as you prefer
8. Click **Generate token**

⚠️ Important: Copy the token immediately — it starts with 'figd_' and you will not be able to see it again after leaving the page.

Paste your token here when ready:"

Wait for the user to paste their token. Validate that it starts with `figd_`.

If valid — store as `FIGMA_ACCESS_TOKEN` and tell the user: "✅ Token received. Moving on."
If invalid — ask the user to check and try again.

Reference: https://help.figma.com/hc/en-us/articles/8085703771159-Manage-personal-access-tokens

---

## WIN STEP 5 — Write MCP Config File

Tell the user: "Now I will write the MCP config file automatically. You do not need to do anything."

Check if config file exists:

```powershell
Test-Path "$env:APPDATA\Claude\claude_desktop_config.json"
```

**If file exists** — read the content and merge the new server entry carefully, preserving any existing mcpServers entries.

**If file does not exist** — create the folder and file:

```powershell
New-Item -ItemType Directory -Force -Path "$env:APPDATA\Claude"
```

Write the following config to `%APPDATA%\Claude\claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "[USER_TOKEN_HERE]",
        "ENABLE_MCP_APPS": "true"
      }
    }
  }
}
```

Replace `[USER_TOKEN_HERE]` with the token provided in WIN Step 4.

Verify the file was written correctly:

```powershell
Get-Content "$env:APPDATA\Claude\claude_desktop_config.json"
```

Tell the user: "✅ Config file written successfully."

Then tell the user: "Please restart Claude Desktop now. Come back when it has reopened."

Wait for confirmation before proceeding to WIN Step 6.

---

## WIN STEP 6 — Import Desktop Bridge Plugin

Tell the user: "Now we need to import the Figma Desktop Bridge plugin. This is what connects Figma and Claude.

First, I will find the plugin path on your machine."

Run:

```powershell
npx figma-console-mcp@latest --print-path
```

Take the output path and append `\figma-desktop-bridge\manifest.json` to it.

Tell the user:

"Your Desktop Bridge plugin manifest is located at:

[FULL PATH TO MANIFEST.JSON]

Now do the following in Figma Desktop:

1. Open any Figma file
2. Go to the menu: **Plugins → Development → Import plugin from manifest...**
3. A File Explorer window will open — click in the address bar at the top, paste this path and press Enter:

[FULL PATH TO MANIFEST.JSON]

4. Select the **manifest.json** file and click **Open**
5. The plugin 'Figma Desktop Bridge' will appear in your Development plugins

Tell me when it is imported."

Wait for confirmation. Proceed to WIN Step 7.

---

## WIN STEP 7 — Launch Desktop Bridge Plugin

Tell the user:

"Almost there! Now we need to run the Desktop Bridge plugin in Figma.

1. In Figma Desktop, go to: **Plugins → Development → Figma Desktop Bridge**
2. The plugin window will open
3. You should see a connection status — look for:
   - ✅ 'MCP ready'
   - ✅ 'Connected to ws://localhost:[port]'

If you see either of these — you are connected. Tell me what you see."

**If connection confirmed** — proceed to WIN Step 8.

**If not connecting** — run troubleshooting:

Tell the user: "Let's fix the connection. Please open PowerShell and run this:"

```powershell
taskkill /F /IM node.exe
```

Then check port:

```powershell
netstat -ano | findstr :9223
```

If a process is on the port, note the PID and run:

```powershell
taskkill /PID [PID] /F
```

Then ask the user to close and reopen the Desktop Bridge plugin in Figma.

Ports used by Figma Console MCP: **9223–9232**. If the default port is taken, the server falls back through this range automatically.

---

## WIN STEP 8 — Verify Connection

Tell the user: "Last step. Let's confirm everything is working."

Using tool: `mcp__figma-console__figma_get_status`

**If response shows** `"active": "websocket"` — tell the user:

"🎉 You are connected! Figma Console MCP is live on port [port number].

You are ready to start working with the agent in Figma.

Welcome to agentic design.

— Design Agent Lab
Automate routine. Craft exceptional."

**If connection fails** — run full troubleshooting:

```powershell
# Kill old processes
taskkill /F /IM node.exe

# Check port
netstat -ano | findstr :9223
```

Then reconnect:

```
mcp__figma-console__figma_reconnect
```

Ask user to close and reopen Desktop Bridge plugin in Figma and try again.

---

## TROUBLESHOOTING REFERENCE

### "Cannot connect to Figma Desktop"
- Confirm Figma Desktop is open (not the web version)
- Confirm Desktop Bridge plugin is running
- Kill orphan processes: `pkill -f figma-console-mcp`
- Restart Claude Desktop
- Reopen Desktop Bridge plugin

### "Invalid token" or authentication errors
- Confirm token starts with `figd_`
- Generate a new token from Figma Settings → Security
- Rewrite config file with new token (repeat Step 6)

### "Tools not showing up in Claude"
- Restart Claude Desktop completely
- Verify config file syntax is valid JSON
- Check: `cat ~/Library/Application\ Support/Claude/claude_desktop_config.json`

### Port conflicts
- Multiple Claude sessions create multiple MCP instances
- Always run one Claude session at a time
- Mac: kill orphan processes with `pkill -f figma-console-mcp`
- Windows: kill orphan processes with `taskkill /F /IM node.exe`
- Never force-quit Figma — it leaves orphan processes
- Ports used: 9223–9232

---

## BEST PRACTICES

- Keep only one Claude Desktop session running at a time
- Always check plugin status before starting work
- Keep the Desktop Bridge plugin window open while working
- If switching between Figma files — reconnect: `figma_reconnect`
- Kill old processes at the start of each session

---

## RESOURCES

- Figma Console MCP: https://github.com/southleft/figma-console-mcp
- Figma Personal Access Tokens: https://help.figma.com/hc/en-us/articles/8085703771159
- Homebrew: https://brew.sh
- Homebrew Docs: https://docs.brew.sh/Manpage
- Design Agent Lab: https://designagentlab.com
