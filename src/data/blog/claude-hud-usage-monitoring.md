---
title: "Claude HUD: Stop Opening Your Browser to Check API Usage"
author: atooooomic
pubDatetime: 2026-01-21T00:00:00Z
slug: claude-hud-usage-monitoring
featured: true
draft: false
tags:
  - claude-code
  - developer-tools
  - productivity
  - monitoring
description:
  A real-time usage monitoring plugin for Claude Code that saves you from constantly checking the web dashboard. Plus a look at CodexBar for multi-service monitoring.
timezone: "America/New_York"
---

If you're a regular Claude Code user, you've probably experienced this: you're in the middle of a productive coding session, and suddenly you wonder, "How much of my rate limit have I used?" Then comes the context switch—opening your browser, navigating to claude.ai, waiting for it to load, finding the usage page—all while your flow state evaporates.

There's a better way.

## Table of contents

## The Problem: Context Switching Kills Productivity

Every time you need to check your Claude usage, you're making a choice: keep working blind and risk hitting rate limits mid-task, or interrupt your flow to check the web dashboard. Neither option is ideal.

For developers who live in the terminal, opening a browser just to glance at a usage meter feels particularly painful. It's the digital equivalent of leaving your workshop to check the fuel gauge in your car—necessary, but disruptive.

## Enter Claude HUD

[Claude HUD](https://github.com/jarrodwatts/claude-hud) is a plugin that brings your Claude Code session stats directly into your terminal's status line. No separate windows, no tmux panes, no browser tabs—just persistent, at-a-glance information exactly where you're already working.

Created by [Jarrod Watts](https://github.com/jarrodwatts), this plugin uses Claude Code's native statusline API (introduced in v1.0.80) to display real-time information about your session without any additional setup beyond installation.

## What It Shows

Claude HUD provides a comprehensive dashboard of information:

### Core Metrics

- **Context usage**: Visual progress bar showing how full your context window is
- **Rate limits**: Real-time consumption display (for Pro, Max, and Team subscribers)
- **Active model and subscription tier**: Know exactly which Claude model you're using
- **Session duration**: How long you've been working

### Development Context

- **Project path**: Configurable display of your current directory (1-3 levels)
- **Git branch**: Current branch name with optional dirty status indicator
- **Configuration counts**: See how many CLAUDE.md files, rules, MCPs, and hooks are active

### Activity Monitoring

- **Tool activity**: Running tools show a spinner with the target file; completed tools aggregate by type with counts
- **Active agents**: Track which subagents are running with elapsed time
- **Todo progress**: Real-time task completion counters

All of this updates approximately every 300ms, giving you a genuinely real-time view of your Claude Code session.

## Installation is Trivial

Getting started takes three commands:

```bash
# Add the marketplace
/plugin marketplace add jarrodwatts/claude-hud

# Install the plugin
/plugin install claude-hud

# Configure your preferences
/claude-hud:setup
```

The setup command offers three presets:

- **Full**: Everything enabled, maximum visibility
- **Essential**: Core metrics only, cleaner display
- **Minimal**: Just the essentials for a distraction-free statusline

You can also toggle individual elements or manually edit the config at `~/.claude/plugins/claude-hud/config.json` for granular control.

**Linux users**: If you encounter cross-device link errors during installation, set `TMPDIR=~/.cache/tmp` before running the install command.

## My Experience: Daily Driver Material

I've been using Claude HUD for several weeks now, and it's become an indispensable part of my workflow. **This plugin actually delivers on its promise.**

The most immediate benefit is psychological: I no longer have that nagging uncertainty about my usage. A quick glance at the statusline tells me if I'm at 20% or 80% of my rate limit, which fundamentally changes how I structure my work sessions.

### What Makes It Valuable

**1. Flow State Preservation**

Not having to context-switch to check usage means I stay in the terminal. This seems small, but the cognitive cost of switching applications, navigating to a dashboard, and returning is surprisingly high. Claude HUD eliminates this entirely.

**2. Proactive Resource Management**

When I can see my context window filling up (say, hitting 70-80%), I know it's time to either wrap up the current task or commit my changes and start a fresh session. Without this visibility, I'd often hit context limits mid-task and lose momentum.

**3. Agent Awareness**

The agent tracking is particularly useful when working with complex orchestration setups (like oh-my-claudecode, which I covered in [my previous post](/posts/oh-my-claudecode-orchestration)). Seeing which subagents are active and how long they've been running helps me understand what's happening under the hood.

**4. Git Branch Safety**

The git branch indicator has saved me multiple times from making changes on the wrong branch. It's a simple feature, but having that constant reminder in my peripheral vision prevents costly mistakes.

### The Configuration Sweet Spot

After experimenting with all three presets, I settled on a custom configuration that's slightly more than "Essential" but less than "Full." I keep:

- Context usage percentage
- Rate limit display
- Current model
- Git branch (with dirty indicator)
- Tool activity

I disabled the session duration timer and config counts—interesting data, but not actionable enough for my workflow.

## The One Missing Piece: Weekly Usage

Here's my main complaint: **Claude HUD doesn't show weekly usage totals.**

For Claude Pro/Max/Team users, both the 5-hour session window and the weekly limit matter. Claude HUD shows the former beautifully, but the latter is invisible. This means I still occasionally need to check the web dashboard to see how much of my weekly quota remains.

This isn't a dealbreaker—the per-session visibility is still valuable—but weekly quota tracking would make the plugin genuinely complete.

## If You Want More: CodexBar

If you're on macOS and want comprehensive usage monitoring across multiple AI services (not just Claude), [CodexBar](https://github.com/steipete/CodexBar) is worth exploring.

### What CodexBar Offers

CodexBar is a macOS menu bar application that monitors usage for a wide range of AI coding assistants:

- Claude Code
- OpenAI Codex
- Cursor
- GitHub Copilot
- Gemini
- And many more (Antigravity, Droid, z.ai, Kimi, Kiro, Vertex AI, Augment, Amp, JetBrains AI)

### Key Advantages

**1. Multi-Service Dashboard**

If you use multiple AI coding tools, CodexBar provides a unified view. You can see all your usage metrics in one place without hunting through different web dashboards.

**2. Weekly Limit Tracking**

This is the big one: CodexBar shows both 5-hour session windows **and** weekly usage with countdown timers for when limits reset. It fills the gap that Claude HUD leaves open.

**3. Visual Quota Indicators**

The menu bar icon uses a two-bar system where the top bar represents your session window and the bottom shows weekly usage. At a glance, you can see both limits.

**4. Cost Analysis**

For Codex and Claude, CodexBar can analyze local usage data to show cost breakdowns over 30-day windows. This is particularly useful if you're managing budget for API usage.

**5. CLI Integration**

CodexBar includes a command-line interface (`codexbar`) for scripting and CI integration. You can run `codexbar cost --provider claude` to get usage reports programmatically.

### Installation

```bash
# Via Homebrew
brew install --cask steipete/tap/codexbar

# Or download directly from GitHub releases
```

Requires macOS 14+ (Sonoma) for the GUI, though the CLI works on Linux too.

### Privacy Considerations

CodexBar does local parsing by default, with browser cookies as an opt-in feature. No passwords are stored, and all data processing happens on your device. The app doesn't scan your disk or phone home.

## When to Use What

Here's my practical recommendation:

### Use Claude HUD if:

- You primarily use Claude Code in the terminal
- You want zero-friction, always-visible session info
- You care about per-session management more than weekly quotas
- You prefer minimal configuration overhead
- You want agent and tool activity tracking

### Use CodexBar if:

- You're on macOS and want a menu bar solution
- You use multiple AI coding services
- Weekly quota tracking is important to you
- You want cost analysis and usage breakdowns
- You prefer a GUI over terminal-based monitoring

### Use Both if:

You want terminal-integrated monitoring (Claude HUD) **and** weekly limit tracking plus multi-service support (CodexBar). They're complementary, not competitive.

I currently run both: Claude HUD for in-terminal awareness during active sessions, and CodexBar for checking weekly limits and monitoring other services I occasionally use.

## Why This Matters: Developer Experience

These tools might seem like minor conveniences, but they represent something important: treating API-based AI tools like first-class development resources that deserve proper instrumentation.

We monitor our CI/CD pipelines, we track our database performance, we watch our cloud costs—why shouldn't we have equally good visibility into our AI tool usage?

Claude HUD and CodexBar are part of a broader trend: developers building better tooling around AI services because the official tools don't quite meet their needs. These projects exist because someone said, "I'm tired of opening my browser to check a number," and then actually built the solution.

## Conclusion

Claude HUD has earned its place in my daily toolkit. It's one of those rare tools that does exactly what it promises with minimal fuss: keeps your Claude Code usage visible so you can work without second-guessing your remaining quota.

The missing weekly usage tracking is my only real gripe, but CodexBar fills that gap nicely if you're on macOS. Between the two, you can achieve comprehensive visibility into your AI coding tool usage without ever context-switching to a web dashboard.

**Bottom line**: If you use Claude Code regularly, install Claude HUD. The three-command setup is trivial, and the constant visibility into your session metrics is genuinely useful. It's not a productivity game-changer, but it's a papercut eliminator—and sometimes, that's exactly what you need.

Stop opening your browser to check API usage. Your flow state will thank you.

## Resources

- **Claude HUD GitHub**: [jarrodwatts/claude-hud](https://github.com/jarrodwatts/claude-hud)
- **CodexBar GitHub**: [steipete/CodexBar](https://github.com/steipete/CodexBar)
- **Claude Code**: [Official Anthropic tool](https://claude.ai/code)
- **Claude HUD on Claude Plugin Hub**: [Plugin listing](https://www.claudepluginhub.com/plugins/davepoon-claude-hud-plugins-claude-hud)

---

**Sources:**

- [GitHub - jarrodwatts/claude-hud](https://github.com/jarrodwatts/claude-hud)
- [Claude HUD - Real-Time Visibility into Your Claude Code Sessions](https://chsami.com/posts/claude-hud.html)
- [Claudepluginhub - claude-hud listing](https://www.claudepluginhub.com/plugins/davepoon-claude-hud-plugins-claude-hud)
- [GitHub - steipete/CodexBar](https://github.com/steipete/CodexBar)
- [CodexBar - Mac Menubar Apps](https://macmenubar.app/app/codex-bar)
- [CodexBar Official Site](https://codexbar.app/)
- [SessionWatcher - Monitor Claude Code & Codex](https://www.sessionwatcher.com/)
