---
title: "CodexBar: Your AI Usage Dashboard That's Always Visible"
author: atooooomic
pubDatetime: 2026-01-21T00:00:00Z
slug: codexbar-menubar-monitoring
featured: true
draft: false
tags:
  - developer-tools
  - productivity
  - monitoring
  - macos
  - ai-tools
description:
  CodexBar brings comprehensive AI service monitoring to your macOS menu bar with a clean UI that's accessible anywhere, anytime—no terminal required.
timezone: "America/New_York"
---

While terminal-based monitoring tools like [Claude HUD](/posts/claude-hud-usage-monitoring) are excellent for active coding sessions, sometimes you need visibility into your AI service usage even when you're not in the terminal. Maybe you're in your browser, reviewing documentation, or in Slack coordinating with your team. In these moments, checking your AI quota shouldn't require opening a specific application.

That's where **CodexBar** excels.

## Table of contents

## What is CodexBar?

[CodexBar](https://github.com/steipete/CodexBar) is a macOS menu bar application that monitors usage quotas for multiple AI coding assistants. Created by [Peter Steinberger](https://github.com/steipete) and released under the MIT license, it provides persistent, at-a-glance visibility into your AI service consumption—from anywhere on your Mac.

The core philosophy is simple: your menu bar is always visible, so your usage stats should be too.

## Why I Love It: Clean UI and Universal Access

I've been running CodexBar for several weeks now with three providers configured: **Claude Code, GitHub Copilot, and Gemini**. Here's why it's become an essential part of my setup:

### 1. Always Visible, Never Intrusive

The menu bar placement is genius. Whether I'm coding in the terminal, writing in Notion, or debugging in Chrome DevTools, my usage stats are right there in the corner of my screen. No application switching, no terminal dependency—just persistent awareness.

The icon itself uses a minimalist two-bar design:
- **Top bar**: Represents your 5-hour session window (or credits when weekly limits are exhausted)
- **Bottom bar**: Shows weekly usage as a thin line

At a glance, you can assess both your short-term and long-term quota status.

### 2. Clean, Polished UI

When you click the menu bar icon, you get a beautifully designed dropdown showing detailed stats for each configured provider. The interface is clean, modern, and information-dense without feeling cluttered.

Each provider shows:
- Session usage percentage with visual progress bar
- Weekly usage percentage with progress bar
- Countdown timers for when limits reset
- Current status (active, approaching limit, etc.)

It's the kind of UI that feels like a native macOS application—because it is one.

### 3. Multi-Provider Support is a Game Changer

This is where CodexBar really shines. Instead of maintaining separate dashboards for different AI services, I have a unified view of:

**Claude Code**: My primary AI coding assistant
- Session and weekly limits
- Rate limit consumption
- Context window awareness (when combined with Claude HUD in terminal)

**GitHub Copilot**: For quick autocompletions and suggestions
- Subscription status
- Usage metrics
- Service health

**Gemini**: For experimental features and comparison testing
- API quota tracking
- Cost monitoring
- Weekly usage trends

Having all three in one place means I can make informed decisions about which service to use for different tasks based on current availability.

### 4. No Terminal Dependency

Here's a subtle but important advantage: CodexBar runs independently of your terminal sessions. Even if I'm not actively coding, I can check my usage stats. This is particularly useful for:

- **Morning planning**: Check quota availability before starting work
- **Budget management**: Monitor usage patterns throughout the day
- **Service selection**: Choose which AI service to use based on remaining quota

With terminal-based tools, you need an active coding session to see stats. CodexBar is always running, always accessible.

## Supported Services (It's Extensive)

CodexBar supports an impressive range of AI coding services:

- **Claude Code**: Anthropic's coding assistant
- **OpenAI Codex**: The original AI code completion
- **GitHub Copilot**: Microsoft's AI pair programmer
- **Cursor**: The AI-first code editor
- **Gemini**: Google's multimodal AI
- **Antigravity**: Next-gen development tools
- **Droid (Factory)**: Specialized coding agents
- **z.ai**: Email and scheduling automation
- **Kimi & Kimi K2**: Chinese AI services
- **Kiro**: AI research assistant
- **Vertex AI**: Google Cloud's AI platform
- **Augment**: Code intelligence platform
- **Amp**: Developer productivity tools
- **JetBrains AI**: IDE-integrated assistance

You can enable or disable each provider individually, so you only see stats for services you actually use.

## Installation is Simple

### Via Homebrew (Recommended)

```bash
brew install --cask steipete/tap/codexbar
```

### Direct Download

Alternatively, download the latest release directly from [GitHub](https://github.com/steipete/CodexBar/releases).

**Requirements**: macOS 14+ (Sonoma)

After installation, launch CodexBar and configure which providers you want to monitor. The app will guide you through authentication for each service.

## Setup: My Three-Provider Configuration

Here's how I set up my current configuration:

### 1. Claude Code

CodexBar can read Claude usage data either through:
- OAuth credentials (automatic with Claude login)
- Browser cookies (opt-in)
- Local session data from Claude CLI

I use OAuth authentication, which works seamlessly and updates in real-time.

### 2. GitHub Copilot

Copilot integration reads subscription status from your GitHub CLI authentication. If you're already using Copilot in VS Code or other IDEs, CodexBar picks up your credentials automatically.

### 3. Gemini

For Gemini, I configured API key authentication. CodexBar tracks:
- API quota consumption
- Cost estimates (for paid tiers)
- Request rate limits

## Key Features Beyond Basic Monitoring

### Cost Analysis

For services like Codex and Claude on metered API plans, CodexBar provides local cost analysis with 30-day lookback. You can run:

```bash
codexbar cost --provider claude
```

This shows your usage trends and estimated costs, which is invaluable for budget planning.

### Provider Status Monitoring

CodexBar checks service status endpoints and displays incident badges if a provider is experiencing issues. This has saved me debugging time on several occasions—when Claude isn't responding as expected, a quick glance shows whether it's a service-wide issue.

### Merge Icons Mode

If you're running multiple providers and want to minimize menu bar clutter, CodexBar offers a "merge icons" mode that combines all providers into a single status item. Click to expand details.

### CLI Integration

The bundled `codexbar` CLI tool enables scripting and CI integration:

```bash
# Check usage in scripts
codexbar cost --provider codex

# Monitor quota before intensive operations
if [ $(codexbar quota --provider claude) -gt 80 ]; then
  echo "High usage, waiting..."
fi
```

This programmatic access opens up automation possibilities.

### Customizable Refresh Intervals

You can configure how often CodexBar polls for updates:
- Manual (on-demand only)
- 1 minute
- 2 minutes
- 5 minutes
- 15 minutes

I use 2-minute intervals—responsive enough for real-time awareness without hammering API endpoints.

## Privacy and Security: Local-First

CodexBar takes a privacy-conscious approach:

- **Local parsing by default**: All data processing happens on your device
- **No disk scanning**: The app only reads explicitly configured credential files
- **Optional browser cookies**: Opt-in feature, not required
- **No password storage**: Uses existing OAuth tokens and API keys
- **Open source**: Full code transparency on GitHub

Your usage data never leaves your machine unless you explicitly configure external integrations.

## CodexBar vs. Claude HUD: Complementary Tools

As I covered in my [Claude HUD review](/posts/claude-hud-usage-monitoring), these tools serve different but complementary purposes:

### Use Claude HUD (Terminal) When:
- You're actively coding in Claude Code
- You want agent and tool activity tracking
- You need real-time context window monitoring
- You prefer terminal-integrated workflows

### Use CodexBar (Menu Bar) When:
- You want always-visible stats across all applications
- You monitor multiple AI services
- Weekly quota tracking is important
- You need access outside terminal sessions

### Use Both Together:
This is my current setup. During active coding:
- **Claude HUD** shows detailed session metrics in my terminal
- **CodexBar** provides weekly quota awareness and multi-service visibility

When I'm not coding but planning work or in meetings, CodexBar ensures I'm never surprised by quota exhaustion.

## Real-World Usage Patterns

Here's how CodexBar has changed my workflow:

### Morning Routine
Before starting work, I check CodexBar to see my weekly quota status across all services. If Claude is at 70% weekly usage, I might plan to use Copilot more for simple completions and save Claude for complex reasoning tasks.

### Service Selection
When choosing which AI service to use for a task:
- **High usage needed**: Choose the service with the most remaining quota
- **Simple completions**: Use Copilot or Gemini to preserve Claude quota
- **Complex reasoning**: Use Claude if available

### Budget Awareness
The cost analysis feature helps me understand actual usage patterns. I discovered I was burning through Claude quota on repetitive tasks that Copilot could handle—adjusting this saved ~30% weekly usage.

### Incident Detection
Twice, CodexBar alerted me to Claude service degradation before I hit errors. Instead of debugging, I switched to Gemini temporarily, saving time and frustration.

## Who Should Use CodexBar?

**Ideal for:**
- **Multi-service users**: You use Claude + Copilot + Gemini or other combinations
- **macOS developers**: The menu bar integration is mac-only (though CLI works on Linux)
- **Budget-conscious users**: You monitor costs on metered API plans
- **Always-visible preference**: You want persistent quota awareness

**Maybe skip if:**
- You exclusively use Claude Code and prefer terminal tools (stick with Claude HUD)
- You're not on macOS and don't need the GUI
- You rarely hit quota limits and don't track usage

## Conclusion

CodexBar delivers on its promise: comprehensive, always-visible AI service monitoring with a clean, native macOS UI. The multi-provider support, weekly quota tracking, and universal accessibility make it indispensable for developers juggling multiple AI coding services.

**Why I recommend it:**

1. **Polished UI**: Feels like a native macOS app (because it is)
2. **Always accessible**: No terminal dependency
3. **Multi-service support**: Unified dashboard for all your AI tools
4. **Privacy-conscious**: Local-first data processing
5. **Open source**: Full transparency and community contributions

My three-provider setup (Claude, Copilot, Gemini) has transformed how I manage AI service usage. Instead of reactive quota management ("Oops, I hit the limit"), I practice proactive resource allocation ("I'll save Claude for this complex refactoring").

If you're on macOS and use any AI coding services, install CodexBar. The Homebrew installation takes 30 seconds, configuration is straightforward, and the persistent visibility is genuinely valuable.

Your menu bar has room for one more icon—make it count.

## Resources

- **CodexBar GitHub**: [steipete/CodexBar](https://github.com/steipete/CodexBar)
- **Official Site**: [codexbar.app](https://codexbar.app/)
- **Homebrew Installation**: `brew install --cask steipete/tap/codexbar`
- **Related Tools**:
  - [Claude HUD](/posts/claude-hud-usage-monitoring) - Terminal-based monitoring
  - [oh-my-claudecode](/posts/oh-my-claudecode-orchestration) - Multi-agent orchestration
- **Alternative**: [SessionWatcher](https://www.sessionwatcher.com/)

---

**Sources:**

- [GitHub - steipete/CodexBar](https://github.com/steipete/CodexBar)
- [CodexBar - Mac Menubar Apps](https://macmenubar.app/app/codex-bar)
- [CodexBar Official Site](https://codexbar.app/)
- [CodexBar on On My Menubar](https://onmymenubar.app/codexbar/)
- [SessionWatcher - Monitor Claude Code & Codex](https://www.sessionwatcher.com/)
- [CodexBar: macOS Menu Bar Usage Stats](https://huntscreens.com/en/products/codexbar)
