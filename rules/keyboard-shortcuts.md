---
name: keyboard-shortcuts
description: Managing global hotkeys and focus-aware listeners
metadata:
  tags: [shortcuts, hotkeys, accessibility, ux]
---

# Keyboard Shortcuts: Global Hotkey Management

A professional video editor must support standard hotkeys (Space for play/pause, Cmd+Z for undo). However, these must not fire when the user is typing in a text input or textarea.

## The Rule

**Centralize shortcut logic in a hook that checks for input focus.**

### 1. Cross-Platform Modifier Keys
Always handle Mac (Command) vs Windows/Linux (Control) keys correctly.

```tsx
const isCommandKey = (e: KeyboardEvent) => {
  return window.navigator.platform.startsWith('Mac') ? e.metaKey : e.ctrlKey;
};
```

### 2. Focus-Aware Listeners
Prevent "Backspace" from deleting a video track when the user is trying to delete a character in a title field.

```tsx
const onKeyDown = (e: KeyboardEvent) => {
  const { activeElement } = document;
  const isInputFocused = activeElement instanceof HTMLInputElement || 
                         activeElement instanceof HTMLTextAreaElement;

  if (isInputFocused && !triggerInInput) return;
  
  if (e.key === ' ') {
    togglePlayback();
    e.preventDefault(); // Stop page from scrolling
  }
};
```

### 3. Cleanup
Always remove event listeners when the component unmounts to prevent memory leaks and "zombie" shortcuts.

```tsx
useEffect(() => {
  window.addEventListener('keydown', onKeyDown);
  return () => window.removeEventListener('keydown', onKeyDown);
}, [onKeyDown]);
```

## Why this matters
Users expect standard video editing shortcuts. If shortcuts are unreliable or conflict with text entry, the editor will feel broken and frustrating.
