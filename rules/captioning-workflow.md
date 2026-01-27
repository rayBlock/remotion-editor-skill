---
name: captioning-workflow
description: Managing multi-stage background tasks for AI captions
metadata:
  tags: captions, whisper, ai, tasks
---

# Captioning Workflow: Multi-Stage AI Tasks

Generating captions involves several distinct stages. Because this process is slow and compute-heavy, it should be managed as a series of background tasks.

## The Rule

**Pipeline the transcription process to minimize latency.**

### 1. The Pipeline Stages
1.  **Extract Audio**: Extract a lightweight WAV/MP3 from the video in the browser to save bandwidth.
2.  **Upload**: Upload the audio to a cloud storage (S3) for server-side processing.
3.  **Transcribe**: Trigger an AI (like Whisper) to generate JSON timestamps.
4.  **Map**: Convert the AI JSON into Remotion-friendly `<Caption>` components.

### 2. Non-Blocking UX
Allow the user to keep editing other parts of the video while the captioning task runs in the background. Use a "Task Indicator" or "Toaster" to show progress.

### 3. Audio Extraction in Browser
Do not upload the full 4K video file just to get captions. Use the Web Audio API or a library like `mediabunny` to extract only the audio track.

```tsx
// Example using Web Audio API
const audioCtx = new AudioContext();
const source = audioCtx.createMediaElementSource(videoElement);
const destination = audioCtx.createMediaStreamDestination();
// ... Record to Blob and Upload
```

## Why this matters
AI transcription is expensive and slow. Optimizing the data transfer (uploading audio only) and providing a non-blocking UI makes the feature feel premium and responsive.
