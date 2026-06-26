# Find PII

A tiny, fast, macOS app that finds and redacts PII from files. No network access, no third party dependencies; nothing leaves your device.

*Built on Swift, with Claude Code; in a supervised, micromanaged way.*

[screenshot: main app window — results table with detected PII]

**Requirements:** macOS 15+

# [Download from here]([url](https://github.com/fzdez/find-pii/releases/latest))

## What it does

Finds structured PII, and shows what it found and where. Redact to write a cleaned copy alongside the original, or clean up pasted text before copying it out.

<img width="940" height="652" alt="image" src="https://github.com/user-attachments/assets/d8f27c65-23b1-479b-b0f7-53da6dab798a" />

## Three ways to scan

- **Drop files or folders** onto the window, or use Add Files.
- **Right-click in Finder** and choose "Find PII" to send files straight to the app.
- **Paste text** with ⌘V — PII highlights as you type.

<img width="940" height="652" alt="image" src="https://github.com/user-attachments/assets/d2afbd67-6dff-4c04-b383-ed8240f172a8" />


## What it detects

- **Structured PII (customisable):** email, credit card (Luhn-checked), SSN, TFN, ABN, ACN, student/staff IDs, UUIDs, AU phone numbers and more (customisable). Uses Regex, or Apple nsDataDetector. Filters can be customised, exported and imported (json).  
- **Contextual PII (customisable prompt):** using Apple's on-device Foundation Models.
- **Add a custom word list** if you want specific terms flagged.

<img width="940" height="856" alt="image" src="https://github.com/user-attachments/assets/13a79429-cc52-488d-9e33-c8795a770f62" />


## Private and secure

Nothing leaves your device. No network access; OS-enforced. The kernel blocks all outbound connections.

---

## Installing

1. Download `Find PII.dmg` from the latest release below.
2. Open the DMG and drag **Find PII** onto the **Applications** shortcut.
   - No admin rights on you Mac? Drag it into a folder named `Applications` inside your `/Users/<username>/Applications` folder instead (create it if it doesn't exist).

## First launch — clearing the macOS security prompt

Find PII is **not notarised by Apple** (notarisation requires a paid Apple Developer account), so the first time you open it macOS blocks it. This is expected for any app distributed outside the App Store without notarisation.

**If you are an administrator on your Mac:**

1. Double-click **Find PII**. You'll see a message that it can't be verified. Click **Done**.
2. Open **System Settings → Privacy & Security**.
3. Scroll to **Security**. Next to "Find PII.app was blocked…", click **Open Anyway**.
4. Confirm with Touch ID or your password. Find PII opens, and you won't be asked again.

**If you are NOT an administrator** (e.g. a managed work Mac), the "Open Anyway" button asks for an admin password you may not have. Use this instead — it needs no admin rights:

1. If you put **Find PII** inside your `/Users/<username>/Applications` folder (you own that folder, so no admin is required).

2. Open **Terminal** (Applications → Utilities → Terminal) and paste:

   ```
   xattr -dr com.apple.quarantine ~/Applications/Find\ PII.app
   ```

3. Press Return, then double-click **Find PII** — it now opens normally.

**Still blocked?** If your Mac is managed by an IT department, security policy may block unsigned
apps entirely, and no user-side step will help. Ask IT to allow it, or use a personal Mac 🙂 


## Verify your download (optional)

Each release publishes a SHA-256 checksum (`Find PII.dmg.sha256`). To confirm your download wasn't
corrupted or tampered with, run:

```
shasum -a 256 "Find PII.dmg"
```

Compare the output to the value on the release page. (Note: because the checksum is hosted on the
same release as the file, it mainly protects against a corrupted download.

## License & disclaimer

Find PII is released under the [MIT License](LICENSE).

**No warranty.** Find PII is provided "as is". It detects *structured* PII (emails, card numbers, IDs, phone numbers, and similar) using patterns and heuristics — it is **not** a guarantee. By design it doesn't detect **names** OOTB, and no detector catches everything. **Always review the output yourself before sharing a file.** You are responsible for confirming that a redacted file is actually safe to share.

