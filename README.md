# @remotion/editor-skill

An Agent Skill package that defines best practices for building video editors and interactive creation tools with [Remotion](https://remotion.dev).

## Installation

```bash
npx skills add remotion-dev/skills # Official skills
# Our custom skill (once published)
npx skills add your-username/remotion-editor
```

## Included Rules

### Architecture
- **State Optimization**: High-performance React patterns for IDEs.
- **Undo/Redo**: Robust history management for complex states.
- **Feature Flags**: Scaling your editor with modular toggles.

### Interaction
- **Timeline Math**: Converting pixels to frames and handling drag thresholds.
- **Timeline & Zooming**: Managing scroll restoration and scaling.
- **Canvas Logic**: Coordinate mapping (UV) and spatial transforms.
- **Keyboard Shortcuts**: Focus-aware hotkeys for Mac and PC.

### Backend & AI
- **Asset Lifecycle**: Local-first caching with IndexedDB.
- **Rendering Pipeline**: State-machine based export UI.
- **Captioning Workflow**: Multi-stage AI transcription pipelines.
- **Editor-Remotion Sync**: Bridging the editor with the Remotion Player.

## Development

This skill was extracted from patterns found in the [Remotion Editor Starter](https://github.com/remotion-dev/editor-starter).
