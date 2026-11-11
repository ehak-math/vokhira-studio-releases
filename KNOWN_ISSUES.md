# Vokhira Studio — Known Issues & Beta Limitations

**Product**: Vokhira Studio  
**Current Release**: `v0.4.22` (Public Beta)  
**Last Updated**: 2026-11-11  

This document tracks verified limitations, confirmed issues, and active workarounds for Vokhira Studio. Every item listed here has been verified through automated QA and integration testing.

---

## 1. Confirmed Issues & Workarounds

### 1.1 Unsigned Installer Triggers Windows SmartScreen
- **Issue ID**: `ISSUE-01`
- **Affected Version**: `v0.4.22`
- **Severity**: Low (Informational / Expected for Beta)
- **Status**: Open (Expected until enterprise certificate is provisioned)
- **Description**:
  When launching `Vokhira-Studio-Setup-v0.4.22.exe`, Microsoft Defender SmartScreen displays a blue dialog stating *"Windows protected your PC — Microsoft Defender SmartScreen prevented an unrecognized app from starting"*.
- **Cause**:
  The Beta build is not digitally signed with an enterprise commercial Authenticode certificate with established Microsoft SmartScreen reputation.
- **Verified Workaround**:
  Verify the installer SHA-256 hash in PowerShell:
  ```powershell
  Get-FileHash .\Vokhira-Studio-Setup-0.4.22.exe -Algorithm SHA256
  ```
  Expected hash:
  `3c1adeb71775fb6e1836397a3593a8dce044085b3fe5b69f4059467b4ee8c650`  
  Click **More info** on the SmartScreen dialog, verify the application name, and click **Run anyway**.

---

### 1.2 Inner Executable File Description Displays "Electron" in Task Manager
- **Issue ID**: `QA-ISS-01`
- **Affected Version**: `v0.4.22`
- **Severity**: Trivial (Cosmetic only)
- **Status**: Documented / Scheduled for future packaging update
- **Description**:
  While the installer filename (`Vokhira-Studio-Setup-v0.4.22.exe`), window title, Start Menu entry, Desktop shortcut, and taskbar icon correctly display **Vokhira Studio**, viewing the executable properties (`Properties` → `Details`) or Windows Task Manager details tab shows `File description: Electron`.
- **Cause**:
  Executable resource editing was bypassed during unsigned packaging (`signAndEditExecutable=false`) to ensure binary build determinism.
- **Workaround**:
  None needed. Application behavior, features, and performance are entirely unaffected.

---

### 1.3 Optional Secondary AI Environments Not Bundled in Base Installer
- **Issue ID**: `DESIGN-01`
- **Affected Version**: `v0.4.22`
- **Severity**: Informational (By Design)
- **Status**: Expected Behavior
- **Description**:
  Selecting optional secondary engines such as **SenseVoice Small**, **FunASR Paraformer**, **Demucs Vocal Separation**, or **PaddleOCR Video Subtitle OCR** displays an informational notification indicating that those optional runtimes are not pre-installed.
- **Cause**:
  To maintain a lightweight standalone installer (`~324 MB`) rather than a multi-gigabyte package, only the primary production pipeline is bundled:
  - **Faster-Whisper (INT8 CPU)** + **Silero VAD**
  - **Meta MMS Khmer TTS**
  - **Microsoft Edge Neural TTS**
  - **Meta NLLB-200**
  - **FFmpeg 9.0.2**
- **Verified Workaround**:
  - For Chinese speech recognition, use the bundled Whisper models (`whisper-tiny`, `whisper-small`, `whisper-medium`, `whisper-large-v3-turbo`) or import a pre-existing `.srt` subtitle file.
  - For background audio mixing, use the multi-track timeline volume sliders for the **Original Audio** and **Music & Effects** tracks.

---

### 1.4 Offline Khmer TTS Uses Pitch Variations Rather Than Separate Voices
- **Issue ID**: `LIMIT-01`
- **Affected Version**: `v0.4.22`
- **Severity**: Moderate (Model Architecture Limitation)
- **Status**: Active (Model Limitation)
- **Description**:
  When using the offline Meta MMS Khmer engine (`facebook/mms-tts-khm`), speaker profiles are differentiated via pitch and rate modulation (`low`, `neutral`, `high`) rather than distinct multi-actor voice timbres.
- **Cause**:
  The underlying Meta MMS Khmer neural checkpoint is a single-speaker acoustic model.
- **Verified Workaround**:
  If connected to the internet, select **Microsoft Edge Neural TTS** in the Voice settings. This provides distinct, natural male (`km-KH-PisethNeural`) and female (`km-KH-SreymomNeural`) neural voices. If offline, the application falls back smoothly to Meta MMS Khmer.

---

### 1.5 Initial Audio Synthesis Latency on Cold Start
- **Issue ID**: `PERF-01`
- **Affected Version**: `v0.4.22`
- **Severity**: Low (Cold-Start Overhead)
- **Status**: Mitigated via Memory Caching
- **Description**:
  Synthesizing the first dialogue line after launching the application or after switching voice models takes between 15 and 25 seconds before audio begins playback.
- **Cause**:
  PyTorch and the neural model weights are dynamically loaded into memory during the initial synthesis call.
- **Verified Workaround**:
  Subsequent lines in the batch, as well as subsequent auditions and adjustments, synthesize rapidly (typically under 1 second per line) because the model remains warm in memory and identical lines leverage deterministic SHA-256 audio disk caching.

---

### 1.6 Google Gemini API Free-Tier Rate Limits (`HTTP 429`)
- **Issue ID**: `NET-01`
- **Affected Version**: `v0.4.22`
- **Severity**: Moderate (Third-Party API Constraint)
- **Status**: Mitigated by Architecture
- **Description**:
  Translating long scripts with hundreds of dialogue lines using a free-tier Google Gemini API key may occasionally encounter rate limit errors (`429 Resource Exhausted`).
- **Cause**:
  Google AI Studio imposes requests-per-minute (RPM) and tokens-per-minute (TPM) limits on non-commercial API keys.
- **Verified Workaround**:
  Vokhira Studio implements automatic exponential backoff retry and persists translations in 30-line atomic batches. If translation pauses due to quota exhaustion, simply wait 60 seconds and click **Translate** again; translation automatically resumes from the last saved batch without repeating completed lines.

---

## 2. Reporting New Issues

If you encounter a defect not documented above:
1. Search existing reports in the [GitHub Issues tracker](https://github.com/ehak-math/vokhira-studio-releases/issues).
2. If the issue is new, file a detailed report using the **[Bug Report Template](https://github.com/ehak-math/vokhira-studio-releases/issues/new?template=bug_report.yml)**.
3. Consult the **[Support Guide](SUPPORT.md)** for instructions on collecting non-sensitive diagnostic logs.