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

Before we dive into the how, let's talk about the why. Analyzing your Claude Code history can help you:

1. **Identify repetitive tasks** that could be automated with custom commands
2. **Understand your workflow bottlenecks** and optimize them
3. **Create personalized skills** that match your actual working style
4. **Spot patterns** you didn't realize existed
5. **Build better prompts** based on what actually works for you

Think of it as **data-driven workflow optimization**. Instead of guessing what might help your productivity, you're using real data from hundreds (or thousands) of interactions.

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

## Real Results: My Usage Analysis

I ran this analysis on my own history using the **scientist agent** from [oh-my-claudecode](/posts/oh-my-claudecode-orchestration). Here's what I discovered from **905 prompts**:

### My Usage Breakdown

- **UI/Component Work**: 24.8% (225 prompts)
  - Creating React components
  - Styling with Tailwind
  - Responsive design fixes

- **Code Modification/Refactoring**: 18.3% (166 prompts)
  - Restructuring functions
  - Improving code quality
  - Type system improvements

- **Debugging/Root Cause Analysis**: 16.1% (146 prompts)
  - Error investigation
  - Build failures
  - Runtime issues

- **Feature Implementation**: 13.4% (122 prompts)
  - Adding new functionality
  - API integrations
  - Database operations

- **Documentation**: 9.7% (88 prompts)
  - Writing README files
  - Code comments
  - API documentation

- **Testing**: 8.2% (74 prompts)
  - Unit tests
  - Integration tests
  - Test debugging

- **Configuration**: 5.9% (54 prompts)
  - Build tools
  - Environment setup
  - Deployment configs

- **Research/Exploration**: 3.6% (30 prompts)
  - Library comparisons
  - Best practices
  - Architecture decisions

### The Aha Moment

Seeing these numbers was eye-opening. I had no idea that **nearly a quarter of my time** was spent on UI and component work. This insight alone suggested several automation opportunities:

- A custom command for scaffolding common component patterns
- A skill for generating Tailwind-based responsive layouts
- Templates for common UI patterns I kept recreating

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

## Using the Scientist Agent

If you have [oh-my-claudecode](/posts/oh-my-claudecode-orchestration) installed, the **scientist agent** is perfect for this kind of analysis:

```bash
# The scientist agent excels at data analysis
@history.jsonl analyze my usage patterns and provide
detailed statistics with visualization recommendations
```

The scientist agent brings specialized data analysis capabilities:

- Statistical clustering algorithms
- Pattern recognition
- Trend analysis
- Structured output with findings and limitations

## Important Caveat: Token Consumption

Here's the catch: **analyzing your entire history can consume significant tokens**, especially if you've been using Claude Code for a while.

My 905-prompt analysis used approximately **50,000-75,000 tokens** (rough estimate based on context window usage). For larger histories with thousands of prompts, this could easily exceed 100,000 tokens.

### Mitigation Strategies

1. **Sample your history**: Analyze the most recent 500-1000 prompts instead of everything
2. **Filter by date**: Focus on recent months for more relevant patterns
3. **Pre-filter**: Remove obvious noise (very short prompts, system messages) before analysis
4. **Batch analysis**: Break it into chunks by time period or task type

You can pre-filter your history with a simple script:

```bash
# Extract only substantive prompts from recent history
tail -n 1000 ~/.local/share/claude-code/history.jsonl | \
  jq -c 'select(.message.length > 50)' > recent-history.jsonl
```

Then analyze the filtered file:

```
@recent-history.jsonl cluster these prompts by purpose...
```

## When This Analysis Shines

Usage pattern analysis is particularly valuable if you:

- **Have been using Claude Code for months** (more data = better patterns)
- **Work on multiple similar projects** (recurring patterns across projects)
- **Feel like you're repeating yourself** (automation opportunities)
- **Want to optimize your workflow** (data-driven improvements)
- **Build custom tooling** (inform your tool design with real usage data)

## When to Skip It

This analysis might not be worth the token cost if you:

- Just started using Claude Code (insufficient data)
- Have highly variable, one-off tasks (few patterns to detect)
- Are on a tight token budget (the cost might not justify insights)
- Already have highly optimized custom commands (patterns already addressed)

## Beyond Automation: Learning About Yourself

One unexpected benefit of this analysis: **you learn about your development patterns**.

Discovering that 16% of my prompts were debugging-related made me realize I should focus more on preventive measures like better type safety and testing. Seeing that only 8.2% of prompts were testing-related revealed a gap in my workflow.

This kind of self-awareness is valuable even without automation. It helps you consciously improve your development practices.

## Combining with Other Tools

This analysis becomes even more powerful when combined with other Claude Code ecosystem tools:

- **[Superpowers plugin](/posts/claude-code-superpowers-plugin)**: Use insights to inform your brainstorming sessions
- **[oh-my-claudecode](/posts/oh-my-claudecode-orchestration)**: Leverage specialized agents for pattern-specific automation
- **[Claude HUD](/posts/claude-hud-usage-monitoring)**: Monitor which automated commands save the most tokens

The ecosystem works better when you understand your actual usage patterns.

## Getting Started

Ready to analyze your own patterns? Here's your action plan:

1. **Locate your history.jsonl file**
2. **Decide on a sample size** (recent 1000 prompts is a good start)
3. **Run the analysis** using the prompt template above
4. **Review the clusters** and look for automation opportunities
5. **Start simple** - create one or two custom commands based on your top patterns
6. **Iterate** - refine based on actual usage

## The Future: Automatic Pattern Detection

Imagine if Claude Code could automatically analyze your patterns and **suggest custom commands proactively**. "I notice you've created 15 similar React components this month. Would you like me to generate a template?"

The data is already there. The analysis capabilities exist. It's just a matter of building the integration.

## Conclusion

Your `history.jsonl` file is more than a log—it's a mirror reflecting your actual development patterns. By analyzing this data, you can move from guesswork to evidence-based workflow optimization.

Yes, the token cost is real. But for developers serious about productivity, understanding your patterns is an investment that pays dividends in time saved and friction reduced.

The question isn't whether you have patterns worth automating. If you've been using Claude Code for any length of time, you definitely do. The question is: are you ready to discover what they are?

Start with a small analysis. See what you learn. You might be surprised by what your own history reveals.

## Resources

- **Claude Code Documentation**: [Official docs](https://docs.anthropic.com/en/docs/claude-code)
- **oh-my-claudecode**: [Multi-agent orchestration with scientist agent](/posts/oh-my-claudecode-orchestration)
- **Custom Skills Guide**: Check the `.claudecode/skills/` directory documentation
- **Plugin Development**: [Claude Code plugin system](https://github.com/anthropics/claude-code/blob/main/docs/plugins.md)

---

*Have you analyzed your Claude Code history? What patterns did you discover? I'd love to hear about your findings and what automation you've created!*
