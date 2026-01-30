---
name: undo-redo
description: Implementing history management for complex video states
metadata:
  tags: [history, undo, redo, state]
---

# Undo/Redo: Managing Project History

A video project has a complex state (many items, many properties). Implementing a reliable undo/redo system is essential for user confidence.

## The Rule

**Explicitly separate Undoable State from Ephemeral State.**

### 1. The State Split

Only put data that represents the "Project Save File" into the history stack.

- **Undoable**: Items, Tracks, FPS, Dimensions.
- **Ephemeral (Exclude)**: Playhead position, Zoom level, Hover states, Selection.

### 2. Commit-based Updates

Instead of pushing every mouse movement to the history stack (which would fill it with 1,000 "move" states), only **commit** to the history on `onMouseUp`.

```tsx
const [state, setState] = useState(initialState);
const history = useRef([]);

const updateState = (newState, commit = false) => {
  setState(newState);
  if (commit) {
    history.current.push(newState.undoableState);
  }
}
```

### 3. Shallow Equality

Use an immutable state pattern (like `immer` or standard JS spreads) to make history snapshots memory-efficient. React will only re-render components whose specific data has changed.

## Why this matters

If a user accidentally deletes their main video track, they must be able to restore it instantly. A robust history system is the difference between a toy and a tool.
