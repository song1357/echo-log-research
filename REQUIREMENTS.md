# EchoLog: Product Requirements Document (PRD)

## 1. Product Vision
A **zero-latency, privacy-first voice journal** that turns unstructured rambling into structured, actionable insights using local AI.

## 2. Core Features (MVP)

### 2.1 The "Capture" Experience
*   **Global Hotkey**: `Cmd+Shift+R` to start/stop recording immediately from anywhere.
*   **Menu Bar Widget**: Visual indicator of recording status.
*   **Tech**: CoreAudio + `ffmpeg` for compression.

### 2.2 Local Intelligence Engine
*   **Transcription**: 
    *   Engine: `openai-whisper` (Python) or `whisper.cpp` (C++).
    *   Model: `base.en` or `small` for speed; `turbo` for quality.
*   **Processing**:
    *   Engine: `opencode` (via `codex` CLI or local API).
    *   Prompt Strategy: "Summarize this day, extract TODOs, and tag the emotional vibe."

### 2.3 Storage & Sync
*   **Format**: Plain Text / Markdown.
*   **Location**: `~/Documents/EchoLog` (User configurable).
*   **Sync**: Relies on system iCloud Drive / Dropbox (Hands-off approach).

## 3. User Flow
1. User presses Hotkey -> 🔴 Recording starts.
2. User speaks thoughts ("Had a tough meeting with Sarah, need to follow up on the Q3 report...").
3. User presses Hotkey -> ⏹️ Recording stops.
4. App runs background job:
    *   `whisper input.wav` -> `text`.
    *   `codex "Extract TODOs from: {text}"` -> `output`.
5. Notification pops up: "Journal saved + 1 TODO added."

## 4. Technical Architecture
*   **Frontend**: Electron (React) or Tauri (Rust) for lightweight UI.
*   **Backend**: Node.js (calling shell commands for Whisper/Codex).
*   **Database**: SQLite (for fast search) + File System (for portability).

## 5. Success Metrics
*   **Retention**: % of users who record >3 entries in first week.
*   **Privacy Trust**: Zero network requests to non-local servers (except initial model download).
