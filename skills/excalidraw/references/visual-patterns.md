# Visual Patterns and Design Checks

Use a pattern that makes a relationship visible. These are starting points; combine or adapt them when the concept calls for it.

## Match the Pattern to the Relationship

| Idea | Pattern |
|---|---|
| One thing produces several outcomes | Fan-out: one source with branches or radial arrows |
| Several things combine | Convergence: inputs narrow toward a shared result |
| Parent and child relationships | Tree: branches and labels, with minimal node boxes |
| Ordered steps or events | Timeline: line, markers, and labels |
| Repeated feedback or change | Cycle: sequence with a visible return path |
| An abstract state or context | Cloud: overlapping ellipses or a loose boundary |
| Input changes into an output | Transformation: before, process, and after |
| Alternatives or tradeoffs | Parallel structures with meaningful visual contrast |
| Phases or boundaries | Separate zones with whitespace, dividers, or borders |

## Match the Shape to Its Role

| Role | Shape or treatment |
|---|---|
| Start, trigger, or external actor | Ellipse |
| End or result | Ellipse |
| Decision or condition | Diamond |
| Process or action | Rectangle |
| Timeline marker or connection point | Small ellipse |
| Hierarchy, timeline, or divider | Lines with free-floating text |
| Section title or annotation | Free-floating text |

Start with text without a container. Add a shape when it expresses meaning, grouping, or a useful connection target. Keep most supporting text unboxed.

## Technical Evidence

Technical and teaching diagrams should contain details that show what the subject actually does. Choose from:

- A short code snippet for an API or integration.
- A small request, response, schema, or data example.
- Actual event, function, endpoint, or state names.
- A sequence of concrete steps or state changes.
- A compact interface mockup containing realistic labels or values.

Verify details from authoritative sources and keep examples readable at the final image size. Do not add evidence that does not help explain the central idea.

## Multiple Levels of Detail

For a broad technical diagram, combine:

1. An overview that shows the complete flow.
2. Sections that group components by responsibility, phase, or actor.
3. Concrete examples that explain important steps within those sections.

Build each section as a coherent group, give elements descriptive IDs, and then review how the sections connect in the whole scene.

## Composition

- Establish one clear path for the viewer's eye.
- Use a common grid and keep related elements closer than unrelated ones.
- Give the main idea more visual weight and space than supporting details.
- Use different visual patterns for different concepts, while keeping colors and typography consistent.
- Connect relationships with arrows or lines; position alone is ambiguous.
- Route arrows around unrelated content. Use waypoints or elbow turns if a direct path would cross another element.
- Use arrow labels only when the relationship itself needs explanation; keep them short.
- Avoid putting a label in the center of a large background zone. Place a separate title near its top edge.
- Use whitespace and typography for hierarchy before adding more boxes.

## Render Review

Use an MCP screenshot after creating or editing the scene. Check it against the design plan and look for:

- Clipped or unreadable text.
- Overlapping elements that obscure meaning.
- Arrows that cross unrelated elements or point to the wrong target.
- Labels that are not clearly associated with anything.
- Sections that feel cramped or leave large, unexplained gaps.
- A reading path or emphasis that differs from the intended explanation.

Fix the issues with MCP edits and inspect a new screenshot. A structurally valid scene can still render poorly, so review the image before delivering it.
