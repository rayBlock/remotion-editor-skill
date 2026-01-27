---
name: editor-remotion-sync
description: Synchronizing editor state with Remotion compositions and the Player
metadata:
  tags: sync, inputProps, player, composition
---

# Editor-Remotion Synchronization

The editor's job is to manipulate data that Remotion then renders. This requires a bridge between the Editor State and the Remotion Composition.

## The Rule

**Use a "Bridge" component to map Editor State to Input Props.** Never pass the raw editor state directly into the composition if it contains ephemeral UI data.

### 1. The Input Props Bridge

Map your `UndoableState` to a clean object that matches your composition's Zod schema.

```tsx
const { undoableState } = useFullState();

const inputProps = useMemo(() => ({
  tracks: undoableState.tracks,
  items: undoableState.items,
  theme: undoableState.theme,
}), [undoableState]);

return (
  <Player
    component={MyComposition}
    inputProps={inputProps}
    durationInFrames={duration}
    fps={fps}
    compositionWidth={width}
    compositionHeight={height}
  />
);
```

### 2. Dynamic Composition Metadata

If your editor allows users to change the video's FPS, width, or height, you must pass these as top-level props to the `<Player />` and `<Composition />`.

### 3. Seek Synchronization

When the user seeks in the timeline, you must call `playerRef.current.seekTo(frame)`. Conversely, when the player is playing, the timeline playhead must follow the player's current frame.

```tsx
// Sync Playhead to Player
usePlayerFrame((frame) => {
  setTimelinePlayhead(frame);
});
```

## Why this matters

Remotion compositions should be "pure" functions of their `inputProps`. By keeping the bridge clean, you ensure that "what you see in the editor" is exactly "what gets rendered" in the final video file.
