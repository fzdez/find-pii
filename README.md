# Find PII - Find and Redact PII in files/text and images (macOS)

[![Release](https://img.shields.io/github/v/release/fzdez/find-pii?label=release)](https://github.com/fzdez/find-pii/releases/latest)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
![Platform](https://img.shields.io/badge/platform-macOS%2015%2B-blue)
![Swift](https://img.shields.io/badge/Swift-6-orange?logo=swift&logoColor=white)
![Dependencies](https://img.shields.io/badge/dependencies-zero-brightgreen)
![Network](https://img.shields.io/badge/network-none-brightgreen)

A tiny, superfast macOS app that **finds** and **redacts** PII (Personally Identifiable Information) in files, images and the clipboard; before sharing on.

No data can leave your device; the app has no network access, and no third party dependencies or libraries. 

### [Download from here](https://github.com/fzdez/find-pii/releases/latest)

Lightning fast (screenshot taken on Macbook Pro M5)

<img width="800" alt="Screenshot showing results screen, with scanning speed magnified. 5,441 files scanned in 0.54s." src="https://github.com/user-attachments/assets/e3ee3b8a-9bee-4c0a-b75d-1cc66fbeded6" />

## Four ways to Find PII

1. **Drop files or folders** onto the window, or use *Add Files*.
2. **Paste text** with <kbd>⌘V</kbd> — PII highlights as you type.
3. **Use Clipboard Cleaner** from the ***optional*** menu-bar item or global <kbd>⌃⌥⌘V</kbd> shortcut. Useful for checking copied text before pasting it into AI tools, or sharing. Password (concealed) and non-text clipboard content won't be processed.
4. **Right-click in Finder** and choose "Find PII" to send files straight to the app.

<img width="800" alt="Screenshot showing blank Find PII welcome page" src="https://github.com/user-attachments/assets/6d569719-188b-44e5-a5f7-3e066e79c47c" />


<img width="800" alt="GIF showing the paste text to scan function, then redacting and copying redacted text" src="https://github.com/user-attachments/assets/1af7cd8a-1eb8-415a-bc47-c227d17c491f" />


## Supported file types

| Type | Scan | Redact |
|---|---|---|
| Text based: txt, md, csv, json and log or similar | Yes | Yes |
| Word (docx), Excel (xlsx) and PowerPoint (pptx) | Yes | Yes |
| RTF (Rich Text Format) | Yes | Yes |
| PDF | Yes (text layer) | No |
| Images: PNG, JPEG, HEIC and TIFF | Yes | Yes (black rectangle) |
| Images: GIF, WebP and BMP | Yes | No |

**Office redaction** covers document body, headers, footers, comments, charts, text boxes, document properties and embedded Office files. Genuinely damaged or suspicious Office files are refused, instead of producing a partial or falsely clean result.

**Image OCR** is best effort using on-device Apple Vision OCR; and can miss text. Find PII shows a banner whenever images are included; review important images manually in Preview or another trusted image editor before sharing. Multi-frame images scan only the first frame and can't be redacted. Redacted image copies are rotated upright, HDR is converted to SDR (8-bit), and stripped of metadata such as EXIF, GPS, IPTC or XMP. 
Note: if no PII is found in an image; redaction won't work and metadata won't be removed. I'll work on that sometime; it's unexpectedly tricky.

## Supported types of PII

<img width="800" alt="Settings-Filter, showing a custom profile." src="https://github.com/user-attachments/assets/e19501ab-5355-43be-9e63-6402d4185648" />

| Detector                                 | Details                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Structured PII** (customisable)        | Email, phone (AU + international), credit card (13–19 digits with Luhn and card-family checks, including UnionPay, Diners Club and Maestro), SSN, AU TFN/ABN/ACN/Medicare, UUIDs, IP addresses, plus custom regex filters. <br>Filters can be exported and imported (via JSON).                                                                                                                     |
| **Contextual PII** (customisable prompt) | Uses Apple's on-device Foundation Models. Not the most accurate right now, but expecting better performance with [Apple Intelligence updates in September 2026](https://www.apple.com/newsroom/2026/06/apple-unveils-next-generation-of-apple-intelligence-siri-ai-and-more/). <br>No integration with third-party AI models via API. |
| **Custom word lists**                    | Wildcards like `*` and `?` supported. Use this to detect and redact staff names, usernames, code words.                                                                                                                                                                                                                               |



<img width="800" alt="Settings-Filter showing a custom word/name list" src="https://github.com/user-attachments/assets/b45c149e-9978-480c-b767-7a673c72c2ed" />


## Private and secure

1. Nothing leaves your device. No network access; OS-enforced (the kernel blocks all outbound connections).
2. No third party libraries or dependencies used. And I don't plan to.
3. The app can't check for updates itself. When a build reaches 30 days old, it shows a tiny dismissible reminder linking to GitHub.
4. Automated-test report in `Settings` > `About` shows it passed all 805 tests.

## Accessible

WCAG 2.1 AA *(according to me and a rigorous Claude test)* with VoiceOver labels, contrast-safe colours, full keyboard navigation, Dynamic Type, reduce-motion support. I'm not used to using a screen reader/voiceover, so please [report issues](https://github.com/fzdez/find-pii/issues).

---

## Get Started / Installation

1. Download `Find PII.dmg` from the latest release below.
2. Open the DMG and drag **Find PII** onto the **Applications** shortcut.
   - No admin rights on your Mac? Drag it into a folder named `Applications` inside your `/Users/<username>/Applications` folder instead (create one, if it doesn't exist).

## First launch — clearing the macOS security prompt

Find PII is **not notarised by Apple** (that requires a 99 USD/year Apple Developer account), so the first time you open it, macOS will block it. This is expected for any app distributed outside the App Store without Apple notarisation. ℹ️ Source code coming soon (July 2026), once I'm able to clean up.

**If you are an administrator on your Mac:**

1. Double-click **Find PII**. You'll see a message that it can't be verified. Click **Done**.
2. Open **System Settings → Privacy & Security**.
3. Scroll to **Security**. Next to "Find PII.app was blocked…", click **Open Anyway**.
4. Confirm with Touch ID or your password. Find PII opens, and you won't be asked again.

<details>
<summary><strong>If you are NOT an administrator</strong> (e.g. a managed work MacBook) — click to expand</summary>

The "Open Anyway" button asks for an admin password you may not have. Do this instead — it needs no admin rights:

1. Drag **Find PII.app** into your `/Users/<username>/Applications` folder (you own that folder, no admin permission required).

2. Open **Terminal** (Applications → Utilities → Terminal), paste and run the command below. ⚠️ If you are unsure, search for what "xattr -dr com.apple.quarantine" does, or ask AI if this command is safe.

If the app is installed to /Users/<username>/Applications
   ```
   xattr -dr com.apple.quarantine ~/Applications/Find\ PII.app
   ```

If the app is installed to default /Applications
   ```
   xattr -dr com.apple.quarantine /Applications/Find\ PII.app
   ```

3. After running that, double-click **Find PII**; it should now open normally.

</details>

**Still blocked?** If your Mac is managed by an IT department, security policy may block unsigned apps entirely, and no user-side step will help. Ask IT to allow it, or use a personal Mac 🙂

<details>
<summary>Verify your download (optional)</summary>

Each release publishes a SHA-256 checksum (`Find PII.dmg.sha256`). To confirm your download wasn't corrupted or tampered with, run this from the same folder as the .dmg file:

```
shasum -a 256 "Find PII.dmg"
```

Compare the output to the value on the release page or the sha256 file.

Note: because the checksum is hosted on the same release as the file, it mainly protects against a corrupted download.

</details>

## License & disclaimer

Find PII is released under the [MIT License](LICENSE).

**No warranty.** Find PII is provided "as is". It detects _structured_ PII (emails, card numbers, IDs, phone numbers, and similar) using patterns and heuristics — it is **not** a guarantee. By design it doesn't detect **names** out of the box (a custom word list is needed), and no detector catches everything. **Always review the output yourself before sharing a file.** You are responsible for confirming that a redacted file is actually safe to share.
