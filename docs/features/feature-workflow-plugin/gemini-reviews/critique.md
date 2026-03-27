# Gemini Review Critique: Feature Workflow Plugin

**Date:** 2026-03-27
**Reviewer:** Gemini CLI (Senior Architect & Security Engineer)
**Verdict:** CONDITIONAL PASS

## Overview
The `feature-workflow-plugin` is a sophisticated lifecycle management tool that brings much-needed structure to agentic development. The use of event-driven hooks (`PreToolUse`, `PostToolUse`) to inject context and manage state is a robust pattern. However, as an architect, I identify several areas where the system could be more resilient and flexible.

## Critical Findings (Blocking for "High-Scale" Readiness)

### 1. Hardcoded Path Dependencies
**Risk:** The plugin is tightly coupled to the `docs/features/` directory structure. If a project uses a different documentation pattern (e.g., `features/` in the root, or `internal/docs/features/`), the hooks will fail to fire or regenerate the dashboard.
**Recommendation:** Implement a configuration mechanism (e.g., a `.feature-workflow.json` or an environment variable `FEATURE_WORKFLOW_DOCS_ROOT`) to allow users to define their own feature storage location.

### 2. Hook Performance and Concurrency
**Risk:** The `PostToolUse` hook spawns a Python subprocess to regenerate the `DASHBOARD.md` on every write to a feature file. While it has a timeout, in a high-activity session (e.g., Claude making multiple surgical edits), this could lead to a "thundering herd" of dashboard generation processes, consuming system resources and potentially leading to race conditions if two processes try to write `DASHBOARD.md` simultaneously.
**Recommendation:** Implement a lock file mechanism or a debounced background worker for dashboard regeneration. Alternatively, verify if the dashboard generation can be made more lightweight (e.g., by only updating the specific row for the changed feature).

## Warning & Suggestions (Non-Blocking)

### 3. Brittle Parsing in Hooks
**Risk:** The `post_tool_use.py` hook parses review verdicts by manually splitting lines and checking prefixes (`verdict:`, `phase:`). This is prone to failure if the markdown formatting changes slightly (e.g., leading spaces or different casing).
**Recommendation:** Use the existing frontmatter parsing logic from `skills/shared/lib/` within the hooks. Since hooks are Python scripts, they should leverage shared libraries for consistency.

### 4. Reviewer Mode State Management
**Risk:** The `~/.claude/reviewer-mode` marker file used to toggle reviewer permissions is a global state that could easily become stale if a session crashes or a user forgets to clear it.
**Recommendation:** Consider using session-specific marker files (e.g., `~/.claude/sessions/<session-id>.reviewer`) to ensure that reviewer mode doesn't leak between different terminal windows or projects.

## Different Perspective: The "Agentic Edge"
Claude (the primary user of this plugin) is excellent at following instructions, but it can be "over-eager" to satisfy requirements. The `PreToolUse` hook's current implementation is a "hard" block, which is good. However, there is no "soft" guardrail for **Scope Creep** within the `plan.md` itself.
**Insight:** A future enhancement should include a "Scope Guardian" that analyzes the `plan.md` against the `idea.md` during the implementation phase to flag when the plan starts to diverge significantly from the original problem statement.

## Conclusion
The architecture is sound for local development, but it requires more robust configuration and concurrency management to be truly "production-grade" for large-scale enterprise use.
