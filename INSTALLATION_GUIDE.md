# Vokhira Studio — Installation & Setup Guide

**Product**: Vokhira Studio  
**Target Platform**: Windows 10 / Windows 11 (64-bit / x64)  
**Package Type**: Standalone Windows NSIS Installer  

---

## Table of Contents

1. [System Requirements](#1-system-requirements)
2. [Downloading the Official Installer](#2-downloading-the-official-installer)
3. [Verifying the SHA-256 Checksum](#3-verifying-the-sha-256-checksum)
4. [Running the Installer & Windows SmartScreen](#4-running-the-installer--windows-smartscreen)
5. [First-Launch Configuration](#5-first-launch-configuration)
6. [Internet vs. Offline Capabilities](#6-internet-vs-offline-capabilities)
7. [Software Updates](#7-software-updates)
8. [Uninstalling Vokhira Studio](#8-uninstalling-vokhira-studio)
9. [Project Data, Credentials & Storage Architecture](#9-project-data-credentials--storage-architecture)
10. [Troubleshooting Common Issues](#10-troubleshooting-common-issues)

---

## 1. System Requirements

Before installing, ensure your PC meets the following hardware and software specifications:

| Requirement | Minimum | Recommended |
|---|---|---|
| **Operating System** | Windows 10 64-bit (Version 1903 or later) | Windows 11 64-bit (Latest build) |
| **Processor (CPU)** | 4 physical cores (e.g., Intel Core i3 / AMD Ryzen 3) | 6 to 8 physical cores with AVX2 instruction support |
| **System Memory (RAM)** | 8 GB RAM | 16 GB or higher |
| **Disk Space** | 4 GB free space on system drive (`C:`) | 15 GB+ free SSD space for video and model caches |
| **Display Resolution** | 1280 x 720 minimum | 1920 x 1080 (Full HD) or higher |
| **Internet Connection** | Required for initial setup and online voices | Broadband connection |

> **Note on Dependencies**: Vokhira Studio packages its own isolated Python 3.11 runtime and FFmpeg 9.0.2 binaries. You do **not** need to install Python, Node.js, Git, or FFmpeg on your operating system.

---

## 2. Downloading the Official Installer

Always download Vokhira Studio exclusively from the official GitHub Releases page:

🔗 **[https://github.com/ehak-math/vokhira-studio-releases/releases](https://github.com/ehak-math/vokhira-studio-releases/releases)**

Under the **Assets** section of the latest release, download both:
1. `Vokhira-Studio-Setup-<version>.exe` (The primary installer, ~324 MB)
2. `Vokhira-Studio-Setup-<version>.exe.sha256` (The verification checksum file)

*(If a release has just been tagged and is currently building in CI, release assets will appear once the build job completes.)*

---

## 3. Verifying the SHA-256 Checksum

To guarantee the integrity and authenticity of your download, verify its cryptographic hash before executing:

1. Open **Windows PowerShell** (or Terminal).
2. Change directory to your `Downloads` folder:
   ```powershell
   cd "$HOME\Downloads"
   ```
3. Run `Get-FileHash` on the downloaded installer:
   ```powershell
   Get-FileHash .\Vokhira-Studio-Setup-*.exe -Algorithm SHA256
   ```
4. Compare the resulting hash against the value published on the GitHub release page and inside the `.sha256` file:
   - For version `0.4.22`:
     ```text
     3c1adeb71775fb6e1836397a3593a8dce044085b3fe5b69f4059467b4ee8c650
     ```

If the checksum does not match, delete the file and download it again.

---

## 4. Running the Installer & Windows SmartScreen

### 4.1 Windows SmartScreen Prompt
Because early Beta versions are not signed with an enterprise commercial Authenticode certificate, Windows Defender SmartScreen may display an informational warning:

> *"Windows protected your PC — Microsoft Defender SmartScreen prevented an unrecognized app from starting."*

This is standard Windows behavior for newly released software without accumulated digital certificate reputation.

**To safely proceed:**
1. Click the **"More info"** text link in the blue SmartScreen dialog.
2. Confirm that the App name is `Vokhira-Studio-Setup-<version>.exe`.
3. Click the **"Run anyway"** button.

> ⚠️ **Important Security Notice**: Never disable Microsoft Defender Antivirus or disable SmartScreen permanently. Proceeding past this prompt on verified software is standard for open beta software, but your system protection should always remain enabled.

### 4.2 Installation Options
- **Installation Scope**: You can install Vokhira Studio for the current user (`%LOCALAPPDATA%\Programs\Vokhira Studio`, no administrator privileges required) or for all users on the machine.
- **Shortcuts**: The installer creates shortcuts on your Desktop and in your Start Menu.
- Click **Install** and allow setup to complete (~15–30 seconds on an SSD).

---

## 5. First-Launch Configuration

When you launch Vokhira Studio for the first time, complete the two setup steps below to prepare your dubbing workflow:

### Step 5.1 — Download AI Models (One-Time Setup)
To keep the installer under 350 MB, large neural network weights are downloaded inside the application on demand.

1. Open **Vokhira Studio**.
2. Click **Settings** (gear icon) in the navigation bar, then select **AI Models**.
3. Choose the models suited for your workflow:
   - **Recommended Starter Pack (`~680 MB`)**:
     - **`whisper-small`** (`~464 MB`): High-accuracy Chinese speech-to-text with moderate RAM usage. *(For lower-spec laptops, `whisper-tiny` at `~75 MB` is also available).*
     - **`khmer-tts`** (`~139 MB`): Local Meta MMS Khmer offline voice engine (`facebook/mms-tts-khm`).
   - **Optional Advanced Models**:
     - **`whisper-medium`** (`~1.46 GB`) or **`whisper-large-v3-turbo`** (`~1.55 GB`): Maximum Chinese transcription accuracy.
     - **`nllb`** (`~2.37 GB`): Meta NLLB-200 offline Chinese-to-Khmer translation engine (only needed if translating without a Gemini API key).
4. Click **Install** next to each desired model. Vokhira Studio automatically verifies downloaded file hashes before activation.

### Step 5.2 — Configure Google Gemini API Key (Recommended for Translation)
For optimal contextual translation quality:
1. Obtain an API key from [Google AI Studio](https://aistudio.google.com/).
2. In Vokhira Studio, open **Preferences** → **Gemini API**.
3. Paste your API key and click **Save**.
4. The key is encrypted using Windows DPAPI and stored only on your local machine.

---

## 6. Internet vs. Offline Capabilities

Vokhira Studio is designed to maximize offline autonomy while providing cloud connectivity for advanced AI models:

| Feature / Task | Requires Internet? | Notes |
|---|---|---|
| **Initial Model Downloads** | **Yes (One-Time)** | Downloads weights from Hugging Face |
| **Whisper Chinese Transcription** | **No (100% Offline)** | Executes entirely locally on CPU |
| **SRT Subtitle Import / Export** | **No (100% Offline)** | Native file processing |
| **Google Gemini Translation** | **Yes** | Communicates directly with Google Gemini API |
| **NLLB Offline Translation** | **No (100% Offline)** | Runs locally once `nllb` model is installed |
| **Microsoft Edge Neural TTS** | **Yes** | Streams natural Khmer neural voices (`Piseth` / `Sreymom`) |
| **Meta MMS Khmer TTS** | **No (100% Offline)** | Runs locally once `khmer-tts` model is installed |
| **Timeline Editing & Auto Align** | **No (100% Offline)** | Real-time local audio/video manipulation |
| **MP4 Video & Subtitle Export** | **No (100% Offline)** | Renders via bundled local FFmpeg binary |

---

## 7. Software Updates

Vokhira Studio includes an integrated updater that periodically queries the public release feed:

1. When a new version is published to GitHub Releases, Vokhira Studio displays an update banner.
2. Clicking **Check for Updates** in the Help or About menu manually queries the release channel.
3. When you choose to update, the new installer is downloaded and verified automatically.
4. During updates, all existing user projects, preferences, and downloaded AI models remain intact.

---

## 8. Uninstalling Vokhira Studio

To remove Vokhira Studio:
1. Close the application.
2. Open Windows **Settings** → **Apps** → **Installed apps** (or **Add or Remove Programs**).
3. Search for **Vokhira Studio** and select **Uninstall**.
4. Alternatively, execute `Uninstall Vokhira Studio.exe` located in your installation directory.

### What is Kept vs. Removed
- **Removed**: Program binaries, Electron files, bundled Python runtime, bundled FFmpeg, and application shortcuts.
- **Preserved**: Your user projects, custom dictionaries, and downloaded multi-gigabyte AI models in `%APPDATA%\Vokhira Studio` are preserved by default to prevent accidental data loss.
- **Complete Clean Removal**: If you wish to delete all project files and downloaded AI models as well, manually delete the `%APPDATA%\Vokhira Studio` folder after running the uninstaller.

---

## 9. Project Data, Credentials & Storage Architecture

Vokhira Studio follows clean Windows application standards:

```text
%LOCALAPPDATA%\Programs\Vokhira Studio\    # Application binaries (read-only)
├── Vokhira Studio.exe
└── resources\
    ├── app.asar                          # Application UI and controller
    ├── ffmpeg\                           # Bundled FFmpeg & FFprobe 9.0.2
    └── python\                           # Relocatable Python 3.11 runtime

%APPDATA%\Vokhira Studio\                  # Mutable user data directory
├── projects.json                         # Project library index
├── settings.json                         # User preferences
├── credentials\
│   └── gemini-key.bin                    # Windows DPAPI encrypted API key
├── models\                               # Downloaded neural network weights
├── analysis\<projectId>\                 # Project timeline, audio, and cache
└── logs\                                 # Diagnostic application logs
```

- **Legacy Migration**: If you previously used *Khmer AI Dubbing Studio* or *storyrecap-ai-studio*, Vokhira Studio automatically detects and adopts existing user directories, ensuring zero data loss.
- **DPAPI Protection**: Sensitive secrets (such as API keys) are encrypted with the Windows DPAPI mechanism tied to your Windows user account.

---

## 10. Troubleshooting Common Issues

### 10.1 "SmartScreen prevented an unrecognized app from starting"
Follow [Section 4.1](#4-running-the-installer--windows-smartscreen). Verify the SHA-256 hash, click **More info**, then click **Run anyway**.

### 10.2 Windows Firewall Prompt for `python.exe`
When running local Whisper transcription, the application initiates an internal background process on loopback address `127.0.0.1` to keep the model warm in memory. If Windows Firewall prompts you, allow access for private/local networks. The background process never listens on external network interfaces.

### 10.3 "Model is not installed or manifest invalid"
Open **Settings** → **AI Models** and click **Install** or **Verify/Repair** next to the relevant model. Ensure an active internet connection during download.

### 10.4 Gemini Translation Fails with Rate Limit (`429`)
Free-tier Google Gemini API keys are subject to per-minute rate limits. Vokhira Studio automatically checkpoints every 30 translated lines. If interrupted, simply click **Translate** again; translation will immediately resume from the last saved checkpoint without re-translating earlier lines.

### 10.5 Missing Audio on Exported Video
By default, the original Chinese dialogue track is muted in dubbing projects so only the new Khmer voice track is audible. If you wish to retain the original audio in the background, open the timeline and raise the volume slider for the **Original Audio** or **Music & Effects** track before rendering.