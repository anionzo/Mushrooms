# Product Docs

This directory is intentionally generic and mostly empty in Harness v0.

When a user provides a project spec, derive smaller product contract files here
instead of keeping one large spec as the living plan. Name files by the product
domains that actually exist in that spec, for example `overview.md`,
`billing.md`, `workflows.md`, `permissions.md`, or `api-conventions.md`.

Do not create domain files before the spec just to fill the folder. Empty
structure is healthier than fake product truth.

## Current Product Contracts

- `DESKTOP_GARDEN_VISION.md` - Vision **Desktop Garden** (ecosystem, moisture, moon, 250+ nấm theo tier, map 25 module, không clone Nook).

- `GDD_OUTLINE.md` - Khung GDD 300–500 trang (7 volume); Part I–III viết sẵn, IV–X mục lục.

- `GAME_MASTER_PLAN.md` - **Kế hoạch đầy đủ** (~72 story, AC, ma trận feature, rủi ro, lịch, D1–D10) — **đọc trước khi code**.

- `GAME_DEVELOPMENT_PLAN.md` - Tóm tắt một trang + link master plan.

- `UNITY_SETUP.md` - Cài Unity Hub / Unity 6 LTS trên Windows 11.

- `DESKTOP_IDLE_SIM_ARCHITECTURE.md` - Full system architecture (20 sections) for
  the Windows 11 / Unity 6 LTS desktop idle mushroom ecosystem simulation:
  vision, requirements, layers, folder/asmdef layout, gameplay systems, data,
  Win32 desktop integration, save/events/state machines, UI, performance, roadmap,
  standards, testing, deployment, and future expansion. **Architecture only; no
  gameplay implementation.**

- `symphony-web-ui-controller.md` - Local Web UI controller for Harness Symphony
  task execution, review, dependency blocking, Codex event logs, PR review, and
  sync.

## Update Rule

When behavior changes:

1. Update the affected product doc.
2. Update or create the story packet.
3. Update durable proof status with `scripts/bin/harness-cli story add` or
   `scripts/bin/harness-cli story update`.
4. Record a decision if the change affects architecture, scope, risk, or a
   previously settled product rule.
