# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

**mcpserver-security-orchestrator** is the **intelligent front door** to the MCP Security ecosystem. It is not another analysis tool — it's the *coordinator* that helps users figure out what they need, routes them to the right tool/workflow, adapts the depth of teaching to the user, and fuses the outputs of many tools. Think "entry point + router + tutor" over the family of sibling repos (finder, audit, builder, operator).

Like its siblings, it is a **prompt-driven knowledge system** (Markdown, no application code). The operative artifact is `prompts/main-prompt.md` — the orchestrator persona a user loads to begin.

## Architecture — the key concepts

Understanding these four ideas is essential before editing content here:

- **Progressive disclosure**: The system deliberately loads *only what the user needs, when they need it*, rather than presenting everything at once. `prompts/main-prompt.md` is the thin entry point; deeper material is pulled in on demand. See `PROGRESSIVE-DISCLOSURE.md` (the rationale) and `PROMPT-STRATEGY.md` (the architecture).
- **4-Level Deployment Context**: Security priorities and tool selection scale with where the server runs — (1) Local, (2) Remote Single-User, (3) Remote Multi-User, (4) Enterprise Multi-User. Recommendations should always be calibrated to the user's level.
- **AI-native / loose coupling**: No rigid output standardization. Tools "do their own thing" and the AI makes sense of / fuses differing outputs (Markdown + YAML frontmatter *encouraged*, not required). See `DATA-HANDLING.md`.
- **Open, tool-agnostic ecosystem**: Prefer the best tool for the job regardless of origin — internal siblings *or* third-party tools — with graceful fallbacks when a tool is unavailable. See `TOOL-ECOSYSTEM.md` and `TOOL-DISCOVERY.md`.

## Layout

```
prompts/main-prompt.md   # The orchestrator persona — the entry point users load
resources/
  REGISTRY-TOOLS.md      # Catalog of tools the orchestrator can route to
  REGISTRY-WORKFLOWS.md  # Catalog of workflows/journeys
```

### Design & strategy docs (top level)
These define how the orchestrator is meant to behave — read the relevant one before changing related behavior:
- **ORCHESTRATION-PATTERNS.md** — workflow templates and decision trees for routing
- **EDUCATIONAL-ORCHESTRATION.md** — coordinating learning experiences across tools
- **PROMPT-STRATEGY.md** / **PROGRESSIVE-DISCLOSURE.md** — the prompt/disclosure architecture and why it was chosen over monolithic automation
- **TOOL-DISCOVERY.md** / **TOOL-ECOSYSTEM.md** — finding/evaluating new tools; goals→tools mapping
- **DATA-HANDLING.md** — data integration/fusion across diverse tool outputs
- **IDEAS.md** — backlog of improvement ideas; **PROGRESS.md** — running log of this AI-native orchestration experiment

There is **no build/test/lint system** — this is a documentation/prompt system. Quality is measured by how well the orchestrator routes users and adapts teaching, not by tests.

## Ecosystem role

Coordinates the **ModelContextProtocol-Security** siblings it routes between:
`mcpserver-finder` (discover) → `mcpserver-audit` (find vulns) → `mcpserver-builder` (build/fix) → `mcpserver-operator` (operate) → `mcpserver-hosting`, backed by the `audit-db` / `vulnerability-db` data repos. Keep terminology and the expert-tutor voice consistent with these.

## Contributing

`main` is protected and requires a code-owner-approved pull request. Contributions are prompt/documentation improvements; keep changes consistent with the progressive-disclosure design (don't front-load everything into the main prompt).
