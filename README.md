# Find PII

A tiny, fast, macOS app that **finds** and **redacts** PII (Personally Identifiable Information) in files and text. No network access, no third party dependencies; nothing leaves your device.

*Built on Swift, with Claude Code; in a supervised, micromanaged way.*

**[Download from here](https://github.com/fzdez/find-pii/releases/latest)**

**Requirements:** macOS 15+

<img width="1019" height="652" alt="Landing screen (in light mode)" src="https://github.com/user-attachments/assets/c41c248e-e106-4621-923f-3997f9fba30d" />


<img width="1019" height="652" alt="Results screen (in dark mode)" src="https://github.com/user-attachments/assets/50c0c3b2-1a98-4130-8609-9b159a0ffe1c" />


## Three ways to scan

- **Drop files or folders** onto the window, or use Add Files.
- **Right-click in Finder** and choose "Find PII" to send files straight to the app.
- **Paste text** with ⌘V — PII highlights as you type.

<img width="1024" height="655" alt="gif showing pasting text to scan, and redacting PII with a click" src="https://github.com/user-attachments/assets/fdff7522-bf0f-496b-a7fb-a995cbbf7d93" />


## What it detects

- **Structured PII (customisable):** email, credit card (Luhn-checked), SSN, TFN, ABN, ACN, student/staff IDs, UUIDs, AU phone numbers and more (customisable). Uses Regex, or Apple nsDataDetector. Filters can be customised, exported and imported (json).  
- **Contextual PII (customisable prompt):** using Apple's on-device Foundation Models.
- **Add a custom word list** if you want specific terms flagged.

<img width="1019" height="652" alt="filter settings showing a custom profile" src="https://github.com/user-attachments/assets/542b6207-87c0-421b-8dc6-743c998277a8" />


<img width="1019" height="652" alt="filter settings showing a custom word/name list" src="https://github.com/user-attachments/assets/68f10218-bf5d-4168-b681-d2d9db383e4f" />


## Private and secure

Nothing leaves your device. No network access; OS-enforced. The kernel blocks all outbound connections. 

This also means the app can't check for updates.

No third party libraries or dependencies used. 

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

**Still blocked?** If your Mac is managed by an IT department, security policy may block unsigned apps entirely, and no user-side step will help. Ask IT to allow it, or use a personal Mac 🙂 


## Verify your download (optional)

Each release publishes a SHA-256 checksum (`Find PII.dmg.sha256`). To confirm your download wasn't corrupted or tampered with, run:

```
shasum -a 256 "Find PII.dmg"
```

Compare the output to the value on the release page. (Note: because the checksum is hosted on the same release as the file, it mainly protects against a corrupted download.

## License & disclaimer

Find PII is released under the [MIT License](LICENSE).

**No warranty.** Find PII is provided "as is". It detects *structured* PII (emails, card numbers, IDs, phone numbers, and similar) using patterns and heuristics — it is **not** a guarantee. By design it doesn't detect **names** OOTB, and no detector catches everything. **Always review the output yourself before sharing a file.** You are responsible for confirming that a redacted file is actually safe to share.

