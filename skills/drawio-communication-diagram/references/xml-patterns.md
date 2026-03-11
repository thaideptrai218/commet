# XML Patterns

Use `mcp__drawio__open_drawio_xml` as the primary rendering path.
Use draw.io XML for the final artifact because communication diagrams in this style need draw.io actor shapes, plain associations, floating text, and free-floating directional connectors.

## Base Document

Start from a normal draw.io XML skeleton:

```xml
<mxfile host="app.diagrams.net">
  <diagram name="UC-Example">
    <mxGraphModel grid="1" gridSize="10" page="1" pageScale="1" pageWidth="1100" pageHeight="850">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Keep coordinates on a 10 px grid.
Use enough whitespace around associations to hold floating message blocks.

## Software Object Recipe

Use a standard rectangle vertex for each software object.

- Shape: rectangle
- Fill: `#82CAFA`
- Stroke: black
- Text: centered, two lines
- Top line: rendered stereotype with guillemets, for example `&#171;coordinator&#187;`
- Bottom line: `: SearchCoordinator`

Recommended style:

```text
rounded=0;whiteSpace=wrap;html=1;fillColor=#82CAFA;strokeColor=#000000;align=center;verticalAlign=middle;fontColor=#000000;
```

Recommended size:

- width: 150-190
- height: 60-80

## Actor Recipe

Use the built-in draw.io UML actor shape.

- Shape: UML actor
- Fill: `#82CAFA`
- Stroke: black
- Label: actor name, shown with the actor shape and no leading colon

Recommended style:

```text
shape=umlActor;whiteSpace=wrap;html=1;fillColor=#82CAFA;strokeColor=#000000;verticalLabelPosition=bottom;verticalAlign=top;align=center;
```

Recommended size:

- width: `40-60`
- height: `70-100`

## Association Recipe

Use a plain black edge for each structural link.

- no arrowheads
- thin black stroke
- orthogonal routing when it improves clarity

Recommended style:

```text
edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;endArrow=none;startArrow=none;strokeColor=#000000;
```

These are structural links only.
Do not encode message direction on the association itself.

## Message Text Recipe

Use one floating text vertex per message near the association, not attached to either endpoint.

- text format: `1.2: request initial published listings`
- keep one message number per text box by default
- do not merge multiple messages into one text box unless the user explicitly asks for grouping

Recommended style:

```text
text;html=1;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;whiteSpace=wrap;fontColor=#000000;
```

## Direction Connector Recipe

Use one short free-floating connector edge per message next to its text box.

- do not connect this edge to the participant nodes
- keep a visible line segment plus arrowhead
- keep it roughly parallel to the nearby association
- point it from the `from` participant toward the `to` participant

Recommended style:

```text
edgeStyle=none;rounded=0;html=1;endArrow=classic;startArrow=none;strokeColor=#000000;
```

Build the connector with `sourcePoint` and `targetPoint` in the edge geometry so it remains editable as a draw.io connector.

## Layout Heuristics

Use these defaults unless the source text clearly says otherwise:

- place the primary actor on the far left or bottom-left
- place the main coordinator or central object near the center
- place external-system actors and their proxies on the far right or bottom-right
- use horizontal spacing around `180-220`
- use vertical branch spacing around `120-160`
- keep at least `50-70` px of free space near a pathway that carries many separate messages

When the source includes an ASCII `Object Layout`, preserve its relative topology and branch direction, then adjust spacing locally to avoid collisions.

## Update Strategy

When editing an existing `.drawio`:

- preserve current coordinates and IDs when the existing structure is still valid
- patch local message blocks and labels when the topology is unchanged
- rebuild the whole XML when topology, actor shape choice, or message placement must change substantially

## Minimal XML Example

Use this as a pattern, not as a fixed template:

```xml
<mxCell id="obj-search" value="&#171;coordinator&#187;&lt;br/&gt;: SearchCoordinator" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#82CAFA;strokeColor=#000000;align=center;verticalAlign=middle;fontColor=#000000;" vertex="1" parent="1">
  <mxGeometry x="360" y="180" width="170" height="70" as="geometry"/>
</mxCell>

<mxCell id="msg-1-1" value="1.1: request search page" style="text;html=1;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;whiteSpace=wrap;fontColor=#000000;" vertex="1" parent="1">
  <mxGeometry x="235" y="205" width="170" height="24" as="geometry"/>
</mxCell>

<mxCell id="msg-1-1-arrow" style="edgeStyle=none;rounded=0;html=1;endArrow=classic;startArrow=none;strokeColor=#000000;" edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="405" y="216" as="sourcePoint"/>
    <mxPoint x="445" y="216" as="targetPoint"/>
  </mxGeometry>
</mxCell>
```
