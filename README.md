# @remotion/editor-skill

An Agent Skill package that defines best practices for building video editors and interactive creation tools with [Remotion](https://remotion.dev).

## Installation

```bash
npx skills add remotion-dev/skills # Official skills
# Our custom skill (once published)
npx skills add your-username/remotion-editor
```

## Included Rules

- **State Optimization**: Performance patterns for complex UI.
- **Timeline Interactions**: Precise frame-to-pixel mapping and zooming.
- **Canvas Logic**: Coordinate transformation and spatial snapping.
- **Undo/Redo**: Reliable history management.
- **Asset Lifecycle**: Local-first caching with IndexedDB.
- **Editor-Remotion Sync**: Bridging editor data with Remotion compositions.

## Development

This skill was extracted from patterns found in the [Remotion Editor Starter](https://github.com/remotion-dev/editor-starter).
