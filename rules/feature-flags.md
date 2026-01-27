---
name: feature-flags
description: Scaling an editor codebase with togglable features
metadata:
  tags: architecture, flags, scale
---

# Feature Flags: Building a Modular Editor

As a video editor grows, it can become cluttered with 100+ experimental or niche features. Feature flags allow you to keep the core engine clean while scaling functionality.

## The Rule

**Define all capabilities as toggleable constants.**

### 1. Central Flag Registry
Create a single file (e.g., `flags.ts`) that exports all feature toggles.

```tsx
export const FEATURE_TIMELINE_SNAPPING = true;
export const FEATURE_AUDIO_WAVEFORM = true;
export const FEATURE_CANVAS_MARQUEE = false; // Experimental
```

### 2. Conditional Rendering
Use these flags to prune the UI and logic at compile-time (or runtime).

```tsx
return (
  <div className="timeline">
    <Items />
    {FEATURE_TIMELINE_SNAPPING && <SnapIndicators />}
  </div>
);
```

### 3. Progressive Adoption
When adding a new, complex feature (like a "Solid Drawing Tool"), wrap it in a flag. This allows you to merge code frequently without breaking the "stable" version of the editor for other users.

## Why this matters
Feature flags enable "Clean Architecture". They force you to think about features as modular plugins rather than hard-coded logic. This makes the codebase easier to test, debug, and customize for different user types.
