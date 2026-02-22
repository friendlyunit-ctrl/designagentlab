# figma-mcp-console-setup

**Version**: 1.6.0
**Platform**: macOS and Windows
**Description**: Step-by-step guided setup of Figma Console MCP for designers. Walks the user through the full installation flow — from package manager to a verified Figma connection.
**Author**: Design Agent Lab — designagentlab.com

---

## Before You Start

**You will need:**
- Claude Desktop app — not the browser version
- Claude Pro, Max, Team or Enterprise
- Figma Professional or above
- Figma Desktop app — not the web version

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

Quick note: This setup works best with Claude Desktop (the app). If you are using the web browser version, please download Claude Desktop first — it takes just a minute.

**Download Claude Desktop:** https://claude.ai/download

Then come back and paste this skill into Claude Desktop. It's worth it!

---

Before we start, here's what you'll need:

✦ Claude Desktop app
✦ Claude Pro, Max, Team or Enterprise
✦ Figma Professional or above
✦ Figma Desktop app
   Download: https://www.figma.com/downloads/

Got everything? Great! We will go through this together — 9 steps in total. Some I handle automatically. Some will ask you to click something in Figma. I will explain clearly at every stage.

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
8. Select the following scopes — check all of these:

**Users**
☑ current_user:read

**Files**
☑ file_comments:read
☑ file_comments:write
☑ file_content:read
☑ file_metadata:read
☑ file_versions:read

**Variables**
☑ file_variables:read
☑ file_variables:write

**Dev resources**
☑ file_dev_resources:read
☑ file_dev_resources:write

**Libraries**
☑ library_assets:read

9. Click **Generate token**

⚠️ Important: Copy the token immediately — it starts with 'figd_' and you will not be able to see it again after leaving the page.

Paste your token here when ready:"

Wait for the user to paste their token. Validate that it starts with `figd_`.

If valid — store as `FIGMA_ACCESS_TOKEN` and tell the user: "✅ Token received. Moving on."
If invalid — ask the user to check and try again.

Reference: https://help.figma.com/hc/en-us/articles/8085703771159-Manage-personal-access-tokens

---

## STEP 6 — Write MCP Config File

Tell the user: "Now I will write the MCP config file automatically. You do not need to do anything."

First, read the existing config file:

```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

**If file exists AND already contains a `figma-console` entry:**

Do NOT add a duplicate. Instead update only the `FIGMA_ACCESS_TOKEN` value in the existing entry. Tell the user: "✅ Figma Console MCP is already in your config. I have updated the token."

**If file exists but does NOT contain a `figma-console` entry:**

Carefully merge the new entry into the existing `mcpServers` object, preserving all other entries. Never overwrite the whole file.

**If file does not exist** — create it:

```bash
mkdir -p ~/Library/Application\ Support/Claude
```

Then write this config:

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

After writing, always verify the file is valid — check there is only ONE `figma-console` entry:

```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

If a duplicate exists — fix it by removing the duplicate entry before proceeding.

Tell the user: "✅ Config file written successfully."

Then tell the user: "Please restart Claude Desktop now. Come back when it has reopened."

Wait for confirmation before proceeding to Step 7.

---

## STEP 7 — Import Desktop Bridge Plugin

Tell the user:

"This is the most important step. The Figma Desktop Bridge plugin is the gateway between Claude and Figma — without it running, nothing works.

We will import it once. After that, you just need to launch it every time you work with the agent in Figma.

Let me find the plugin on your machine and copy the path to your clipboard automatically."

Run:

```bash
MANIFEST=$(find ~/.npm/_npx -name "manifest.json" -path "*/figma-desktop-bridge/*" 2>/dev/null | head -1)
if [ -z "$MANIFEST" ]; then
  BASE=$(npx figma-console-mcp@latest --print-path 2>/dev/null)
  MANIFEST="${BASE}/figma-desktop-bridge/manifest.json"
fi
echo "$MANIFEST"
echo "$MANIFEST" | pbcopy
```

**If the path is found** — tell the user this (be specific and clear):

"✅ Found it.

Your plugin manifest is at:
$MANIFEST

Here's what that path means:
- The `.npm/_npx` folder is where npm caches packages
- The long code (`[unique-code]`) is generated by npm and is different on every machine — this is normal
- Inside that folder is the figma-console-mcp package
- Inside that is the figma-desktop-bridge folder with the manifest.json file we need

I have copied this entire path to your clipboard.

Now do this in Figma Desktop:

1. Open any Figma file
2. Go to **Plugins → Development → Import plugin from manifest...**
3. A Finder file picker window will open — this is the standard Mac file browser
4. The path you need is very deep in folders (in `.npm/_npx/...`), so instead of clicking through many folders, we will use a Mac shortcut:
   - Press **Cmd + Shift + G** — a small input field will appear at the top
   - This is the 'Go to Folder' shortcut — it lets you paste a path directly instead of browsing
5. Press **Cmd + V** to paste the path (I already copied it to your clipboard)
6. Press **Enter** — Finder will instantly jump to that folder
7. You will see the file `manifest.json` in the folder
8. Click on it and click **Open**
9. Figma will import the plugin — 'Figma Desktop Bridge' will now appear in **Plugins → Development**

Tell me when you see 'Figma Desktop Bridge' in your Development plugins list."

**If the path is empty** — the package cache may not exist yet. Tell the user:

"The plugin file is not cached yet. Let me download it now."

Run:

```bash
npx -y figma-console-mcp@latest
```

This will download the package. After it completes, I will run the find command again and give you the path.

Wait for confirmation. Proceed to Step 8.

---

## STEP 8 — Launch Desktop Bridge Plugin

Tell the user:

"Now we need to launch the Desktop Bridge plugin. This is the gateway — it must be running every time you use the agent in Figma. Think of it as turning the key before starting the engine.

Here is how to launch it:

1. Open any Figma file in Figma Desktop
2. In the Figma menu at the top, go to **Plugins**
3. Look for the **Development** section (usually at the bottom of the menu)
4. Inside Development, you will see 'Figma Desktop Bridge' — click on it
5. The plugin window will open — keep it open in a separate window, do not close it
6. You should see a connection status in the plugin window. Look for:
   - ✅ 'MCP ready'
   - ✅ 'Connected to ws://localhost:[port]' (the port number will be something like 9223, 9224, etc.)

⚠️ Important: The plugin window must stay open while you work. If you close it, the connection drops. Keep it open in the background.

Also make sure 'Use Developer VM' is enabled in Figma:
- Go to **Plugins → Development → Use Developer VM** — toggle it on if it is off

Tell me what you see in the plugin window when it opens."

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

Run this test command automatically:

```powershell
echo "claude-code-enabled"
```

**If the command runs successfully** — tell the user: "✅ Code execution is enabled. Moving on." — proceed to WIN Step 1.

**If the command fails** — tell the user:

"I need one permission before we start. Claude needs to be allowed to run code on your machine — without this I cannot handle the automatic steps.

Here is how to enable it:

1. Click the **Claude menu** in the top left
2. Go to **Settings**
3. Click **Capabilities**
4. Toggle on **'Code execution and file creation'**

Come back when it is on — I will check again automatically."

Then re-run the test command to verify. Proceed to WIN Step 1 when confirmed.

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
8. Select the following scopes — check all of these:

**Users**
☑ current_user:read

**Files**
☑ file_comments:read
☑ file_comments:write
☑ file_content:read
☑ file_metadata:read
☑ file_versions:read

**Variables**
☑ file_variables:read
☑ file_variables:write

**Dev resources**
☑ file_dev_resources:read
☑ file_dev_resources:write

**Libraries**
☑ library_assets:read

9. Click **Generate token**

⚠️ Important: Copy the token immediately — it starts with 'figd_' and you will not be able to see it again after leaving the page.

Paste your token here when ready:"

Wait for the user to paste their token. Validate that it starts with `figd_`.

If valid — store as `FIGMA_ACCESS_TOKEN` and tell the user: "✅ Token received. Moving on."
If invalid — ask the user to check and try again.

Reference: https://help.figma.com/hc/en-us/articles/8085703771159-Manage-personal-access-tokens

---

## WIN STEP 5 — Write MCP Config File

Tell the user: "Now I will write the MCP config file automatically. You do not need to do anything."

First, read the existing config file:

```powershell
Get-Content "$env:APPDATA\Claude\claude_desktop_config.json"
```

**If file exists AND already contains a `figma-console` entry:**

Do NOT add a duplicate. Instead update only the `FIGMA_ACCESS_TOKEN` value in the existing entry. Tell the user: "✅ Figma Console MCP is already in your config. I have updated the token."

**If file exists but does NOT contain a `figma-console` entry:**

Carefully merge the new entry into the existing `mcpServers` object, preserving all other entries. Never overwrite the whole file.

**If file does not exist** — create the folder:

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

Tell the user: "This is the most important step. The Figma Desktop Bridge plugin is the gateway between Claude and Figma — without it running, nothing works.

We will import it once. After that, you just need to launch it every time you work with the agent in Figma.

Let me find the plugin on your machine and copy the path to your clipboard automatically."

Run:

```powershell
$MANIFEST = Get-ChildItem -Path "$env:LOCALAPPDATA\npm-cache\_npx","$env:APPDATA\npm-cache\_npx" -Filter "manifest.json" -Recurse -ErrorAction SilentlyContinue |
  Where-Object { $_.DirectoryName -like "*figma-desktop-bridge*" } |
  Select-Object -First 1 -ExpandProperty FullName
if (-not $MANIFEST) {
  $BASE = (npx figma-console-mcp@latest --print-path 2>$null)
  $MANIFEST = "$BASE\figma-desktop-bridge\manifest.json"
}
Set-Clipboard $MANIFEST
Write-Output "Path: $MANIFEST"
```

**If the path is found** — tell the user this (be specific and clear):

"✅ Found it.

Your plugin manifest is at:
$MANIFEST

Here's what that path means:
- The `AppData\Roaming\npm-cache\_npx` folder is where npm caches packages on Windows
- The long code (`[unique-code]`) is generated by npm and is different on every machine — this is normal
- Inside that folder is the figma-console-mcp package
- Inside that is the figma-desktop-bridge folder with the manifest.json file we need

I have copied this entire path to your clipboard.

Now do this in Figma Desktop:

1. Open any Figma file
2. Go to **Plugins → Development → Import plugin from manifest...**
3. A File Explorer window will open — this is the standard Windows file browser
4. The path you need is very deep in folders (in `AppData\Roaming\npm-cache\_npx\...`), so instead of clicking through many folders, we will use the address bar:
   - At the very top of File Explorer, you see the current folder path (like `C:\Users\YourName\Documents`)
   - Click on the **address bar** at the top
5. Press **Ctrl + V** to paste the path (I already copied it to your clipboard)
6. Press **Enter** — File Explorer will instantly jump to that folder
7. You will see the file `manifest.json` in the folder
8. Click on it and click **Open**
9. Figma will import the plugin — 'Figma Desktop Bridge' will now appear in **Plugins → Development**

Tell me when you see 'Figma Desktop Bridge' in your Development plugins list."

Wait for confirmation. Proceed to WIN Step 7.

---

## WIN STEP 7 — Launch Desktop Bridge Plugin

Tell the user:

"Now we need to launch the Desktop Bridge plugin. This is the gateway — it must be running every time you use the agent in Figma. Think of it as turning the key before starting the engine.

Here is how to launch it:

1. Open any Figma file in Figma Desktop
2. In the Figma menu at the top, go to **Plugins**
3. Look for the **Development** section (usually at the bottom of the menu)
4. Inside Development, you will see 'Figma Desktop Bridge' — click on it
5. The plugin window will open — keep it open in a separate window, do not close it
6. You should see a connection status in the plugin window. Look for:
   - ✅ 'MCP ready'
   - ✅ 'Connected to ws://localhost:[port]' (the port number will be something like 9223, 9224, etc.)

⚠️ Important: The plugin window must stay open while you work. If you close it, the connection drops. Keep it open in the background.

Also make sure 'Use Developer VM' is enabled in Figma:
- Go to **Plugins → Development → Use Developer VM** — toggle it on if it is off

Tell me what you see in the plugin window when it opens."

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
