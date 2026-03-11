# HMSS Draw.io MCP Workflow

## Purpose

This note defines how we will build and refine HMSS diagrams with the draw.io MCP so the repo keeps a stable source of truth and the diagrams stay consistent across phases.

## File Strategy

- Keep text blueprints in `260310-hmss/step-*.md`.
- Keep editable draw.io sources in `260310-hmss/diagrams/`.
- Treat the Markdown blueprint as the business source of truth.
- Treat the `.drawio` file as the visual source of truth.
- When the blueprint changes, update the `.drawio` source in the same turn.

## MCP Workflow

1. Start from the approved HMSS requirement or analysis artifact.
2. Convert that artifact into a compact diagram blueprint before drawing.
3. Create or update the `.drawio` XML manually so layout is deliberate, not auto-generated noise.
4. Open the XML with draw.io MCP for visual review.
5. Refine spacing, routing, labels, and stereotype placement until the diagram is clean enough to export into the report.
6. Keep one diagram per `.drawio` source file unless multiple pages are clearly necessary.

## Layout Rules

- Use a wide canvas and align all vertices to a 10px grid.
- Leave at least 60px between neighboring shapes.
- Put human actors on the left and external systems on the right unless the notation strongly suggests otherwise.
- Use orthogonal connectors for dense diagrams.
- Spread connector entry points along a shape edge instead of stacking every edge into the same point.
- Prefer short business-visible labels over sentence-length edge text.
- Do not show internal decomposition on the context diagram.
- Do not invent `<<include>>` or `<<extend>>` links unless they are explicitly justified by the requirement model.

## HMSS-Specific Rules

- Context diagram: model HMSS as one black-box system only.
- Use case diagram: show 19 use cases, including both `UC-08a Create Property` and `UC-08b Update Property`.
- Keep `Registered User` only as an actor generalization for `Tenant`, `Owner`, and `System Admin`.
- Show `Google Maps`, `Cloud Storage`, and `Email Provider` as external systems, not internal components.
- Keep names identical to the existing HMSS artifacts so the report, blueprints, and diagrams do not drift.

## Review Checklist

- The diagram matches the latest approved HMSS text artifact.
- Actor placement and system boundary are unambiguous.
- Edge routing is readable without overlaps hiding arrowheads or labels.
- Labels stay at analysis level and avoid design detail.
- No duplicate actors, duplicate use cases, or mixed naming variants appear.
