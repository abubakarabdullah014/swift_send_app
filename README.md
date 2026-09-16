# SwiftSend

Desktop app for sending personalized Gmail emails from a CSV (compose, follow-up, attachments, scheduling).

**Download:** get `SwiftSend.exe` from this repo → double-click to open.

No install folder required. Put the `.exe` on your Desktop or anywhere you like.

---

## Requirements

- Windows 10 or 11
- [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) (already on most PCs)
- A Gmail account
- One-time Google Cloud OAuth setup (below)

Your login and settings are stored in:

`%APPDATA%\SwiftSend\`

---

## First-time Google setup (once)

### 1. Enable Gmail API

1. Open [Google Cloud Console](https://console.cloud.google.com/)
2. Create a project (or select one)
3. Enable **Gmail API**:  
   [Enable Gmail API](https://console.cloud.google.com/apis/library/gmail.googleapis.com)

### 2. OAuth consent screen (Audience)

1. Go to **Google Auth Platform → Audience**
2. User type: **External**
3. Publishing status: **Testing** is fine for personal use
4. Under **Test users**, click **Add users**
5. Add **your** Gmail address

> If Google shows **403 access_denied**, your email is missing from Test users.

### 3. Create a Desktop OAuth client

1. Go to **Clients → Create client**
2. Application type: **Desktop app**
3. Download the JSON file (`client_secret_....json`)

### 4. Connect Gmail inside SwiftSend

1. Open **SwiftSend.exe**
2. Click **Copy login link** (copied automatically)
3. Paste the URL in any browser (Chrome, Edge, Firefox, …)
4. Sign in with Google and Allow
5. Return to SwiftSend — token is saved automatically

Or use **Open default browser** if you prefer Windows to open the link.

---

## How to use

### Dashboard (CSV send)

1. Upload a CSV with columns like:
   - **Email** / `to`
   - **Email Subject** / `subject`
   - **Email Body** / `body`
   - Optional: name column
2. Optionally add attachments (CV, PDF, etc.)
3. Set delay between emails if you want
4. Click **Send** or **Schedule**

Broken / fancy dashes in subjects (`–`, `—`, `â€“`) become a normal `-`. A plain `-` is left as-is.

### Compose

Write one subject + body, add many recipients (type them or upload a CSV email list). Each person gets their own email.

### Follow-up

Replies in the **same Gmail thread** as your last Sent message to that address (like Reply in Gmail). Addresses with no prior Sent mail can be skipped.

### Scheduled sends

Pick a future date/time.  
**Important:** your PC must be on and **SwiftSend must be open** at that time. Gmail has no remote “schedule send” API for this app.

### History

Past sends are listed in the **History** tab.

---

## Sharing this app

You can send `SwiftSend.exe` to someone else as a single file.

Each person must:

1. Use **their own** Google Cloud `credentials.json`
2. Add **themselves** as a Test user
3. Sign in with **their** Gmail in Settings

Do not share your `credentials.json` or login token.

---

## Troubleshooting

| Problem | Fix |
|--------|-----|
| App won’t open / blank window | Install [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/), then try again |
| 403 access_denied | Add your Gmail under OAuth **Test users** |
| credentials.json missing | Upload the Desktop client JSON in **Settings** |
| Asks to sign in again after update | **Settings → Sign out → Sign in with Google** (new permissions) |
| Scheduled email didn’t send | Keep the PC awake and SwiftSend open at the scheduled time |
| Wrong icon after rename | Windows icon cache — rename the file once or refresh the folder |

---

## Privacy

- The app runs **locally** on your PC
- Emails are sent through **your** Gmail via Google’s official API
- Tokens and history stay in `%APPDATA%\SwiftSend\`
- This repo ships only the app binary + this guide (no source code)
