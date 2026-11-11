# Vokhira Studio — Third-Party Licenses & Legal Notices

**Product**: Vokhira Studio  
**Application Copyright**: &copy; 2026 Vokhira Studio. All rights reserved.  
**Distribution Repository**: `ehak-math/vokhira-studio-releases`  

---

## 1. Overview & Licensing Architecture

Vokhira Studio is distributed as a proprietary desktop application. The core application logic, user interface, orchestration engine, and proprietary brand assets are protected by copyright law.

To provide high-performance multimedia processing and artificial intelligence capabilities, Vokhira Studio bundles and interoperates with third-party open-source runtimes, software libraries, and machine learning models. This document provides mandatory attribution, licensing terms, redistribution notices, and source code availability for all third-party components included in or utilized by the distributed application.

---

## 2. Bundled Binary Distributions

### 2.1 FFmpeg & FFprobe (GPL v3.0)
- **Component**: FFmpeg & FFprobe standalone CLI binaries
- **Packaged Version**: `9.0.2-essentials_build` (Windows x64 static build by [gyan.dev](https://www.gyan.dev/))
- **Binary SHA-256 Checksums**:
  - `ffmpeg.exe`: `3256173f3f8bffd7df12227c68adf68025edb1832273a9530688a7bb1ed8edec`
  - `ffprobe.exe`: `f0d36ecbbdd3bcfac3efa078c96c7271c2e68b3810595552ac3b7f17e9a65c52`
- **License**: **GNU General Public License v3.0 (GPL v3)**
  *(The `essentials_build` configuration is compiled with `--enable-gpl` and includes GPL-licensed libraries).*
- **Upstream Source Code**: [FFmpeg Git Commit `946fcce07b`](https://github.com/FFmpeg/FFmpeg/commit/946fcce07b) / [CodexFFmpeg 9.0.2](https://github.com/GyanD/codexffmpeg/tree/9.0.2)
- **Aggregation Notice**:
  FFmpeg and FFprobe are packaged as separate, standalone executable binaries located in `resources/ffmpeg/`. Vokhira Studio communicates with these tools strictly as an external subprocess via standard command-line pipes and arguments (`child_process.spawn`). The binaries are distributed alongside their accompanying `LICENSE` (GNU GPL v3) and `README.txt` files in accordance with Section 6 of the GNU GPL v3.

```text
FFmpeg is a trademark of Fabrice Bellard, originator of the FFmpeg project.
This software uses libraries from the FFmpeg project under the GNU General Public License v3.0.
Full license text: https://www.gnu.org/licenses/gpl-3.0.html
```

---

### 2.2 Python Runtime (PSF License 2.0)
- **Component**: Relocatable Python 3.11 Windows runtime
- **Version**: Python 3.11.9
- **License**: Python Software Foundation (PSF) License Agreement
- **Location**: `resources/python/`
- **Notice**:
```text
PYTHON SOFTWARE FOUNDATION LICENSE VERSION 2
--------------------------------------------
1. This LICENSE AGREEMENT is between the Python Software Foundation ("PSF"), and
the Individual or Organization ("Licensee") accessing and otherwise using this
software ("Python") in source or binary form and its associated documentation.
2. Subject to the terms and conditions of this License Agreement, PSF hereby
grants Licensee a nonexclusive, royalty-free, world-wide license to reproduce,
analyze, test, perform and/or display publicly, prepare derivative works, distribute,
and otherwise use Python alone or in any derivative version.
```

---

### 2.3 Electron & Chromium Runtimes
- **Component**: Electron Desktop Framework & Embedded Chromium
- **Version**: Electron 31.x / Chromium
- **License**:
  - Electron: **MIT License**
  - Chromium: **BSD 3-Clause License** and related multi-license notices
- **Notice**:
```text
Copyright (c) OpenJS Foundation and Electron contributors.
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software...
```

---

## 3. Core Software Libraries & Python Packages

| Package | Version | License | Upstream Link |
|---|---|---|---|
| **Faster-Whisper** | 1.2.1 | MIT License | [SYSTRAN/faster-whisper](https://github.com/SYSTRAN/faster-whisper) |
| **CTranslate2** | 4.8.3 | MIT License | [OpenNMT/CTranslate2](https://github.com/OpenNMT/CTranslate2) |
| **Silero VAD** | Integrated | MIT License | [snakers4/silero-vad](https://github.com/snakers4/silero-vad) |
| **Edge-TTS** | 7.3.1 | GNU LGPL v3.0 | [rany2/edge-tts](https://github.com/rany2/edge-tts) |
| **PyTorch** | 2.14.1 | Modified BSD License | [pytorch/pytorch](https://github.com/pytorch/pytorch) |
| **Transformers** | 4.57.6 | Apache License 2.0 | [huggingface/transformers](https://github.com/huggingface/transformers) |
| **ONNX Runtime** | 1.31.0 | MIT License | [microsoft/onnxruntime](https://github.com/microsoft/onnxruntime) |
| **SoundFile** | 0.14.0 | BSD 3-Clause License | [bastibe/python-soundfile](https://github.com/bastibe/python-soundfile) |
| **NumPy** | 2.3.5 | BSD 3-Clause License | [numpy/numpy](https://github.com/numpy/numpy) |
| **Hugging Face Hub**| 0.36.2 | Apache License 2.0 | [huggingface/huggingface_hub](https://github.com/huggingface/huggingface_hub) |
| **React** | 18.x | MIT License | [facebook/react](https://github.com/facebook/react) |
| **Lucide Icons** | Integrated | ISC License / MIT | [lucide-icons](https://github.com/lucide-icons/lucide) |

---

## 4. Machine Learning Models & Weights

> **Important Packaging Notice**: In order to keep the standalone installer size under 350 MB, **no AI model weights are bundled directly inside the installer binary**. All model weights are downloaded on demand by the user through the in-app AI Model Manager and stored locally in `%APPDATA%\Vokhira Studio\models\`.

### 4.1 OpenAI Whisper Models (Faster-Whisper INT8)
- **Models**: `whisper-tiny`, `whisper-small`, `whisper-medium`, `whisper-large-v3-turbo`
- **Origin**: OpenAI / SYSTRAN Faster-Whisper converted weights
- **License**: **MIT License**
- **Terms**: Open for commercial and non-commercial utilization under MIT conditions.

### 4.2 Meta Massively Multilingual Speech (MMS) Khmer TTS
- **Model**: `facebook/mms-tts-khm`
- **Origin**: Meta AI Research
- **License**: **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)**
- **Notice**:
  The Meta MMS Khmer TTS checkpoint is released under CC BY-NC 4.0. Users utilizing this offline speech engine must adhere to Meta's non-commercial licensing terms.

### 4.3 Meta NLLB-200 Machine Translation
- **Model**: `facebook/nllb-200-distilled-600M`
- **Origin**: Meta AI Research
- **License**: **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)**
- **Notice**:
  The NLLB-200 model weights are provided under CC BY-NC 4.0 for non-commercial research and personal translation workflows.

### 4.4 Microsoft Edge Neural TTS
- **Service**: Microsoft Edge Online Speech Services (`km-KH-PisethNeural`, `km-KH-SreymomNeural`)
- **Protocol**: Accessed via WebSocket requests utilizing the LGPL-v3 licensed `edge-tts` client wrapper.
- **Notice**: Use of Microsoft Edge TTS endpoints is subject to Microsoft's service terms and acceptable use policies.

---

## 5. Compliance Verification & Source Code Offer

In accordance with the requirements of the **GNU General Public License v3.0 (GPL v3)** and **GNU Lesser General Public License v3.0 (LGPL v3)**:

1. **Source Code Availability**:
   - For FFmpeg 9.0.2: Full source code corresponding to the packaged build is available at [FFmpeg Git Commit 946fcce07b](https://github.com/FFmpeg/FFmpeg/commit/946fcce07b).
   - For Edge-TTS: Source code is available at [rany2/edge-tts](https://github.com/rany2/edge-tts).
2. **Accompanying Documentation**:
   The installer staging pipeline (`scripts/build/stage-runtime.py`) copies the complete FFmpeg `LICENSE` and `README.txt` files directly into `build/ffmpeg/`, ensuring they reside side-by-side with the executable binaries on the user's filesystem upon installation.
3. **No Dynamic Linking**:
   The proprietary Vokhira Studio executable does not dynamically link against GPL-licensed libraries; it operates FFmpeg as an independent subprocess.

---

## 6. Questions or Inquiries

For inquiries regarding third-party licensing or open-source compliance:
- Open a discussion or inquiry in [GitHub Issues](https://github.com/ehak-math/vokhira-studio-releases/issues).