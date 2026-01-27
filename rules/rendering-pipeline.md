---
name: rendering-pipeline
description: Implementing a robust state machine for video exports
metadata:
  tags: rendering, lambda, progress, async
---

# Rendering Pipeline: The Export State Machine

Exporting a video is a long-running async operation. The UI must transition smoothly through various states to keep the user informed.

## The Rule

**Model the rendering process as a 4-state machine.** Avoid simple "loading" booleans.

### 1. The States
- **Initiated**: The request was sent to the server.
- **In-Progress**: The server is rendering frames (show percentage).
- **Done**: The file is ready (provide download link).
- **Error**: Something went wrong (show error message).

### 2. Polling for Progress
Since HTTP requests can time out, use a polling mechanism to check render status every 250ms–1000ms.

```tsx
const pollProgress = async (renderId) => {
  const res = await fetch(`/api/progress?id=${renderId}`);
  const status = await res.json();

  if (status.type === 'done') {
    updateState({ type: 'done', url: status.url });
    return;
  }

  if (status.type === 'in-progress') {
    updateState({ type: 'in-progress', progress: status.progress });
    setTimeout(() => pollProgress(renderId), 500); // Poll again
  }
};
```

### 3. Error Handling
Always catch network errors and server-side render failures. Inform the user whether the error is transient or permanent.

## Why this matters
Video rendering can take minutes. Without a clear state machine and progress updates, users will think the application has crashed and will refresh the page, potentially wasting compute resources.
