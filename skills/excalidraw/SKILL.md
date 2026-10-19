---
name: excalidraw
description: Create and refine Excalidraw diagrams for workflows, architectures, systems, and concepts. Use whenever the user wants a diagram or asks to visualize how something works, including local .excalidraw files, Obsidian .excalidraw.md drawings, or images for Markdown. Use the configured Excalidraw MCP tools for all canvas and file operations. This skill provides visual design guidance.
---

# Excalidraw Diagram Design

Use the configured Excalidraw MCP server to create, inspect, refine, and export diagrams. The skill guides concept mapping and visual decisions; MCP tools operate the canvas, read and write scene files, and return screenshots and images.

## Customization

`references/color-palette.md` is the color source for this skill. Read it before choosing colors. Use its semantic colors consistently for shape fills, strokes, text, and evidence panels. If the user gives brand colors, adapt the palette to those colors while preserving contrast and consistent meaning.

Read `references/visual-patterns.md` for the pattern library and `references/element-templates.md` for MCP-friendly element examples. Read `references/json-schema.md` when a task requires inspecting or understanding native Excalidraw data.

## Core Idea

Design diagrams to explain. The shapes, spacing, and connections should communicate relationships, causality, and flow alongside their labels.

**Structure check:** imagine removing every label. The remaining arrangement should still give some clue about how its parts relate. If it does not, choose a more meaningful layout.

**Learning check:** a viewer should be able to learn a concrete fact or relationship from the diagram. A collection of names in boxes often gives little more than a list.

## Assess the Required Depth First

### Simple or Conceptual Diagrams

Use a small number of abstract shapes when:

- Explaining a mental model, principle, or philosophy.
- The audience needs an overview instead of technical detail.
- The abstraction itself is the subject.

### Comprehensive or Technical Diagrams

Use concrete details when:

- Showing a real system, protocol, or architecture.
- The diagram will teach a process or integration.
- The audience needs to recognize actual inputs, outputs, events, or component behavior.

Technical diagrams should include evidence artifacts (see below) when they help prove the explanation or teach how the system behaves.

## Research Technical Details

Before drawing a protocol, API, framework, or architecture, verify important details against its source or authoritative documentation:

1. Find the actual payloads, formats, or data structures.
2. Confirm real event, method, endpoint, or state names.
3. Understand how the documented parts connect.
4. Use the source's terminology and distinguish verified facts from assumptions.

Research improves both accuracy and the diagram's teaching value. Keep citations or source links near technical details when the output context supports them.

## Evidence Artifacts

An evidence artifact is a compact, concrete example that lets a viewer see what a component or transition actually does. Include the kinds that fit the subject:

| Evidence | Useful for | Visual treatment |
|---|---|---|
| Short code excerpt | APIs, integrations, and implementation | Compact dark panel with readable syntax colors |
| Data or JSON sample | Payloads, schemas, and transformations | Small panel with actual keys and representative values |
| Events or steps | Protocols, workflows, and lifecycles | Timeline with actual event names |
| Interface details | Products and user-facing flows | Small realistic UI arrangement with meaningful content |
| Real input or output | Processing and conversion | Show representative content entering or leaving the process |
| Method or endpoint names | Technical connections | Use actual names from verified sources |

For a data pipeline, show meaningful input, transformation, and output. For a streaming protocol, show real event names and a useful sample of the data. Select examples that support the explanation, and keep them legible at the intended display size.

## Diagrams with Multiple Zoom Levels

Comprehensive diagrams should help the viewer move from overview to explanation:

1. **Summary flow:** show the whole process or system at a glance.
2. **Sections:** group parts by role, phase, responsibility, or actor.
3. **Details:** add examples, payloads, code, or real events where they teach something.

The summary provides context; section boundaries provide organization; details explain how important parts work. Use all three levels for tutorials and technical overviews when the scope warrants it.

## Display Information with Structure

Choose layouts that mirror the subject. A fan-out can show one source producing several outputs. A timeline can make order visible. A convergence can show aggregation. A cycle can show feedback. See `references/visual-patterns.md` for more choices and examples.

| Less informative | More explanatory |
|---|---|
| A row of equal boxes with names | Each item has a form that reflects its behavior |
| Repeating cards for every concept | Distinct visual patterns for distinct relationships |
| Icons added only for decoration | Shapes that express the concept itself |
| Every item in the same container | Selective grouping with clear boundaries |
| Only abstract labels | Real examples where technical detail matters |

Simple diagrams work well for broad ideas and quick introductions. Comprehensive diagrams serve detailed walkthroughs where the viewer needs to learn both structure and behavior.

## Containers and Free-Floating Text

Text does not always need a box. Prefer free-floating text for:

- Section headings, captions, and annotations.
- Supporting details and metadata.
- Labels where typography already creates enough hierarchy.

Use a container when:

- It defines an important region or group.
- The shape itself represents a distinct object or action.
- Other elements need to connect to its boundary.

For each container, consider whether text alone would communicate as well. Use size, weight, and color to create hierarchy before adding shapes. Keep the ratio of text inside containers low; as a guide, aim for fewer than one in three text elements inside boxes.

## Design Process

Use this sequence before creating the scene:

### Step 1: Assess the Depth

Choose a conceptual overview or a comprehensive technical explanation. If the diagram needs to teach a technical subject, research it and plan evidence artifacts first.

### Step 2: Understand the Subject

Read the source material. For each concept, identify:

- What it does.
- Which other concepts it affects or depends on.
- What changes as information moves through the process.
- What a viewer needs to see to understand it.

### Step 3: Map Concepts to Patterns

Choose a visual pattern for each important relationship. Patterns include fan-out, convergence, tree, timeline, cycle, cloud, transformation, comparison, and phase separation. Use `references/visual-patterns.md` to select and combine them.

### Step 4: Add Variety

For a diagram with several major concepts, vary the visual form according to their meaning. Keep a shared color palette, typographic hierarchy, and spacing system so the scene still feels cohesive.

### Step 5: Sketch the Reading Path

Plan the viewer's route through the diagram. Mark the start, major transitions, sections, examples, and conclusion. Leave room for connections and evidence before positioning individual elements.

### Step 6: Create Elements Through MCP

Use `read_diagram_guide` for current canvas guidance, then create the scene with the configured Excalidraw MCP tools. Use `references/element-templates.md` for concise MCP-compatible shapes, labels, and arrows.

### Step 7: Render and Refine

Use `get_canvas_screenshot` to inspect the rendered scene. Compare it with the planned explanation, correct visual defects using MCP edits, and inspect a new screenshot. Continue until the diagram is ready to share.

## Large Diagram Strategy

Build a comprehensive scene in manageable sections. This makes each part easier to reason about and reduces errors in placement, labels, and connections.

### Build Each Section

1. Plan the whole scene and its natural sections before creating elements.
2. Create one coherent section at a time, including its labels and internal connections.
3. Use stable descriptive IDs such as `trigger_event` or `request_validation`.
4. Keep track of cross-section relationships and connect them when both endpoints are present.
5. Use space to show section boundaries; add a boundary shape only when it clarifies grouping.

### Review the Whole Scene

After all sections are present, inspect the scene and check:

- Connections between sections point to the intended elements.
- The overall spacing feels balanced.
- Sections are easy to distinguish and the viewer can follow the whole flow.
- Stable IDs and arrow bindings refer to existing elements.

### Section Planning

Common section roles include an entry point, routing or decisions, the main activity, and resulting outputs. Let the subject determine section order and size; the central teaching point may need the most room.

## Visual Pattern Library

Choose the pattern that best explains a relationship. Examples and guidance are in `references/visual-patterns.md`.

- **Fan-out:** one source branches to several outcomes.
- **Convergence:** several inputs combine into one result.
- **Tree:** a hierarchy branches from parent to child.
- **Timeline:** markers and labels show ordered events.
- **Cycle:** a return path shows repeated feedback or improvement.
- **Cloud:** overlapping shapes suggest a fuzzy state or context.
- **Transformation:** input passes through a process into a changed output.
- **Comparison:** parallel structures make differences visible.
- **Separation:** a boundary or gap marks a phase change.
- **Lines as structure:** use lines for timelines, trees, flow spines, and dividers; labels can sit alongside without boxes.

When an arrow would cross unrelated content, add waypoints or route it around the perimeter. Avoid crowded long cross-zone arrows; make the sections adjacent or use a clearer relationship annotation.

## Shape Meaning

Choose shapes based on their role:

| Concept | Suggested form |
|---|---|
| Labels, descriptions, and details | Free-floating text |
| Titles and annotations | Free-floating text with typographic hierarchy |
| Timeline or connection markers | Small ellipses |
| Starts, triggers, external actors, and outcomes | Ellipses |
| Decisions and conditions | Diamonds |
| Processes and actions | Rectangles |
| Abstract states or contexts | Overlapping ellipses |
| Hierarchies | Lines with text labels |

Use a shape when the form adds meaning. Text alone is often the clearer choice for labels and supporting detail.

## Color as Meaning

Colors should distinguish semantic roles or states. Use `references/color-palette.md` as the default palette and the MCP `read_diagram_guide` for current canvas guidance. Keep a consistent mapping from meaning to color, pair darker strokes with lighter fills, and choose text colors with enough contrast.

Evidence panels can use a dark background and restrained syntax or data colors. Use the palette instead of inventing extra colors for decoration.

## Finish and Aesthetics

For a clean technical diagram, use smooth edges (`roughness: 0`). For a brainstorming sketch, use a hand-drawn edge style when it fits the requested tone. Keep line widths consistent: thin for dividers, standard for shapes and main connections, and bold only for a small number of emphasized paths.

Use full opacity. Establish hierarchy through position, scale, color, stroke, and whitespace. Small dots can work as timeline markers, bullets, or connection points without adding another container.

## Layout Principles

- Use scale to establish priority: the main concept should attract attention first.
- Give important ideas more breathing room than supporting details.
- Use consistent spacing for elements that have the same role.
- Choose a clear direction for sequences, usually left-to-right or top-to-bottom; use radial placement for hubs.
- Draw arrows or lines for relationships that matter.
- Give sections enough room for labels and evidence; avoid both cramped groups and unexplained empty areas.

## Text Rules

Use readable content in the element's `text` field. Keep titles and body labels concise. Use an obvious type hierarchy and make labels large enough for the expected output size. Avoid placing every label on an arrow; short arrows especially have little room for text.

When building technical examples, use the correct field names and values. For shapes with labels, provide the label through the MCP normalized `text` property so it can maintain the bound text correctly. See `references/element-templates.md` and `references/json-schema.md` for details.

## Native Scene Structure

The MCP handles common Excalidraw element bookkeeping. Use `references/json-schema.md` when you need to understand a saved `.excalidraw` file or native relationships between text, shapes, and arrows. Prefer normalized MCP fields over manually maintaining native binding metadata.

## Render and Validate (Required)

A diagram's data does not reveal every visual issue. After generating or editing it, call `get_canvas_screenshot`, inspect the image, and refine through MCP tools.

### Review Loop

1. Render the current canvas with `get_canvas_screenshot`.
2. Compare the image with the conceptual plan. Check that visual patterns match the relationships and that the eye follows the intended order.
3. Check for text clipping, accidental overlaps, crossing arrows, ambiguous labels, inconsistent spacing, unreadable small text, and unbalanced sections.
4. Correct the problems with `update_element`, `batch_create_elements`, deletion, or layout tools.
5. Render another screenshot and inspect the updated result.
6. Repeat while improvements are needed. A clean but weak composition still deserves another pass if its structure does not teach the intended idea.

### Stop When

- The image matches the planned visual explanation.
- Text is readable and no important content is clipped.
- Connections reach the right elements and route cleanly.
- Spacing, hierarchy, and section boundaries are balanced.
- Technical examples are accurate and useful.

## Quality Checklist

### Depth and Evidence

- Technical names, formats, and relationships have been checked against reliable sources.
- Evidence examples show real details and remain readable.
- Comprehensive diagrams combine an overview, sections, and focused examples when appropriate.
- The audience can learn something concrete from the diagram.

### Concept and Composition

- The visual structure communicates the relationship, even with fewer labels.
- The diagram has one clear argument or explanatory path.
- Major concepts use patterns that reflect their behavior.
- The layout avoids repeated generic cards and containers.
- Each container contributes grouping or meaning.

### Structure and Style

- Lines and text are used where they make hierarchies or timelines clearer.
- Relationships have explicit arrows or lines.
- The important elements have the most visual weight and space.
- Palette meanings are consistent and text contrast is strong.
- Text content is clean, concise, and large enough to read.
- Smooth linework is used for technical subjects unless another style is requested.

### Rendered Result

- The diagram has been rendered and visually inspected through MCP.
- No text is clipped or unreadable.
- No unintended overlaps remain.
- Arrows reach their intended targets without obscuring unrelated elements.
- Similar elements have consistent spacing and the overall scene feels balanced.

## Save for Markdown and Obsidian

For a repository diagram, use `export_scene` to save the editable `.excalidraw` source. Use `export_to_image` to create a PNG or SVG for a Markdown renderer, then link the image with a relative path:

```markdown
![Service request flow](./service-request-flow.png)
```

Keep the editable source beside the image when future edits are expected. Report both output paths when you create both files.

For an Obsidian vault, use `export_scene` with a `filePath` ending in `.excalidraw.md` to save the plugin's native Markdown-backed format. Use `import_scene` to open an existing drawing and `export_to_image` when the Markdown page also needs a directly rendered image.

## References

- `references/color-palette.md` — semantic colors, evidence panel colors, and contrast.
- `references/visual-patterns.md` — relationship patterns, shape meaning, composition, and visual review.
- `references/element-templates.md` — MCP-friendly examples for common elements and arrow bindings.
- `references/json-schema.md` — native Excalidraw scene structure and element properties.
- [Excalidraw MCP server](https://github.com/yctimlin/mcp_excalidraw) — the canvas tools used by this skill.
- [Excalidraw diagram design source](https://github.com/coleam00/excalidraw-diagram-skill) — source of the design approach adapted here.
