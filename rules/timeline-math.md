---
name: timeline-math
description: Best practices for frame-to-pixel translation and dragging
metadata:
  tags: [math, timeline, dragging, snapping]
---

# Timeline Math: Frames and Pixels

To build a draggable timeline, you must translate screen coordinates (pixels) into temporal positions (frames) accurately.

## The Rule

**Use a "Visible Frames" window for all spatial math.**

### 1. The Core Formula
To find the frame under the mouse, use the ratio of the horizontal offset to the total width of the timeline container.

```tsx
// deltaX: Pixels moved
// timelineWidth: Width of the visible timeline area
// visibleFrames: Number of frames currently in view

const frameOffset = Math.round((deltaX / timelineWidth) * visibleFrames);
```

### 2. Move Threshold
Do not start a drag operation immediately on `onMouseDown`. Use a small threshold (e.g., 4px) to distinguish between an intentional drag and an accidental slight movement during a click.

```tsx
const DRAG_THRESHOLD = 4;
if (Math.abs(currentX - startX) > DRAG_THRESHOLD) {
  setIsDragging(true);
}
```

### 3. Magnetic Snapping Math
When snapping, convert the `thresholdInPixels` to `thresholdInFrames` to ensure snapping feels consistent at different zoom levels.

```tsx
const snapThresholdInFrames = (thresholdInPixels / timelineWidth) * visibleFrames;

const bestSnap = snapPoints.find(p => Math.abs(p - targetFrame) < snapThresholdInFrames);
```

## Why this matters
Consistent math ensures that items always land exactly on frame boundaries. Without a move threshold, users will find it impossible to "select" an item without accidentally moving it by 1 or 2 frames.
