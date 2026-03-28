# Installing and Using the Gemini Reviewer

This repository contains a specialized Gemini CLI skill designed to act as a "second opinion" reviewer for feature-driven development workflows.

## Installation (Run in your Terminal)

**IMPORTANT:** The following commands must be executed in your **shell (zsh, bash, etc.)**, not inside an active Gemini session.

### 1. Global Installation (Recommended)
To make the Gemini Reviewer available across **all** your projects, install it to your user tier:

```bash
# From your terminal, run:
gemini skills install https://github.com/schuettc/gemini-reviewer.git
```

### 2. Project-Specific Installation
If you prefer to keep it within a specific project, clone the repo and copy the `SKILL.md` to your project's `.gemini/skills/` directory:

```bash
# From your terminal, run:
mkdir -p .gemini/skills/gemini-reviewer/
cp /path/to/gemini-reviewer/SKILL.md .gemini/skills/gemini-reviewer/
```

---

## How to Use (Inside Gemini CLI)

Once the skill is installed, start a Gemini session and use the internal `activate_skill` tool:

1.  **Activate the Skill:**
    ```
    activate_skill gemini-reviewer
    ```

2.  **Run a Review:**
    Ask Gemini to perform a review based on the current context:
    - "Review the current feature plan for 'auth-system'."
    - "Provide a critical perspective on the implementation in `src/api.ts`."

    **Pro Tip:** You can also define a custom `/feature-review` command for this. See `GEMINI.md` for instructions.

## How it Works
The Gemini Reviewer is a **Read-Only** agent. It follows a strict SOP defined in its `SKILL.md`:
1.  **Research:** It reads the `docs/features/` directory to understand the context.
2.  **Analyze:** It evaluates code changes against the plan.
3.  **Critique:** It writes a detailed markdown report to `docs/features/<id>/gemini-reviews/critique.md`.

**Note:** It will never modify your source code. It only writes to its designated review directory.
