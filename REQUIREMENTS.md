# EchoLog: Product Requirements Document (PRD) v2
**Based on:** Market Feasibility Study (Feb 2026)

## 1. Product Vision
**EchoLog** is a "Zero-Knowledge" AI Voice Journal. It empowers privacy-conscious professionals to capture thoughts, track mental health, and structure their lives without sending a single byte of private data to the cloud.

## 2. Core Value Proposition (USP)
1.  **Local-First AI**: All transcription (Whisper) and analysis (LLM) happen on-device.
2.  **Voice-to-Insight**: Not just "Speech-to-Text", but "Speech-to-Structure" (Action items, Emotion tags, Summaries).
3.  **Markdown Native**: Users own their data (plain text files), compatible with Obsidian/Logseq.

## 3. Core Features (MVP)

### 3.1 The "Capture" Experience
*   **Global Hotkey**: `Cmd+Shift+R` (Instant record).
*   **Status Bar**: Minimal UI (Recording dot).
*   **Background Processing**: Recording continues even if window is closed.

### 3.2 The Local Intelligence Engine
*   **Transcription**: 
    *   **Engine**: `openai-whisper` (Python) or `whisper.cpp`.
    *   **Optimization**: Use Apple CoreML / Metal acceleration where possible.
*   **Analysis**:
    *   **Engine**: `codex` (Local Mode) or `Ollama`.
    *   **Task**: Extract "Mood", "Topics", "Action Items".

### 3.3 The "Dashboard" (Mental Health)
*   **Weekly Review**: A generated summary of the week's emotional trends.
*   **Privacy Dial**: A visual indicator showing "Offline Mode Active".

## 4. Technical Architecture
*   **App Shell**: **Tauri** (Rust) for security and small binary size (vs Electron).
*   **Database**: SQLite for metadata; File System for content (`.md` files).
*   **Bridging**: Tauri Sidecar -> Python/C++ binaries for AI.

## 5. Roadmap
*   **Phase 1 (MVP)**: Record -> Local Transcribe -> Markdown File.
*   **Phase 2**: Local LLM Integration (Summarization).
*   **Phase 3**: iOS Companion App (Sync via iCloud).

## 6. Success Metrics
*   **Trust**: 0 Data Leaks.
*   **Performance**: Transcription < 0.5x realtime (e.g., 1 min audio transcribed in <30s).
