---
name: remotion-editor
description: Best practices for building video editors and interactive tools with Remotion
metadata:
  tags: [remotion, editor, timeline, canvas, video-editing, react-performance]
  author: rayBlock
---

# Remotion Editor Skill

This skill provides comprehensive guidance for developers building video editors on top of Remotion. It covers everything from low-level timeline math to high-level state management and AI integration.

## When to use

Use this skill when:
- Building a timeline-based video editor.
- Implementing interactive canvas elements (DRAG, RESIZE, ROTATE).
- Optimizing React performance for 60fps playhead updates.
- Implementing complex features like Undo/Redo or AI captioning.

## Rules Reference

### Core Architecture
- **[State Optimization](rules/state-optimization.md)**: Using the "Many Contexts" pattern to avoid global re-renders.
- **[Undo/Redo](rules/undo-redo.md)**: Implementing a robust, memory-efficient history stack.
- **[Feature Flags](rules/feature-flags.md)**: Managing complexity in a growing editor codebase.
- **[Editor-Remotion Sync](rules/editor-remotion-sync.md)**: Maintaining consistency between editor state and Remotion.

### Timeline & Math
- **[Timeline Math](rules/timeline-math.md)**: Converting between pixels and frames; handling snapping.
- **[Timeline Interactions](rules/timeline-interactions.md)**: Zooming, scrolling, and performance.
- **[Keyboard Shortcuts](rules/keyboard-shortcuts.md)**: Focus-aware global listeners.

### Canvas & Rendering
- **[Canvas Logic](rules/canvas-logic.md)**: UV coordinate mapping and spatial transforms.
- **[Rendering Pipeline](rules/rendering-pipeline.md)**: Exporting videos and tracking job status.

### Data & AI
- **[Asset Lifecycle](rules/asset-lifecycle.md)**: Managing blobs, IndexedDB, and remote assets.
- **[Captioning Workflow](rules/captioning-workflow.md)**: Multi-stage transcription and subtitle editing.
