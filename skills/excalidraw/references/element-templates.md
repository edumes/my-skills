# MCP Element Examples

Use these examples with `batch_create_elements`. They show the MCP's normalized element format; choose actual colors from `color-palette.md`. The server fills in Excalidraw bookkeeping fields and converts `text` on a shape into a bound label.

## Free-Floating Text

```json
{
  "id": "section-title",
  "type": "text",
  "x": 100,
  "y": 80,
  "width": 300,
  "height": 32,
  "text": "Request Processing",
  "fontSize": 24,
  "fontFamily": "3",
  "strokeColor": "#1e40af",
  "textAlign": "left",
  "verticalAlign": "top",
  "roughness": 0
}
```

## Labeled Process

```json
{
  "id": "validate-request",
  "type": "rectangle",
  "x": 360,
  "y": 180,
  "width": 220,
  "height": 90,
  "text": "Validate request",
  "backgroundColor": "#60a5fa",
  "strokeColor": "#1e3a5f",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "roughness": 0
}
```

## Decision

```json
{
  "id": "valid-request",
  "type": "diamond",
  "x": 670,
  "y": 180,
  "width": 150,
  "height": 110,
  "text": "Valid?",
  "backgroundColor": "#fef3c7",
  "strokeColor": "#b45309",
  "fillStyle": "solid",
  "roughness": 0
}
```

## Bound Arrow

```json
{
  "id": "request-to-validation",
  "type": "arrow",
  "x": 0,
  "y": 0,
  "startElementId": "incoming-request",
  "endElementId": "validate-request",
  "text": "HTTPS"
}
```

Use `startElementId` and `endElementId` to connect the arrow to the edges of existing elements. Omit `text` on an arrow unless naming the relationship helps the viewer.

## Timeline Marker and Structural Line

```json
[
  {
    "id": "event-marker-1",
    "type": "ellipse",
    "x": 180,
    "y": 280,
    "width": 14,
    "height": 14,
    "backgroundColor": "#3b82f6",
    "strokeColor": "#1e3a5f",
    "roughness": 0
  },
  {
    "id": "timeline-spine",
    "type": "line",
    "x": 100,
    "y": 286,
    "width": 500,
    "height": 0,
    "points": [[0, 0], [500, 0]],
    "strokeColor": "#64748b",
    "strokeWidth": 1,
    "roughness": 0
  }
]
```

Create arrows after their endpoint shapes when the tool workflow requires the target IDs to exist first. For background zones, use an unlabeled rectangle and a separate free-floating title near its top edge.
