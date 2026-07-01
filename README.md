# Find PII

![Platform](https://img.shields.io/badge/platform-macOS%2015%2B-blue)
![Swift](https://img.shields.io/badge/Swift-6-orange?logo=swift&logoColor=white)
![Dependencies](https://img.shields.io/badge/dependencies-zero-brightgreen)
![Network](https://img.shields.io/badge/network-none-lightgrey)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

A tiny,superfast macOS app that **finds** and **redacts** PII (Personally Identifiable Information) in files and pasted text. Redact to write a cleaned copy, or clean up pasted text before copying it out. 

_Built on Swift, with Claude Code; in a supervised, micromanaged way._ No network access, no third party dependencies; nothing leaves your device.

### [Download from here](https://github.com/fzdez/find-pii/releases/latest) (needs macOS 15+)

Lightning fast (screenshot taken on Macbook Pro M5)

<img width="800" alt="Screenshot showing results screen, with scanning speed magnified. 1,948 files scanned in 0.38s." src="https://github.com/user-attachments/assets/60c371bc-b25c-4ded-a42a-6b05d1ad24b7" />



## Three ways to scan

<img width="800" alt="Screenshot showing blank Find PII welcome page" src="https://github.com/user-attachments/assets/faae247e-daaa-4a0b-808e-965a3aff20fe" />

- **Drop files or folders** onto the window, or use Add Files.
- **Right-click in Finder** and choose "Find PII" to send files straight to the app.
- **Paste text** with <kbd>⌘V</kbd> — PII highlights as you type.

<img width="800" alt="GIF showing the paste text to scan function, then redacting and copying redacted text" src="https://github.com/user-attachments/assets/e146b808-8a50-4bb0-be5a-cf885f6f0030" />


## What it detects

<img width="800" alt="Settings-Filter, showing a custom profile." src="https://github.com/user-attachments/assets/e19501ab-5355-43be-9e63-6402d4185648" />

| Detector                                 | Details                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Structured PII** (customisable)        | Email, phone (AU + international), credit card (with Luhn check), SSN, AU TFN/ABN/ACN/Medicare, UUIDs, IP addresses, plus custom regex filters. <br>Filters can be exported and imported (via JSON).                                                                                                                                  |
| **Contextual PII** (customisable prompt) | Uses Apple's on-device Foundation Models. Not the most accurate right now, but expecting better performance with [Apple Intelligence updates in September 2026](https://www.apple.com/newsroom/2026/06/apple-unveils-next-generation-of-apple-intelligence-siri-ai-and-more/). <br>No integration with third-party AI models via API. |
| **Custom word lists**                    | Wildcards like `*` and `?` supported. Use this to detect and redact staff names, usernames, code words.                                                                                                                                                                                                                               |



<img width="800" alt="Settings-Filter showing a custom word/name list" src="https://github.com/user-attachments/assets/b45c149e-9978-480c-b767-7a673c72c2ed" />


## Private and secure

1. Nothing leaves your device. No network access; OS-enforced (the kernel blocks all outbound connections).
2. No third party libraries or dependencies used. And I don't plan to.
3. This also means the app can't check for updates. Come here maybe once a month 😬 

## Accessible

WCAG 2.1 AA *(according to a rigorous Claude test)* with VoiceOver labels, contrast-safe colours, full keyboard navigation, Dynamic Type, reduce-motion support. I tested too, but I'm not used to using a screen reader/voiceover, so please [report issues](https://github.com/fzdez/find-pii/issues).

---

## Installing

1. Download `Find PII.dmg` from the latest release below.
2. Open the DMG and drag **Find PII** onto the **Applications** shortcut.
   - No admin rights on your Mac? Drag it into a folder named `Applications` inside your `/Users/<username>/Applications` folder instead (create it if it doesn't exist).

## First launch — clearing the macOS security prompt

Find PII is **not notarised by Apple** (that requires a 99 USD/year Apple Developer account), so the first time you open it, macOS blocks it. This is expected for any app distributed outside the App Store without Apple notarisation. Source code will come soon (July 2026), once I'm able to clean up.

**If you are an administrator on your Mac:**

1. Double-click **Find PII**. You'll see a message that it can't be verified. Click **Done**.
2. Open **System Settings → Privacy & Security**.
3. Scroll to **Security**. Next to "Find PII.app was blocked…", click **Open Anyway**.
4. Confirm with Touch ID or your password. Find PII opens, and you won't be asked again.

<details>
<summary><strong>If you are NOT an administrator</strong> (e.g. a managed work Mac) — click to expand</summary>

The "Open Anyway" button asks for an admin password you may not have. Use this instead — it needs no admin rights:

1. Drag **Find PII.app** into your `/Users/<username>/Applications` folder (you own that folder, no admin permission required).

2. Open **Terminal** (Applications → Utilities → Terminal), paste and run the command below. If you are unsure, ask AI if this command is safe, and what the risks are.

   ```
   xattr -dr com.apple.quarantine ~/Applications/Find\ PII.app
   ```

3. After running that, double-click **Find PII**; it should now open normally.

</details>

**Still blocked?** If your Mac is managed by an IT department, security policy may block unsigned apps entirely, and no user-side step will help. Ask IT to allow it, or use a personal Mac 🙂

<details>
<summary>Verify your download (optional)</summary>

Each release publishes a SHA-256 checksum (`Find PII.dmg.sha256`). To confirm your download wasn't corrupted or tampered with, run:

```
shasum -a 256 "Find PII.dmg"
```

Compare the output to the value on the release page or the sha256 file.

Note: because the checksum is hosted on the same release as the file, it mainly protects against a corrupted download.

</details>

## License & disclaimer

Find PII is released under the [MIT License](LICENSE).

**No warranty.** Find PII is provided "as is". It detects _structured_ PII (emails, card numbers, IDs, phone numbers, and similar) using patterns and heuristics — it is **not** a guarantee. By design it doesn't detect **names** out of the box (a custom word list is needed), and no detector catches everything. **Always review the output yourself before sharing a file.** You are responsible for confirming that a redacted file is actually safe to share.
