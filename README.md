# Remotion Editor Skill

An Agent Skill package defining best practices for building production-grade video editors and interactive creation tools with [Remotion](https://remotion.dev).

## Overview

This skill provides a set of patterns and rules derived from the [Remotion Editor Starter](https://github.com/remotion-dev/editor-starter). It focuses on high-performance React patterns, complex timeline math, and robust asset management.

## Installation

To use this skill in your agent environment:

```bash
# Add this custom skill
npx skills add rayBlock/remotion-editor-skill
```

## Included Rules

| Category | Rule | Description |
| :--- | :--- | :--- |
| **Architecture** | [State Optimization](rules/state-optimization.md) | High-performance React patterns using granular contexts. |
| | [Undo/Redo](rules/undo-redo.md) | Efficient history management for complex project states. |
| | [Feature Flags](rules/feature-flags.md) | Scaling the editor with modular toggles. |
| **Interaction** | [Timeline Math](rules/timeline-math.md) | Frame-to-pixel translation and drag thresholds. |
| | [Timeline Zooming](rules/timeline-interactions.md) | Managing scroll restoration and scaling. |
| | [Canvas Logic](rules/canvas-logic.md) | Coordinate mapping (UV) and spatial transforms. |
| | [Keyboard Shortcuts](rules/keyboard-shortcuts.md) | Focus-aware hotkeys for cross-platform support. |
| **Backend & AI** | [Asset Lifecycle](rules/asset-lifecycle.md) | Local-first caching with IndexedDB. |
| | [Rendering Pipeline](rules/rendering-pipeline.md) | State-machine based export UI and polling. |
| | [Captioning](rules/captioning-workflow.md) | Multi-stage AI transcription pipelines. |
| | [Editor Sync](rules/editor-remotion-sync.md) | Bridging the editor with the Remotion Player. |

## Development

Contributions are welcome. This skill is designed to be used by AI coding agents to ensure consistency when building complex Remotion-based tools.
