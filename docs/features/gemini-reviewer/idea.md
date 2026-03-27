---
id: gemini-reviewer
name: Gemini Reviewer Extension
type: Feature
priority: P1
effort: Medium
impact: High
created: 2026-03-27
---

# Gemini Reviewer Extension

## Problem Statement
The current feature-workflow relies heavily on Claude for implementation, planning, and review. This can lead to blind spots where the same model that implemented a feature also reviews it, or the reviews follow a single perspective.

## Proposed Solution
Add a "Gemini Reviewer" to the process. This reviewer will:
1. Provide a "second opinion" with a critical eye.
2. Focus on architectural edge cases, security, and maintainability.
3. Be strictly read-only for implementation files.
4. Write reviews to a separate `gemini-reviews/` directory to avoid interfering with Claude's workflow.

## Affected Areas
- gemini-cli skills
- documentation/reviews
