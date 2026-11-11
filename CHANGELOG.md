# Changelog

All notable changes to **Vokhira Studio** will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Planned
- Enterprise Authenticode digital code signing for seamless Windows SmartScreen bypass.
- Expanded multi-speaker voice profiles and neural emotion controls.
- Direct GPU acceleration support for Faster-Whisper on NVIDIA hardware.

---

## [0.4.22] - 2026-11-11

**Initial Public Beta Prerelease** under the new **Vokhira Studio** identity (*formerly Khmer AI Dubbing Studio*).

### Added
- **Vokhira Studio Brand & Design**: Rebranded application identity, new visual assets, splash screen, and refreshed dark-mode editor styling.
- **Standalone Windows Distribution**: Single-file NSIS installer (`Vokhira-Studio-Setup-v0.4.22.exe`) bundling:
  - Isolated **Python 3.11.9** runtime (no external Python installation required).
  - Pinned **FFmpeg & FFprobe 9.0.2** media tools.
- **Offline Speech Recognition (ASR)**:
  - Local CPU INT8 transcription using **Faster-Whisper** (`whisper-tiny`, `whisper-small`, `whisper-medium`, `whisper-large-v3-turbo`).
  - Integrated **Silero VAD** for voice activity detection and silence filtering.
  - Warm background Whisper daemon with loopback socket reuse for fast consecutive segment transcription.
- **Dialogue Translation System**:
  - Contextual **Google Gemini API** translation with JSON schema validation, automatic rate-limit backoff, and 30-line batch checkpointing.
  - Offline fallback translation using **Meta NLLB-200** (`facebook/nllb-200-distilled-600M` INT8).
- **Khmer Neural Voice Synthesis**:
  - Online **Microsoft Edge Neural TTS** integration (`km-KH-PisethNeural` and `km-KH-SreymomNeural`).
  - Offline **Meta MMS Khmer TTS** engine (`facebook/mms-tts-khm`) with pitch/speed presets (`low`, `neutral`, `high`).
  - Single-sentence audition feature for instantaneous clip regeneration.
  - Deterministic SHA-256 audio disk caching.
- **Multi-Track Timeline Editor**:
  - Dedicated tracks: Original Audio/Video, Khmer Voice, Music & Effects, Subtitles, and Overlays.
  - Individual track volume, mute, solo, and lock controls.
  - 20 ms waveform peak envelope generation with disk caching.
  - Boundary Auto Align and conflict detection for multi-thousand-clip timelines.
- **Production MP4 Export**:
  - H.264/AAC MP4 video rendering with burned-in styled Khmer typography.
  - Optional soft subtitle track (`mov_text`) and image/text overlays.
- **In-App Model Manager**:
  - On-demand download, verification, and repair for AI models with SHA-256 integrity checks.
- **Automated Update Mechanism**:
  - Native integration with the public GitHub Releases distribution channel.

### Changed
- Re-architected storage directory to `%APPDATA%\Vokhira Studio` with backward-compatible migration for legacy `%APPDATA%\Khmer AI Dubbing Studio` and `%APPDATA%\storyrecap-ai-studio` profiles.
- Relocated runtime binaries into dedicated, isolated `resources/` directory.

### Security
- Google Gemini API key encryption using native **Windows Data Protection API (DPAPI)** at `%APPDATA%\Vokhira Studio\credentials\gemini-key.bin`.
- Strictly eliminated credential and private token logging across all application subroutines.