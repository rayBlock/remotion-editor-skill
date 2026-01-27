---
name: canvas-logic
description: Handling interactive elements and spatial snapping on the canvas
metadata:
  tags: canvas, layout, snapping, transform
---

# Canvas Logic: Coordinates and Transforms

The canvas is a free-form area where Remotion compositions are rendered. It requires complex coordinate mapping between the "Screen" (pixels) and the "Composition" (composition units).

## The Rule

**Always work in Composition Units.** Normalize all mouse coordinates to the composition's width and height before updating state.

### 1. UV Coordinate Mapping

When zooming into a specific point on the canvas, calculate the "UV" (0 to 1) coordinate of the mouse relative to the composition.

```tsx
const uvX = mouseX / compositionWidth;
const uvY = mouseY / compositionHeight;

// Zoom centered on mouse
const zoomDiff = newZoom - oldZoom;
const correctionX = -uvX * (zoomDiff * compositionWidth);
```

### 2. Spatial Snapping

Just like the timeline has time-snapping, the canvas needs spatial snapping (edges, centers).

- **Center Snapping**: `0.5 * compositionWidth`
- **Edge Snapping**: `0` and `compositionWidth`
- **Object Snapping**: Bounding boxes of other layers.

### 3. Layer Management

Render the Remotion `<Player>` as a background layer, with an "Interaction Overlay" on top for handles and selection boxes.

```tsx
<div className="canvas-container">
  <Player {...props} /> {/* The Actual Visuals */}
  <InteractionOverlay>
    {selectedItems.map(id => <SelectionBox key={id} />)}
  </InteractionOverlay>
</div>
```

## Why this matters

If you update item positions in "pixels", the video will look different at different zoom levels. Always store `x`, `y`, `width`, and `height` in composition units.
