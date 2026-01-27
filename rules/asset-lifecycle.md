---
name: asset-lifecycle
description: Managing remote assets and local caching for video editing
metadata:
  tags: assets, indexeddb, caching, blob
---

# Asset Lifecycle: Local-First Editing

Video assets are large. A web-based editor must cache these assets locally to prevent lag and high bandwidth usage during playback and seeking.

## The Rule

**Use IndexedDB as an Asset Cache.** Proxy all remote asset URLs through a local caching layer that stores blobs.

### 1. Transparent Caching Pattern

When an asset is added to the editor:
1.  Check if `assetId` exists in **IndexedDB**.
2.  If yes, create a `URL.createObjectURL(blob)` and use it as the `src`.
3.  If no, fetch the remote URL, store the blob in IndexedDB, and then create the blob URL.

```tsx
// caching/load-asset.ts
export const getAssetSrc = async (assetId, remoteUrl) => {
  const cached = await db.get(assetId);
  if (cached) return URL.createObjectURL(cached);
  
  const blob = await fetch(remoteUrl).then(r => r.blob());
  await db.put(assetId, blob);
  return URL.createObjectURL(blob);
}
```

### 2. Cleaning Up

Always revoke blob URLs when they are no longer needed to prevent memory leaks.

```tsx
useEffect(() => {
  const url = URL.createObjectURL(blob);
  setSrc(url);
  return () => URL.revokeObjectURL(url);
}, [blob]);
```

### 3. Mediabunny Integration

Use `mediabunny` to pre-calculate durations and dimensions before adding assets to the timeline. This ensures the UI is ready immediately without waiting for the `<Video>` tag to load.

## Why this matters

Waiting for a 500MB video to buffer every time you seek makes an editor unusable. Local caching makes web-based video editing feel like a desktop app.
