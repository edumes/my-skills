# Excalidraw Scene and Element Structure

Use MCP tools for file and scene operations. This reference explains the native `.excalidraw` structure when checking files or investigating a rendering issue. Prefer the MCP-friendly element format in `element-templates.md` when sending new elements to the server.

## Scene Envelope

A native scene file is a JSON object with scene metadata, an `elements` array, application state, and an optional files map:

```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "https://excalidraw.com",
  "elements": [],
  "appState": {
    "viewBackgroundColor": "#ffffff",
    "gridSize": 20
  },
  "files": {}
}
```

## Common Element Fields

| Field | Meaning |
|---|---|
| `id` | Stable element identifier |
| `type` | `rectangle`, `ellipse`, `diamond`, `arrow`, `line`, `text`, or `frame` |
| `x`, `y` | Position in scene coordinates |
| `width`, `height` | Element dimensions |
| `strokeColor` | Outline or text color |
| `backgroundColor` | Fill color or `transparent` |
| `fillStyle` | Fill pattern, often `solid` |
| `strokeWidth`, `strokeStyle` | Outline thickness and pattern |
| `roughness` | Edge style; use `0` for smooth technical diagrams |
| `opacity` | Visibility from 0 to 100 |
| `seed` | Deterministic value for hand-drawn rendering |
| `isDeleted` | Whether the native element is deleted |

The MCP server normalizes common defaults and bound labels. Do not hand-author low-level binding bookkeeping when the MCP format supports a simpler equivalent.

## Text Fields

Text elements use `text` and `originalText`, with `fontSize`, `fontFamily`, `textAlign`, and `verticalAlign` controlling appearance. Text within a shape has a `containerId` in the native format, while the MCP can create it from a shape's `text` value.

## Arrows and Bindings

Native arrow elements store relative coordinates in `points`, plus `startBinding` and `endBinding` objects that identify connected shapes. The MCP's normalized input accepts `startElementId` and `endElementId` and manages the binding relationships. Ensure each referenced element ID exists.

For deliberate bends, provide intermediate points. Curved arrows can use a rounded path; elbowed arrows use right-angle segments. Check the rendered result to confirm the route avoids unrelated elements.
