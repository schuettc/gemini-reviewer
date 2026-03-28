# Feature Reviewer: The "Second Opinion" Skill

A specialized Gemini CLI skill designed to provide a critical, senior-architectural perspective on feature plans and implementations.

## Installation (Shell Command)

To use this skill globally, run the following command in your **Terminal (not inside Gemini CLI)**:

```bash
gemini skills install https://github.com/schuettc/gemini-reviewer.git
```

## How to Use (Inside Gemini Session)

Once installed, start a Gemini session and activate the skill:

```bash
# Inside your Gemini CLI session
activate_skill feature-reviewer
```

### Supported Workflow
The reviewer is pre-configured to understand the "feature-driven" workflow structure:
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
