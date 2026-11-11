# Vokhira Studio — Community Support & Issue Reporting Guidelines

Welcome to the Vokhira Studio support hub. Because Vokhira Studio is currently in Public Beta, user feedback and bug reports are invaluable for identifying defects and refining workflows.

---

## 1. Where to Get Help

| Need | Recommended Channel | Link |
|---|---|---|
| **Bug Reports** | GitHub Issues (Bug Template) | [Submit Bug Report](https://github.com/ehak-math/vokhira-studio-releases/issues/new?template=bug_report.yml) |
| **Feature Ideas** | GitHub Issues (Feature Template) | [Request Feature](https://github.com/ehak-math/vokhira-studio-releases/issues/new?template=feature_request.yml) |
| **Setup & Guides** | Repository Documentation | [Installation Guide](INSTALLATION_GUIDE.md) |
| **Known Issues** | Confirmed Defect Tracker | [Known Issues](KNOWN_ISSUES.md) |
| **Security Issues** | Private Security Advisory | [Report Security Issue](https://github.com/ehak-math/vokhira-studio-releases/security/advisories/new) |

---

## 2. Before You Submit an Issue

To help resolve problems quickly, please perform these initial checks:

1. **Check Known Issues**: Search [KNOWN_ISSUES.md](KNOWN_ISSUES.md) to see if your symptom is an expected beta limitation or already known.
2. **Search Existing Issues**: Search the [GitHub Issue Tracker](https://github.com/ehak-math/vokhira-studio-releases/issues) to ensure the bug hasn't already been reported.
3. **Verify Installer Checksum**: If your application crashes on startup, verify that your installer wasn't corrupted during download (see [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md#3-verifying-the-sha-256-checksum)).
4. **Update to Latest Beta**: Ensure you are running the latest version available on the [Releases page](https://github.com/ehak-math/vokhira-studio-releases/releases).

---

## 3. Reporting a Bug

When submitting a bug report via our [Bug Report Form](https://github.com/ehak-math/vokhira-studio-releases/issues/new?template=bug_report.yml), please provide:

- **Application Version**: Found in the window title bar or `Help` → `About` (e.g., `0.4.22`).
- **Windows OS Version**: Exact build (e.g., `Windows 11 Pro 64-bit 23H2`).
- **Steps to Reproduce**: Clear, numbered steps from launching the app to the point of failure.
- **Expected Behavior**: What you expected to happen.
- **Actual Behavior**: What actually happened (include error messages or screenshots).
- **Diagnostics**: Non-sensitive log excerpts (see below).

---

## 4. Collecting Diagnostic Logs (Safely)

Vokhira Studio writes execution logs locally to your user profile:

```text
%APPDATA%\Vokhira Studio\logs\
```

*(You can open this folder by pressing `Win + R`, pasting the path above, and pressing Enter).*

### 🔒 Privacy First: Sanitizing Your Logs Before Posting

> ⚠️ **CRITICAL WARNING**: Never post the following in public GitHub Issues:
> - **API Keys**: Never share your Google Gemini API key or any tokens.
> - **Personal Information**: Redact full names, email addresses, or proprietary company data.
> - **Private Video / Audio Assets**: Do not upload copyrighted or private customer media.
> - **File Paths**: If your username or folder paths contain private information, replace them with `<username>` or `<path>`.

The application is engineered never to print raw API keys to log files. However, always review log snippets before pasting them into public tickets.

---

## 5. Security Vulnerabilities

We take application security and user data protection seriously.

**Do NOT report suspected security vulnerabilities through public GitHub Issues.**

If you discover a security vulnerability (such as credential exposure, insecure communication, or memory safety bugs):
1. Open a **Private Security Advisory** via [GitHub Advisory Submission](https://github.com/ehak-math/vokhira-studio-releases/security/advisories/new).
2. If GitHub Advisory submission is unavailable on your account, create a confidential issue or contact the repository owner directly through their GitHub profile.
3. Include detailed steps to reproduce the vulnerability and potential impact.
4. Allow reasonable time for remediation before any public disclosure.