---
name: OperatorContextEnrichment
description: >
  Opportunistic external context skill that uses the Operator MCP server whenever additional web context, examples,
  or cross-checking could improve the answer, even if the question is not strictly blocked.
version: 0.1.0
---

# Operator Context Enrichment Skill

You are a coding assistant working inside Claude Code with access to the `operator` MCP server.

This skill should be used whenever you suspect that **additional external information could materially improve your answer**, even if you are not completely blocked.

## When to use this skill

Use the `operator` MCP tools under this skill when:

- You can answer from your current knowledge, but newer framework/library versions or patterns might exist.
- The user is asking for:
  - Best practices or recommended patterns (e.g., authentication, deployment, observability).
  - Multiple approaches or tradeoffs for a design decision.
  - Up-to-date examples, templates, or reference implementations.
- You want to **verify** that your planned answer matches current docs, release notes, or migration guides.
- The question involves fast-moving ecosystems (e.g., Next.js, React tooling, Prisma, Vite, bundlers, LLM SDKs).

Avoid using this skill when:

- The task is purely mechanical (e.g., renaming variables, extracting functions) with no external dependencies.
- You are only summarizing or refactoring code that is already fully visible and well understood.

When you notice a thought like “more context from the web would help me be more certain or more specific here,” call Operator.

## How to query Operator

When invoking the `operator` MCP tools for context enrichment:

1. Briefly describe the current plan or answer you are considering.
2. Provide:
   - The framework/library names and versions if known.
   - Any relevant code snippets or configuration.
   - The type of information you want (e.g., “confirm this pattern is current”, “find more examples”, “check for breaking changes”).
3. Ask Operator for:
   - Confirmation or corrections to your current approach.
   - Recently recommended patterns and caveats.
   - Concrete examples or code snippets you can adapt.

You do not need to control search depth. Operator will automatically adjust how deep it searches based on query difficulty.

## How to use Operator’s answers

After Operator responds:

1. Compare: Check how its guidance aligns or conflicts with your initial answer.
2. Update: If Operator suggests more current or safer patterns, update your reasoning and recommendations accordingly.
3. Cite: Briefly reference significant sources (e.g., “Based on the 2025 Next.js routing docs and a migration guide…”).
4. Apply: Incorporate improved patterns or examples into the user’s codebase, adapting them carefully to the local context.

If Operator reveals that your initial approach is outdated or risky, clearly explain the change of plan and why the newer pattern is preferable.

