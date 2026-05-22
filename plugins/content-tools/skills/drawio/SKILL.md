---
name: drawio
description: Generate professional draw.io diagrams (architecture, flowcharts, system maps, ERDs, sequence diagrams) by writing .drawio XML files. Use when the user asks to create or update any diagram. Pairs with the VS Code "Draw.io Integration" extension for live preview.
---

# draw.io Diagramming Skill

Generate a complete `.drawio` XML file in one shot and write it to disk. The user opens it in VS Code (with the Draw.io Integration extension) for live preview. When updating an existing diagram, read the file first, then write the full updated XML.

---

## Workflow

1. **Understand the diagram** — identify type (architecture, flowchart, ERD, etc.), components, and relationships
2. **Plan the layout** — decide layers, columns, and which elements connect to which
3. **Write the XML** — one complete file, no iteration
4. **Save the file** — write to `<working-dir>/<diagram-name>.drawio`
5. **Tell the user** — give the file path and say "open in VS Code to view"

For updates: Read the existing file first, make targeted edits, write the full file back.

---

## File Structure

Every draw.io file follows this wrapper:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="app.diagrams.net" version="24.0.0">
  <diagram name="Diagram Title" id="unique-id">
    <mxGraphModel dx="1200" dy="900" grid="0" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1" page="1"
                  pageScale="1" pageWidth="1200" pageHeight="900" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- all elements go here, with parent="1" unless inside a container -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## Element Types

### Text label (title)
```xml
<mxCell id="title" value="My Diagram"
  style="text;html=1;strokeColor=none;fillColor=none;align=center;
         verticalAlign=middle;whiteSpace=wrap;fontSize=26;fontStyle=1;
         fontFamily=Helvetica;"
  vertex="1" parent="1">
  <mxGeometry x="50" y="14" width="1000" height="42" as="geometry" />
</mxCell>
```

### Swimlane (layer / zone container)
```xml
<mxCell id="zone-backend" value="Backend Services"
  style="swimlane;startSize=24;fillColor=#dae8fc;strokeColor=#6c8ebf;
         strokeStyle=dashed;strokeWidth=2;fontFamily=Helvetica;fontSize=12;
         fontColor=#1971c2;fontStyle=1;rounded=1;arcSize=4;"
  vertex="1" parent="1">
  <mxGeometry x="50" y="80" width="960" height="110" as="geometry" />
</mxCell>
```
Children of a swimlane use `parent="zone-backend"` and **relative coordinates** (x/y from the container's top-left, below the startSize header).

### Box (component / node)
```xml
<mxCell id="svc-auth" value="Auth Service"
  style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;
         strokeColor=#6c8ebf;fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="zone-backend">
  <mxGeometry x="20" y="30" width="160" height="55" as="geometry" />
</mxCell>
```
Use `&#xa;` for newlines inside a value: `value="Line 1&#xa;Line 2"`

### Arrow (edge)
```xml
<mxCell id="arr-1" value="HTTP"
  style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;
         jettySize=auto;exitX=0.5;exitY=1;exitDx=0;exitDy=0;
         entryX=0.5;entryY=0;entryDx=0;entryDy=0;
         fontFamily=Helvetica;fontSize=12;strokeColor=#6c8ebf;strokeWidth=2;"
  edge="1" source="svc-auth" target="svc-db" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```
- Always use `parent="1"` for arrows, even when source/target are inside containers
- `exitX/Y` and `entryX/Y` control which edge the arrow leaves/enters (0.5/1 = bottom center, 0.5/0 = top center, 1/0.5 = right center, 0/0.5 = left center)
- `edgeStyle=orthogonalEdgeStyle` gives clean right-angle routing automatically

### Diamond (decision node)
```xml
<mxCell id="decision-1" value="Auth OK?"
  style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;
         fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="1">
  <mxGeometry x="300" y="200" width="120" height="80" as="geometry" />
</mxCell>
```

### Cylinder (database)
```xml
<mxCell id="db-1" value="PostgreSQL"
  style="shape=mxgraph.flowchart.database;whiteSpace=wrap;html=1;
         fillColor=#dae8fc;strokeColor=#6c8ebf;fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="1">
  <mxGeometry x="300" y="200" width="120" height="80" as="geometry" />
</mxCell>
```

### Actor (user/person)
```xml
<mxCell id="user-1" value="Developer"
  style="shape=mxgraph.flowchart.start_2;fillColor=#dae8fc;strokeColor=#6c8ebf;
         fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="80" as="geometry" />
</mxCell>
```

---

## Color Palettes

### Enterprise Consulting + Document Standards (preferred for architecture diagrams)
*Merges SAP deck visual impact (red accent, navy card headers) with AI Guidelines PDF structure (deep navy section headers, gray code blocks)*

**Two-accent rule:**
- **NAVY_DEEP** `#1F3B6E` = dominant — use for section labels, component titles, zone headers
- **RED** `#E31837` = power accent — use SPARINGLY for numbered circles, highlighted/active components only

| Role / Element         | fillColor  | strokeColor | fontColor  | Notes |
|------------------------|------------|-------------|------------|-------|
| Page background        | `#FFFFFF`  | —           | —          | Always white |
| Standard component box | `#FFFFFF`  | `#D0D5DD`   | `#1A1A1A`  | Thin gray border |
| Title / label text     | —          | —           | `#1F3B6E`  | NAVY_DEEP, bold |
| Active / highlighted   | `#FEE2E2`  | `#E31837`   | `#E31837`  | Use sparingly |
| Section zone (light)   | `#F5F7FA`  | `#D0D5DD`   | `#1A1A1A`  | Group container |
| Card header band       | `#0D3B5E`  | `#0D3B5E`   | `#FFFFFF`  | NAVY_CARD, bold |
| Arrow / connector      | `#9CA3AF`  | —           | `#6B7280`  | Gray, width=2 |
| Numbered circle        | `#E31837`  | `#E31837`   | `#FFFFFF`  | Sequence labels |
| NAVY circle (alt)      | `#1F3B6E`  | `#1F3B6E`   | `#FFFFFF`  | For non-key steps |
| Decision node          | `#EEF2FF`  | `#C7D2FE`   | `#1F3B6E`  | Light indigo fill |
| Database / storage     | `#F0F9FF`  | `#BAE6FD`   | `#1F3B6E`  | Light sky fill |
| Code / template block  | `#F0F2F5`  | `#D0D5DD`   | `#1A1A1A`  | Monospace text |
| External system        | `#F0FDF4`  | `#BBF7D0`   | `#166534`  | Light green |

Arrow stroke: `#9CA3AF`, width=2. Label font: Helvetica 11pt, color `#6B7280`.
Section zone label: bold, `#1F3B6E`, fontSize=13, placed at top-left of zone.

### Technical Layered Style (for swimlane/zone diagrams)

| Layer / Role     | fillColor | strokeColor | fontColor  |
|------------------|-----------|-------------|------------|
| User / Frontend  | `#dae8fc` | `#6c8ebf`   | `#1971c2`  |
| Core / Engine    | `#e1d5e7` | `#9673a6`   | `#9c36b5`  |
| Tools / Services | `#d5e8d4` | `#82b366`   | `#2f9e44`  |
| MCP / Middleware | `#ffe6cc` | `#d6b656`   | `#e8590c`  |
| API / External   | `#f8cecc` | `#b85450`   | `#e03131`  |
| Data / Storage   | `#d7f0f7` | `#0c8599`   | `#0c8599`  |
| Decision / Logic | `#fff2cc` | `#d6b656`   | `#1e1e1e`  |
| Neutral box      | `#ffffff`  | `#868e96`   | `#1e1e1e`  |

Use this palette for technical audience diagrams. Arrow stroke matches the originating layer.

---

## Layout Rules

### Swimlane (layered architecture)
- All zones: same x and width (e.g. `x=50, width=960`)
- Zone height: `startSize=24` header + content height (typically 80–110px total)
- Gap between zones: 16px
- Box y inside swimlane: start at 28–32px (leaves room below header)
- Box heights: 50px single-line, 60px two-line label

**5-item row** (width=960, box w=160, gap=32):
- x positions inside container: 20, 212, 404, 596, 788

**4-item row** (width=960, box w=215, gap=32):
- x positions: 15, 262, 509, 756

**3-item row** (width=960, box w=280, gap=40):
- x positions: 20, 340, 660

### Flowchart
- Top-to-bottom flow, 80px vertical spacing between nodes
- Decision diamonds: 120×80, center-aligned with flow
- All nodes same width (160px typical)

### ERD
- Entity boxes: 180px wide, 40px per row of attributes
- Use `fontStyle=1` (bold) for primary keys

---

## Arrow Discipline

- **Only connect adjacent layers** — arrows that skip layers create crossing clutter
- **3–6 arrows maximum** for architecture diagrams — one per key flow, not one per connection
- **Use orthogonalEdgeStyle** — draw.io auto-routes around containers, no manual waypoints needed
- **Label arrows** with ≤ 3 words (longer labels overlap boxes)
- For bidirectional flow, use one arrow with label "↕ request / response" rather than two arrows

---

## Common Diagram Templates

### Architecture — Component-Flow Style (Enterprise Consulting, preferred)
White background, labelled boxes, numbered red circles on arrows, clean left-to-right or hub-and-spoke layout.

```xml
<!-- Background (optional light zone grouping) -->
<mxCell id="zone-core" value=""
  style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F5F7FA;strokeColor=#D0D5DD;
         strokeWidth=1;arcSize=4;fontFamily=Helvetica;"
  vertex="1" parent="1">
  <mxGeometry x="300" y="60" width="560" height="200" as="geometry" />
</mxCell>

<!-- Component box -->
<mxCell id="comp-1" value="&lt;b&gt;Component Name&lt;/b&gt;&#xa;Short description"
  style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#D0D5DD;
         strokeWidth=1.5;fontFamily=Helvetica;fontSize=12;align=center;
         verticalAlign=middle;"
  vertex="1" parent="1">
  <mxGeometry x="340" y="100" width="180" height="60" as="geometry" />
</mxCell>

<!-- Numbered circle on arrow (place over the arrow midpoint) -->
<mxCell id="num-1" value="1"
  style="ellipse;whiteSpace=wrap;html=1;fillColor=#E31837;strokeColor=#E31837;
         fontColor=#FFFFFF;fontFamily=Helvetica;fontSize=11;fontStyle=1;
         aspect=fixed;"
  vertex="1" parent="1">
  <mxGeometry x="520" y="122" width="24" height="24" as="geometry" />
</mxCell>

<!-- Arrow (gray, clean) -->
<mxCell id="arr-1" value=""
  style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;
         jettySize=auto;exitX=1;exitY=0.5;exitDx=0;exitDy=0;
         entryX=0;entryY=0.5;entryDx=0;entryDy=0;
         strokeColor=#9CA3AF;strokeWidth=2;fontFamily=Helvetica;fontSize=11;"
  edge="1" source="comp-1" target="comp-2" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Rules for component-flow diagrams:**
- White background (`#FFFFFF`), no page-level color
- Boxes: `fillColor=#FFFFFF`, `strokeColor=#D0D5DD`, `strokeWidth=1.5`, `rounded=1`
- Highlighted/active box: `fillColor=#FEE2E2`, `strokeColor=#E31837`
- Arrows: `strokeColor=#9CA3AF`, `strokeWidth=2`, no label (use numbered circles instead)
- Numbered circles: 24×24 ellipse, `fillColor=#E31837`, `fontColor=#FFFFFF`
- Group zones: `fillColor=#F5F7FA`, `strokeColor=#D0D5DD`, no header band
- Font: Helvetica 12pt throughout; bold component names with `&lt;b&gt;` HTML tags

### Architecture (layered / swimlane)
Structure: Title → swimlane zones top-to-bottom → orthogonal arrows between adjacent layers.
Use the Technical Layered palette above. Best for technical audiences.

### Flowchart
```xml
<!-- Start -->
<mxCell id="start" value="Start"
  style="ellipse;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;
         fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="1">
  <mxGeometry x="400" y="40" width="120" height="50" as="geometry" />
</mxCell>
<!-- Step -->
<mxCell id="step1" value="Process request"
  style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
         fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="1">
  <mxGeometry x="380" y="140" width="160" height="55" as="geometry" />
</mxCell>
<!-- Decision -->
<mxCell id="dec1" value="Valid?"
  style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;
         fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="1">
  <mxGeometry x="390" y="250" width="140" height="80" as="geometry" />
</mxCell>
<!-- End -->
<mxCell id="end" value="End"
  style="ellipse;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;
         fontFamily=Helvetica;fontSize=13;"
  vertex="1" parent="1">
  <mxGeometry x="400" y="390" width="120" height="50" as="geometry" />
</mxCell>
```

---

## Quality Checklist (before writing the file)

1. All IDs unique — no two `id=` values are the same
2. Every arrow's `source` and `target` reference an existing cell ID
3. Children of swimlanes use the swimlane's ID as `parent`
4. All arrows use `parent="1"`
5. Newlines in labels use `&#xa;` not `\n`
6. Font is Helvetica throughout — no omitted fontFamily
7. Arrow labels are ≤ 3 words
8. No more than 6 arrows for architecture diagrams
