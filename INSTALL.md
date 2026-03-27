# Installing and Using the Gemini Reviewer

This repository contains a specialized Gemini CLI skill designed to act as a "second opinion" reviewer for feature-driven development workflows (specifically compatible with `schuettc/claude-code-plugins`).

## How to Import/Install

### 1. Global Installation (Recommended)
To make the Gemini Reviewer available across **all** your projects, install it to your user tier:

```bash
# From this repository's root
gemini skills install .

# Or from GitHub (once you publish)
gemini skills install https://github.com/schuettc/gemini-reviewer.git
```

### 2. Project-Specific Installation
To use it only within a specific project, copy the `skills/gemini-reviewer` directory to your project's `.gemini/skills/` folder:

```bash
mkdir -p .gemini/skills/
cp -r /path/to/gemini-reviewer/skills/gemini-reviewer .gemini/skills/
```

## How to Use

1.  **Activate the Skill:** In any Gemini CLI session, run:
    ```
    activate_skill gemini-reviewer
    ```

2.  **Run a Review:** Once activated, you can ask Gemini to perform a review. For example:
    - "Review the current feature plan for 'auth-system'."
    - "Provide a critical perspective on the implementation in `src/api.ts`."

## How it Works
The Gemini Reviewer is a **Read-Only** agent. It follows a strict SOP defined in its `SKILL.md`:
1.  **Research:** It reads the `docs/features/` directory to understand the context.
2.  **Analyze:** It evaluates code changes against the plan.
3.  **Critique:** It writes a detailed markdown report to `docs/features/<id>/gemini-reviews/critique.md`.

**Note:** It will never modify your source code. It only writes to its designated review directory.
