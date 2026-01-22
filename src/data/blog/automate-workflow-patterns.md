---
title: "Automate Your Workflow: Mining Claude Code History for Custom Commands"
author: atooooomic
pubDatetime: 2026-01-22T00:00:00Z
slug: automate-workflow-patterns
featured: true
draft: false
tags:
  - claude-code
  - workflow
  - automation
  - productivity
  - data-analysis
description:
  Discover how to analyze your Claude Code usage patterns from history.jsonl to identify repetitive tasks and create custom commands or skills that supercharge your workflow.
timezone: "America/New_York"
---

Ever wonder if you're repeating the same types of prompts over and over in Claude Code? What if you could **analyze your actual usage patterns** and automatically generate custom commands or skills tailored to your workflow?

Turns out, you can. And it's hiding in plain sight in your `history.jsonl` file.

## Table of contents

## The Hidden Goldmine: history.jsonl

Every prompt you've ever typed into Claude Code is stored in a file called `history.jsonl`. This isn't just a backup—it's a **comprehensive record of your development patterns**, complete with:

- Every prompt you've written
- All commands you've executed
- The context and outcomes of each interaction
- Timestamps showing when you work and what you work on

On Linux/Mac, you'll typically find it at:
```bash
~/.local/share/claude-code/history.jsonl
```

On Windows:
```bash
%APPDATA%\claude-code\history.jsonl
```

This file is a treasure trove of data about how you actually use AI in your development workflow—not how you think you use it, but the reality of your day-to-day patterns.

## Why Analyze Your Usage Patterns?

Analyzing your Claude Code history helps you identify repetitive tasks worth automating, understand workflow bottlenecks, and create personalized commands that match how you actually work. It's data-driven workflow optimization—using real patterns from your interactions instead of guessing what might help.

## The Analysis Process

Here's the beautiful part: you can use Claude Code itself to analyze your Claude Code usage. Meta, right?

The prompt is elegantly simple:

```
@history.jsonl analyze the prompts I've written (excluding simple commands
like /exit, /clear, etc.) and cluster them by purpose. Then suggest
custom commands or skills that could automate these patterns.
```

When you run this, Claude will:

1. **Parse your history file** to extract actual prompts (filtering out system commands)
2. **Cluster similar prompts** by intent and purpose
3. **Calculate statistics** on your most common task types
4. **Suggest automation opportunities** based on the patterns it finds

## What You'll Discover

When you run this analysis, you'll typically see patterns emerge across categories like:

- **UI/Component Work** - Repetitive component creation, styling patterns, layout fixes
- **Code Modification/Refactoring** - Similar restructuring tasks, code quality improvements
- **Debugging/Root Cause Analysis** - Error investigation, build failures, runtime issues
- **Feature Implementation** - API integrations, database operations, new functionality
- **Documentation** - README files, code comments, API docs
- **Testing** - Unit tests, integration tests, test debugging
- **Configuration** - Build tools, environment setup, deployment configs
- **Research/Exploration** - Library comparisons, best practices, architecture decisions

The key is identifying which categories dominate your workflow. These are your prime automation candidates.

## Turning Insights into Automation

Once you have your usage patterns, the next step is creating custom commands or skills. Here are some examples based on common patterns:

### Example 1: Component Generator

If you find yourself frequently creating similar React components:

```bash
# Custom skill: /generate-component
Creates a new React component with:
- TypeScript types
- Tailwind styling
- Props interface
- Export statement
```

### Example 2: Debug Analyzer

For frequent debugging sessions:

```bash
# Custom skill: /debug-deep-dive
Automatically:
- Checks recent error logs
- Analyzes stack traces
- Suggests likely causes
- Proposes fixes with context
```

### Example 3: Refactor Assistant

For code quality improvements:

```bash
# Custom skill: /smart-refactor
Identifies and applies:
- Duplicate code extraction
- Type safety improvements
- Performance optimizations
- Best practice patterns
```

## How to Create Custom Commands

Claude Code supports custom commands through the plugin system. Here's the general approach:

1. **Identify the pattern** from your analysis
2. **Define the command interface** (what inputs it needs)
3. **Write the skill definition** (what Claude should do)
4. **Test and refine** based on actual usage

You can create skills using the `.claudecode/skills/` directory in your project, or as part of a plugin if you want to share them.

## When This Works Best

This analysis is most valuable when you've been using Claude Code regularly for a while and notice yourself repeating similar prompts. If you just started or have highly variable tasks, you might not have enough data for meaningful patterns yet.

Beyond automation, you'll learn about your actual development habits—discovering you spend more time debugging than expected, or that testing prompts are surprisingly rare. This self-awareness helps you improve your workflow regardless of automation.

## Getting Started

Ready to analyze your own patterns?

1. Locate your `history.jsonl` file
2. Run the analysis using the prompt template above
3. Review the clusters and identify automation opportunities
4. Create one or two custom commands based on your top patterns
5. Iterate and refine based on actual usage

## Conclusion

Your `history.jsonl` file is more than a log—it's a mirror reflecting your actual development patterns. If you've been using Claude Code for a while, you definitely have patterns worth automating. The question is: are you ready to discover what they are?

Start with the analysis prompt above. You might be surprised by what your own history reveals.

## Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Claude Code plugin system](https://github.com/anthropics/claude-code/blob/main/docs/plugins.md)

---

*Have you analyzed your Claude Code history? What patterns did you discover? I'd love to hear about your findings and what automation you've created!*
