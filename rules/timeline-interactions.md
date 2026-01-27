---
name: timeline-interactions
description: Implementing seeking, snapping, and zooming in the timeline
metadata:
  tags: timeline, zooming, snapping, seeking
---

# Timeline Interactions

The timeline is the heart of the editor. It must handle frame-accurate positioning and provide "magnetic" feedback to the user.

## The Rule

**Decouple frames from pixels.** All timeline math should be based on a `pixelsPerFrame` ratio that is centrally managed.

### 1. Frame-to-Pixel Mapping

Use a CSS variable for the zoom level. This allows you to update the width of thousands of timeline elements via a single style change rather than thousands of React prop updates.

```tsx
// In the Timeline Container
const pixelsPerFrame = zoomLevel * BASE_WIDTH;
return (
  <div style={{ '--pixels-per-frame': pixelsPerFrame } as any}>
    {children}
  </div>
);

// In a Timeline Item
const width = item.durationInFrames * var(--pixels-per-frame);
```

### 2. Smooth Zooming

Use `flushSync` when updating zoom level if you need to perform scroll restoration immediately after the zoom.

```tsx
import { flushSync } from 'react-dom';

const updateZoom = (newZoom) => {
  const scrollOffset = getScrollRatio();
  flushSync(() => {
    setZoom(newZoom);
  });
  restoreScroll(scrollOffset);
};
```

### 3. Magnetic Snapping

Snapping should be "global". When dragging an item, check its start and end points against a sorted array of `snapPoints` (other items' boundaries, playhead, markers).

```tsx
const snapPoints = [0, playhead, ...itemBoundaries];
const findSnap = (time) => {
  return snapPoints.find(p => Math.abs(p - time) < SNAP_THRESHOLD);
}
```

## Why this matters

A professional editor needs to feel "precise". Without frame-accurate pixel mapping and snapping, it is impossible for users to perform clean cuts.
