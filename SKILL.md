---
name: remotion-editor
description: Best practices for building video editors with Remotion
metadata:
  tags: remotion, editor, timeline, state-management, canvas, undo-redo
---

## When to use

Use this skill when you are building a video editor or an interactive creation tool on top of Remotion. It provides patterns for high-performance state management, timeline interactions, and canvas manipulation.

## How to use

Read individual rule files for detailed explanations and code examples:

- [rules/state-optimization.md](rules/state-optimization.md) - Using the "Many Contexts" pattern to optimize editor performance.
- [rules/timeline-interactions.md](rules/timeline-interactions.md) - Implementing seeking, snapping, and zooming in the timeline.
- [rules/canvas-logic.md](rules/canvas-logic.md) - Handling interactive elements, drag-and-drop, and snap points on the canvas.
- [rules/undo-redo.md](rules/undo-redo.md) - Implementing an efficient undo/redo stack for video project states.
- [rules/asset-lifecycle.md](rules/asset-lifecycle.md) - Managing remote assets, local caching (IndexedDB), and blob URL persistence.
- [rules/editor-remotion-sync.md](rules/editor-remotion-sync.md) - Synchronizing editor state with Remotion compositions and the Player.
