---
name: drawio-communication-diagram
description: Create or update editable draw.io UML communication diagrams from loose raw text, structured markdown blueprints, or existing `.drawio` files. Use when Codex must parse participants, stereotypes, object layout, and numbered messages, then use `mcp__drawio__open_drawio_xml` to build a communication diagram with the built-in UML actor shape, stereotype-labeled object boxes, plain association links, one editable text box per message, and short free-floating directional connectors with a line and arrowhead. Use only for communication diagrams, not other UML diagram types.
---

# Drawio Communication Diagram

Use this skill to turn communication-diagram source text into editable draw.io XML and save it as a `.drawio` file.

## Quick Start

1. Normalize the input with [references/input-contract.md](references/input-contract.md).
2. Stop and ask focused clarification questions when any blocking issue appears. Do not guess.
3. Build or update the diagram in XML with [references/xml-patterns.md](references/xml-patterns.md).
4. Save the XML as a `.drawio` file.
5. Open the XML with `mcp__drawio__open_drawio_xml` for a visual check when that tool is available.

## Supported Inputs

- Use for loose raw text that names participants, their roles or stereotypes, and numbered messages.
- Use for structured markdown blueprints with sections such as `Object Layout`, `Participants`, `Messages`, and `Notes`.
- Use for update requests that include an existing `.drawio` file plus revised source text.

Load [references/example-blueprint.md](references/example-blueprint.md) only when you need a concrete example of the normalized source format.

## Normalize Before Drawing

Require a normalized model with:
- a diagram title or output basename
- participants with unique names
- one classification per participant: actor or software object
- a stereotype for every software object
- numbered messages with unique numbers, source, target, and visible message text
- enough topology to place undirected associations

Prefer explicit `Object Layout`.
If `Object Layout` is missing, derive associations from message pathways only when one clean undirected topology is implied.
If two or more plausible topologies exist, stop and ask.

## Create Workflow

- Parse the source into the normalized model.
- Validate names, numbering, endpoints, stereotypes, and layout consistency before drawing.
- Place the primary actor on the far left or bottom-left.
- Place the main coordinator or central object near the center.
- Place external actors and their proxies on the far right or bottom-right.
- Keep association lines plain and undirected.
- Represent each message with its own editable text box and its own short directional connector near the relevant association.
- Do not merge multiple message numbers into one text box unless the user explicitly asks for a compact grouped layout.
- Save the final XML as a `.drawio` file next to the source file when a source file exists.
- Save to `output/<slug>.drawio` when the user gives only pasted text and no source path.

## Update Workflow

- Read the existing `.drawio` XML and the revised source text.
- Preserve current positions and styles when the structure is still compatible.
- Rebuild affected nodes, links, and message blocks when the text change makes the old layout inconsistent.
- Regenerate the full diagram instead of patching piecemeal when structure, topology, or style drift would make patching less reliable.
- Tell the user when you switch from minimal patching to full regeneration.

## Non-Negotiable Rules

- Do not guess missing participants, stereotypes, message directions, or pathway connections.
- Do not silently rename participants.
- Do not attach arrowheads to association lines.
- Do not use Mermaid or CSV for final rendering when the diagram needs draw.io actor shapes and floating directional connectors. Use XML.
- Render each software object as two centered lines: stereotype on top, `: ObjectName` on the second line.
- Render actors with the built-in draw.io UML actor shape, not a manually assembled stick figure.
- Render each actor label with the actor shape and without a leading colon.
- Use a short directional connector with a visible line and arrowhead for each message. Do not use a standalone triangle marker.
- Keep one message per text box by default so each message stays independently editable.

## References

- Use [references/input-contract.md](references/input-contract.md) for parsing rules, blocking conditions, and output naming.
- Use [references/xml-patterns.md](references/xml-patterns.md) for draw.io XML structure, actor construction, object box styles, message blocks, and layout heuristics.
- Use [references/example-blueprint.md](references/example-blueprint.md) only when you need a full example blueprint.
