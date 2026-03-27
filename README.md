# Gemini Reviewer: The "Second Opinion" Skill

A specialized Gemini CLI skill designed to provide a critical, senior-architectural perspective on feature plans and implementations.

This is NOT a Claude Code plugin. This is a **Gemini CLI Skill** that works alongside your development process to provide an independent "second set of eyes."

## Why Use Gemini Reviewer?
- **Different Perspective:** Claude often implements the feature; Gemini reviews it from a skeptical, architectural, and security-focused viewpoint.
- **Read-Only Safety:** Strictly observes and critiques. It will NEVER modify your source code.
- **Structured Feedback:** Writes detailed, actionable critiques to `docs/features/<id>/gemini-reviews/`.

## Installation

To use this skill in any project, install it globally to your Gemini CLI:

```bash
gemini skills install https://github.com/schuettc/gemini-reviewer.git
```

## How it Works

Once installed, activate the skill in your Gemini session:

```bash
activate_skill gemini-reviewer
```

### Supported Workflow
The reviewer is pre-configured to understand the "feature-driven" workflow structure (compatible with `schuettc/claude-code-plugins`):
1.  **Detects Features:** It reads your `docs/features/` directory to find the context of what you are building.
2.  **Architectural Critique:** It evaluates your `plan.md` and actual code changes.
3.  **Separate Review Storage:** It saves its findings to a dedicated `gemini-reviews/` folder, ensuring it doesn't interfere with your main development files.

## Review Standards
The reviewer follows a senior-level SOP (defined in `GEMINI.md`) focusing on:
- **Edge Case Analysis:** Missed failure modes.
- **Security:** OWASP Top 10 and common pitfalls.
- **Performance:** Identifying non-obvious bottlenecks.
- **Maintainability:** Architectural alignment and project conventions.

## License
MIT
