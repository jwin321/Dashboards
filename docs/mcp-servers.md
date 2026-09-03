# Recommended MCP Servers

These MCP servers support building and maintaining the ET Operations
Dashboard platform. Enable them for this repository via **Repository
Settings → Copilot → Coding agent → MCP configuration** (server availability
and setup steps depend on your GitHub plan/environment).

| Server | Priority | Why it helps this project |
|---|---|---|
| **GitHub** | 10/10 | Repository structure analysis, branch/PR management, issue tracking, backlog maintenance, and searching prior architecture decisions. |
| **Context7** | 10/10 | Pulls current documentation for the frontend/data stack (e.g., React, Next.js, Tailwind, charting/grid libraries, TypeScript, Node, database SDKs) instead of relying on possibly outdated model knowledge. |
| **Playwright** | 9/10 | Automated UI verification and regression testing — essential once the platform grows to dozens of control-room screens. |
| **Chrome DevTools** | 9/10 | Layout, performance, responsiveness, and CSS validation while building operator/executive-facing pages. |
| **Serena** (or equivalent code-intelligence server) | 8.5/10 | Symbol/reference navigation and safe refactoring across a large, multi-facility codebase. |
| **MarkItDown** (or equivalent document-conversion server) | 8/10 | Converting P&IDs, control-room screenshots, and spreadsheets into text/markdown the agent can reason about. |
| **Netdata** (or equivalent monitoring server) | 5/10 | Only needed once dashboard servers/databases are actually hosted and require live monitoring. |

## Notes

- Prioritize servers that reduce trial-and-error (GitHub, Context7) before
  servers that add convenience (DevTools, Playwright, Serena).
- Only add monitoring/infrastructure servers (e.g., Netdata) once there is
  infrastructure to monitor — avoid installing tooling ahead of need.
- Keep this list current as new servers become available or requirements
  change; treat it as part of routine dependency/tooling maintenance
  (see Priority 1 in `docs/master-plan.md`).
