---
name: design-selfcheck
description: Review a design systematically before handoff, using the included checklist to find requirement gaps, interaction issues, layout problems, and delivery risks.
---

# Design Selfcheck

Use this skill when the user shares a Figma link, screenshots, PRD context, or asks for a structured design review.

## Inputs

Collect as many of these as available:
- Figma link or screenshots
- PRD link, document, or requirement summary
- Target users and main tasks
- Known constraints or edge cases

## Workflow

1. **Resolve the PRD first.** Before reviewing the design, make sure you actually understand the requirements.
   - If the user provides a **Confluence link** (contains `/pages/`, `pageId=`, `/display/`, or matches the internal Confluence host), load the `confluence-search` skill at `~/.codex/skills/confluence-search/SKILL.md` and use it to fetch the page content by ID.
   - If the user provides raw PRD text or screenshots, work with that directly.
   - If no PRD is provided but the design clearly implies one, ask the user for it once before continuing.
2. **Extract PRD essentials** into a short internal summary you will reuse during the review:
   - business goal and target user
   - core user tasks / main flow
   - explicit functional requirements
   - stated edge cases, constraints, non-goals
   - open questions or ambiguities in the PRD itself
3. Read the checklist index at `reference/checklist/README.md`.
4. Pull in only the checklist files relevant to the current review.
5. Review the design in phases:
   - requirements coverage (compare design ↔ PRD summary from step 2)
   - framework and layout
   - interaction and edge cases
   - visual detail
   - delivery readiness
6. Output prioritized findings.

## PRD Link Handling (Confluence)

When the PRD is a Confluence URL:

1. Extract the page ID from the URL:
   - `pageId=123456` → `123456`
   - `/pages/123456/...` → `123456`
   - For `/display/SPACE/Title` style URLs, fall back to a title-based CQL search via `confluence-search`.
2. Invoke the `confluence-search` workflow to fetch the page body (prefer fetching by ID directly over searching when the ID is known).
3. If the page body comes back empty (Confluence Macro page), ask the user to paste the key sections or provide a child page.
4. Do not dump the full PRD back to the user — summarize it into the PRD essentials above and proceed with the review.

## Output Format

- PRD summary (2–5 bullets, only if a PRD was resolved)
- Severe issues
- Normal issues
- Optimization suggestions
- Open questions

## Rules

- Always ground findings in the PRD when one exists; explicitly flag gaps between design and PRD.
- Be direct about missing states, hidden complexity, and delivery risk.
- Tie findings back to user goals and flows, not only visual polish.
- Prefer concrete fixes over vague design opinions.
- Never perform writes against Confluence; read-only access only.
