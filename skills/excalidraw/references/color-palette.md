# Excalidraw Color Palette

Use color to communicate role or state. Apply semantic colors consistently within a diagram. Pair a light fill with a darker stroke for contrast, and use the MCP `read_diagram_guide` tool when the canvas guide or user-provided brand colors should take precedence.

## Shape Colors

| Meaning | Fill | Stroke |
|---|---|---|
| Primary or neutral | `#3b82f6` | `#1e3a5f` |
| Secondary | `#60a5fa` | `#1e3a5f` |
| Tertiary | `#93c5fd` | `#1e3a5f` |
| Start or trigger | `#fed7aa` | `#c2410c` |
| End or success | `#a7f3d0` | `#047857` |
| Warning or reset | `#fee2e2` | `#dc2626` |
| Decision | `#fef3c7` | `#b45309` |
| AI or model | `#ddd6fe` | `#6d28d9` |
| Inactive or disabled | `#dbeafe` | `#1e40af` |
| Error | `#fecaca` | `#b91c1c` |

Use a dashed outline for inactive elements where that helps distinguish them from active elements.

## Text Hierarchy

| Role | Color |
|---|---|
| Titles | `#1e40af` |
| Subtitles | `#3b82f6` |
| Details and annotations | `#64748b` |
| Text on light fills | `#374151` |
| Text on dark fills | `#ffffff` |

## Evidence Panels

Use `#1e293b` for a dark code or data panel. Use syntax-aware colors for code and `#22c55e` for JSON or data text when it remains readable. Keep evidence snippets short and legible.

## Lines and Canvas

- Arrows can use the stroke color of their source element.
- Structural lines can use `#1e3a5f` or `#64748b`.
- Marker dots can use the primary fill, `#3b82f6`.
- Default to a white canvas (`#ffffff`) unless the output needs a dark background.
