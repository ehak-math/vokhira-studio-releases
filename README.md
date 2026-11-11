# Vokhira Studio — v0.4.22 Closed Beta Release Notes

**Product Name**: Vokhira Studio  
**Tagline**: *Give Every Story a Voice.*  
**Version**: `0.4.22` (Closed Beta Prerelease)  
**Platform**: Windows 10 / Windows 11 (64-bit / x64)  
**Application ID**: `com.vokhira.studio`  
**Release Date**: 2026-11-11

---

## 1. Overview

**Vokhira Studio v0.4.22** is the first standalone Windows x64 Closed Beta release under the **Vokhira Studio** identity (formerly *Khmer AI Dubbing Studio*).

This release packages the desktop application, a self-contained **Python 3.11.9** runtime, **FFmpeg / FFprobe 9.0.2** media binaries, and the AI worker pipeline into a single Windows installer (`Vokhira-Studio-Setup-v0.4.22.exe`). Testers do **not** need to install Node.js, Python, or FFmpeg separately.

---

## 2. What's Included in v0.4.22

### Video Import & Multi-Track Timeline
- Import local video files (`.mp4`, `.mov`, `.mkv`, `.webm`, `.m4v`, `.avi`) with automatic 20 ms waveform peak envelope generation and disk caching.
- Multi-track timeline supporting **Original Video/Audio**, **Khmer Voice**, **Music & Effects**, **Khmer Subtitles**, **Text Overlays**, and **Image Overlays**, with per-track visibility, mute, lock, and volume controls.
- Synchronized video preview with real-time Khmer audio scheduling, scrubbing, and frame-accurate transport controls.

### Chinese Speech Transcription (Offline ASR) & SRT Workflows
- Out-of-the-box CPU INT8 speech recognition powered by **Faster-Whisper** (`whisper-tiny`, `whisper-small`, `whisper-medium`, `whisper-large-v3-turbo`) with **Silero VAD** speech activity filtering and word-level timestamps.
- Warm background Whisper session daemon so consecutive chunks and retries reuse the loaded model in memory.
- Import existing Chinese `.srt` subtitle files (with UTF-8/BOM/CRLF/multiline validation) and export Chinese or Khmer `.srt` subtitles at any time.

### Chinese-to-Khmer AI Translation
- **Google Gemini API Translation**: Context-aware, batch-checkpointed Chinese-to-Khmer dialogue translation with custom translation rules, character glossary preservation, strict JSON schema validation, automatic `429` retry/backoff, and crash-safe resume.
- **Offline NLLB Translation**: Local fallback translation via `facebook/nllb-200-distilled-600M` (dynamic INT8 quantized on CPU).

### Khmer Voice Generation & Synchronization
- **Offline Khmer TTS**: Local synthesis via Meta MMS Khmer (`facebook/mms-tts-khm`) with pitch presets (`low`, `neutral`, `high`), rate/pitch/volume controls, and deterministic SHA-256 audio caching.
- **Online Microsoft Edge Khmer TTS**: Neural Khmer voices (`km-KH-PisethNeural`, `km-KH-SreymomNeural`) with automatic fallback to local MMS Khmer if offline.
- **Single-Sentence Audition**: Regenerate and audition individual dialogue lines without rebuilding the entire project voice track.
- **Independent Speed & Auto Align**: Per-clip speed calculation, silence-aware boundary alignment, and overlap conflict scanning across multi-thousand-clip timelines.

### MP4 Export & Project Persistence
- Hardware-friendly H.264/AAC `.mp4` export with burned-in styled Khmer subtitles, soft subtitle track (`mov_text`), image/text overlays, and post-render duration verification.
- Atomic `.tmp` project and checkpoint persistence in `%APPDATA%\Vokhira Studio` with automatic upgrade compatibility for existing `%APPDATA%\Khmer AI Dubbing Studio` and `%APPDATA%\storyrecap-ai-studio` user profiles.

---

## 3. Installer & Checksum

| Field | Value |
|---|---|
| **Installer Filename** | `Vokhira-Studio-Setup-v0.4.22.exe` |
| **Installer Size** | `339,889,324` bytes (`324.14 MB`) |
| **Architecture** | Windows x64 (`AMD64`) |
| **SHA-256 Checksum** | `3c1adeb71775fb6e1836397a3593a8dce044085b3fe5b69f4059467b4ee8c650` |
| **Code Signing Status** | **Unsigned** (Closed Beta build — Windows SmartScreen prompt expected on first run) |

Verify the downloaded installer in PowerShell before running:

```powershell
Get-FileHash .\Vokhira-Studio-Setup-v0.4.22.exe -Algorithm SHA256
```

---

## 4. System Requirements

- **OS**: Windows 10 (64-bit, version 1903+) or Windows 11 (64-bit)
- **CPU**: 4+ cores / 8+ threads x64 processor recommended
- **RAM**: `8 GB` minimum (`16 GB` recommended for `whisper-medium`, `whisper-large-v3-turbo`, or offline `nllb`)
- **Graphics**: Integrated graphics or discrete GPU (all bundled AI inference runs on CPU out of the box)
- **Disk Space**:
  - `~1.2 GB` for the installed application (`resources/python`, `resources/ffmpeg`, `resources/app.asar`)
  - `2 GB – 8 GB` free in `%APPDATA%` (`C:\Users\<User>\AppData\Roaming\Vokhira Studio`) for downloaded AI models, waveform caches, and project audio
- **Internet Connection**:
  - **Required** for: initial AI model downloads from Hugging Face, Google Gemini API translation, and Microsoft Edge Neural TTS (`km-KH-PisethNeural` / `km-KH-SreymomNeural`).
  - **Not Required** (works 100% offline once models are installed) for: video import, SRT import/export, Whisper ASR transcription, offline Meta MMS Khmer TTS (`khmer-tts`), offline NLLB translation (`nllb`), timeline editing, Auto Align, and MP4 export.

---

## 5. Companion Beta Documentation

- [Installation & First-Launch Guide](file:///d:/A%20Video%20Shorts/storyrecap-ai-offline/docs/beta/INSTALLATION_GUIDE.md)
- [Known Issues & Limitations](file:///d:/A%20Video%20Shorts/storyrecap-ai-offline/docs/beta/KNOWN_ISSUES.md)
- [Closed Beta Testing Plan & Checklist](file:///d:/A%20Video%20Shorts/storyrecap-ai-offline/docs/beta/TESTING_CHECKLIST.md)
- [Beta Feedback & Bug Report Template](file:///d:/A%20Video%20Shorts/storyrecap-ai-offline/docs/beta/FEEDBACK_TEMPLATE.md)

