---
name: state-optimization
description: Using the "Many Contexts" pattern for high-performance editors
metadata:
  tags: state, context, performance, react
---

# State Optimization: The "Many Contexts" Pattern

Video editors require high-frequency updates (e.g., updating the playhead 60 times per second) and complex state updates (e.g., moving 100+ items on a timeline). Putting all state in a single "God Object" will cause the entire application to re-render on every frame.

## The Rule

**Split your editor state into granular contexts.** Separate state that changes often from state that changes rarely.

### Recommended Context Split:

1.  **TimelineContext**: `durationInFrames` (Changes only on edit)
2.  **PlayheadContext**: `currentFrame` (Changes 60fps)
3.  **SelectionContext**: `selectedItems` (Changes on click)
4.  **ZoomContext**: `zoomLevel` (Changes on scroll)
5.  **UndoableStateContext**: `items`, `tracks` (The "Source of Truth")

### Example: Granular Provider Pattern

```tsx
// Separate Zoom from Main State
export const ZoomProvider = ({ children }) => {
  const [zoom, setZoom] = useState(1);
  return (
    <ZoomContext.Provider value={{ zoom, setZoom }}>
      {children}
    </ZoomContext.Provider>
  );
};
```

### Avoiding Re-renders with Imperative State

Use `useRef` to hold the "Source of Truth" state for imperative actions (like dragging) while using `useState` for React-driven UI updates.

```tsx
const imperativeState = useRef(state);
imperativeState.current = state; // Keep ref in sync

const moveItem = () => {
  const currentItems = imperativeState.current.items;
  // Perform math on currentItems...
}
```

## Why this matters

In a Remotion editor, seeking the timeline must be instantaneous. If the `Inspector` panel re-renders its 50+ input fields every time the playhead moves, the editor will feel laggy.
