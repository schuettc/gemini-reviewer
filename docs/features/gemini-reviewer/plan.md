---
started: 2026-03-27
---

# Implementation Plan: Gemini Reviewer Extension

## Overview
Add a specialized Gemini-based reviewer skill to provide a "second perspective" in the feature development workflow.

## Implementation Steps
- [x] Create `.gemini/skills/gemini-reviewer/SKILL.md` with persona and mandates
- [x] Establish `docs/features/<id>/gemini-reviews/` as the standard output directory
- [ ] Create a `GEMINI.md` in the root of the project to formalize the reviewer's instructions and context
- [ ] Provide an initial review of the `feature-workflow` itself to demonstrate the perspective

## Testing Strategy
- [ ] Verify that the `gemini-reviewer` skill can be activated
- [ ] Ensure that reviews are written to the correct subdirectory and NOT the standard Claude review location
- [ ] Confirm that no implementation files are modified during the review process

## Progress Log
### 2026-03-27
- Defined the Gemini Reviewer skill and mandates.
- Created the feature idea and implementation plan in the `docs/features/` structure.
