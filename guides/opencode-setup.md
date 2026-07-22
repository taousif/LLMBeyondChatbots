# OpenCode Setup Guide

## What is OpenCode?

OpenCode is an open source AI coding agent that helps you write code in your terminal, IDE, or desktop. It supports 75+ LLM providers and is built for privacy.

## Desktop App (GUI)

OpenCode offers a native desktop app (beta) with a graphical interface, multi-session tabs, drag-and-drop, and a built-in editor.

### Download

Download from [opencode.ai/download](https://opencode.ai/download) or GitHub Releases.

| Platform | Install |
|----------|---------|
| macOS (Apple Silicon) | `brew install --cask opencode-desktop` or download .dmg |
| macOS (Intel) | download .dmg from releases |
| Windows | `scoop install extras/opencode-desktop` or download .exe |
| Linux | .deb, .rpm, or AppImage from releases |

### First Launch & Config

1. Launch the app and run `/connect` in the chat
2. Select **OpenCode Zen** (free built-in models) or another provider
3. Sign in and paste your API key

Configuration is stored at:
- **macOS**: `~/Library/Application Support/opencode/`
- **Windows**: `%APPDATA%\opencode\`
- **Linux**: `~/.config/opencode/`

### Key Shortcuts

| Action | Shortcut |
|--------|----------|
| New Session | `Cmd/Ctrl + N` |
| Open File | `Cmd/Ctrl + O` |
| Toggle Sidebar | `Cmd/Ctrl + B` |
| Settings | `Cmd/Ctrl + ,` |

The desktop app auto-updates on launch. Check manually via the app menu.

## Installation

### macOS / Linux
```bash
curl -fsSL https://opencode.ai/install | bash
```

### Alternative methods

**npm:**
```bash
npm install -g opencode-ai
```

**Homebrew:**
```bash
brew install anomalyco/tap/opencode
```

**Bun:**
```bash
bun install -g opencode-ai
```

**pnpm:**
```bash
pnpm install -g opencode-ai
```

**Yarn:**
```bash
yarn global add opencode-ai
```

**Arch Linux:**
```bash
sudo pacman -S opencode
```

### Windows (via WSL recommended)
```bash
choco install opencode
# or
scoop install opencode
# or
npm install -g opencode-ai
```

### Docker
```bash
docker run -it --rm ghcr.io/anomalyco/opencode
```

## Prerequisites

- A modern terminal emulator (WezTerm, Alacritty, Ghostty, Kitty)
- API keys for the LLM providers you want to use

## Configuration

### Option 1: OpenCode Zen (recommended for new users)
Run `/connect` in the TUI, select opencode, sign in at [opencode.ai/auth](https://opencode.ai/auth), add billing details, and paste your API key.

### Option 2: Other providers
Configure any supported provider with their API key.

## Initialize a Project

```bash
cd /path/to/project
opencode
/init
```

This creates an `AGENTS.md` file (should be committed to git).

## Basic Usage

- **Ask questions** — `How is authentication handled in @file.ts`
- **Add features** — Switch to Plan mode (Tab key), describe intent, iterate, switch back to Build mode
- **Make changes** — Directly describe what to change
- **Undo/Redo** — `/undo` or `/redo` commands

## Customization

- Themes, keybinds, formatters, custom commands
- Configure via the OpenCode config file

## Share Conversations

Use `/share` to create a shareable link to any conversation.

## More Info

- Docs: [https://opencode.ai/docs](https://opencode.ai/docs)
- GitHub: [https://github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)
