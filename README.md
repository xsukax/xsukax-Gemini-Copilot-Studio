<div align="center">

# ✦ xsukax Gemini Copilot Studio

### Your Gemini models. Your copilots. Your encrypted workspace.

A lightweight, **single-file, browser-based AI workspace** powered by the **Google Gemini API**. Create specialized copilots, chat with live-streaming responses, and keep your API key, conversations, and settings in a password-protected local vault.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)
![HTML5](https://img.shields.io/badge/HTML5-single--file-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-F7DF1E?logo=javascript&logoColor=black)
![Google Gemini](https://img.shields.io/badge/AI-Google%20Gemini-4285F4?logo=google&logoColor=white)
![No backend required](https://img.shields.io/badge/Backend-not%20required-22A06B)

[**Quick Start**](#-quick-start) · [**Features**](#-features) · [**Security**](#-privacy--security) · [**FAQ**](#-frequently-asked-questions) · [**License**](#-license)

</div>

---

## 📖 Overview

**xsukax Gemini Copilot Studio** is a self-contained chat application built with HTML, CSS, and JavaScript. It connects directly from your browser to Google's Gemini API using **your own API key**—without an application backend, database server, Node.js installation, or third-party JavaScript dependencies.

Create dedicated copilots for writing, research, programming, translation, analysis, or any other task. Each copilot can have its own instructions and preferred model, while your workspace and chat history are encrypted before being saved in browser storage.

> [!IMPORTANT]
> An **internet connection** and a **Google AI Studio Gemini API key** are required to request AI responses. The application runs locally, but Gemini inference runs on Google's servers.

## ✨ Features

### 🤖 Gemini AI chat

- **Real-time streaming:** Display response text as it arrives using the Gemini API's server-sent events (SSE) streaming endpoint.
- **Dynamic model discovery:** Fetch the models available to your API key and filter for models supporting `generateContent`.
- **Flexible model selection:** Choose a workspace default model and override it for individual copilots or conversations.
- **Multiple conversations:** Keep separate chat histories, automatically titled from your first message.
- **Conversation management:** Rename, clear, delete, retry an incomplete response, or stop an active generation.
- **Readable answers:** Basic Markdown rendering for headings, lists, links, quotes, inline code, and code blocks; copy messages with one click.

### 🧩 Custom copilots

- Create any number of task-specific copilots within your workspace.
- Set a **name**, **emoji icon**, and **short description**.
- Supply custom **system instructions** to define each copilot's role and behavior.
- Assign an optional **preferred Gemini model**.
- Optionally configure **temperature** and **maximum output tokens**.
- Edit, duplicate, or delete copilots; start new conversations directly from a copilot.

**Example copilot ideas:**

| Copilot | Example role |
| --- | --- |
| 🧑‍💻 Code Assistant | Explain, review, and draft code |
| 🔎 Research Assistant | Organize findings and compare information |
| ✍️ Writing Editor | Polish drafts and adjust tone |
| 🌍 Translator | Translate text with context and terminology |
| 📊 Data Analyst | Interpret pasted data and explain patterns |
| 🎓 Study Partner | Teach concepts and generate practice questions |

*These are examples you can create; the initial workspace includes a general-purpose assistant.*

### 🔐 Encrypted local workspace

- Encrypt your API key, copilot configurations, model settings, and conversations **before storing them in the browser**.
- Unlock the workspace with your own vault password after reloading.
- Lock the workspace when you are finished.
- Change the local vault password from Settings.
- Keep browser data separate by browser profile and origin.

### 📦 Password-protected JSON backups

- Export the **complete workspace** as a portable encrypted `.json` file.
- Choose a backup password independently of the local vault password.
- Restore the API key, model metadata, copilots, chat histories, and workspace settings by importing a compatible backup.
- Restore your workspace in another browser/device that can run the application.

> [!CAUTION]
> **Import replaces the current local workspace** after confirmation. Export a backup before importing another one. Passwords are not recoverable.

### 🖥️ Interface

- Modern dark theme with responsive desktop, tablet, and mobile layouts.
- Sidebar navigation for copilots and conversations.
- Separate selectors for the active copilot and model.
- Keyboard-friendly message composition (`Enter` to send, `Shift + Enter` for a new line).
- Clear feedback for streaming, saving, and errors.

## 🚀 Quick Start

### Requirements

- A current browser with **Web Crypto API** support (for example, Chrome, Edge, Firefox, or Safari).
- A [Google AI Studio API key](https://aistudio.google.com/apikey).
- Internet access to the Google Gemini API.

### Option 1 — Open the HTML file

1. Download or clone this repository.
2. Open **`index.html`** in a supported browser.
3. Paste your Google AI Studio API key.
4. Create and confirm a **vault password** (at least 8 characters).
5. The application will retrieve available Gemini models. Select a model and start a chat.

> Some browsers or configurations restrict API requests or encrypted storage from `file://` pages. If you encounter an error, use the localhost option below.

### Option 2 — Run with a local web server (recommended)

Clone the repository:

```bash
git clone https://github.com/xsukax/xsukax-Gemini-Copilot-Studio.git
cd xsukax-Gemini-Copilot-Studio
```

Start a local server with Python (only needed to serve the static file):

```bash
python3 -m http.server 8000
```

Open **http://localhost:8000** in your browser, then complete the initial setup.

No package installation, API proxy, build process, Docker container, or backend database is required.

### First-time setup

1. **API key:** Enter your own Gemini API key. The app contacts Google's model listing endpoint to confirm access and load eligible models.
2. **Vault password:** Create a strong password. This encrypts your local workspace; there is no password recovery feature.
3. **Start chatting:** Use the built-in **General Assistant**, or click **+** under *Copilots* to create a specialized assistant.
4. **Back up:** Go to **Settings & backup → Export encrypted JSON** and store the backup and password safely.

## 🧩 Creating a copilot

1. In the left sidebar, click **+** next to **Copilots**.
2. Enter a name, emoji, and optional description.
3. Write the system instructions for the job you want the copilot to perform.
4. Optionally choose a model, temperature, and output token limit.
5. Click **Create copilot**, then select it to start a new conversation.

Example system instructions for a writing copilot:

```text
You are a professional writing editor.
Improve clarity, grammar, and structure while preserving the
original meaning and intended tone. Explain major edits briefly.
Reply in the same language as the user's text unless asked otherwise.
```

**Tip:** Updating a copilot changes the instructions that will be used for its future Gemini requests. Switching the copilot of an existing chat also changes the instructions applied to subsequent messages.

## 🔒 Privacy & Security

The app is **local-first for storage**, not an offline AI model and not an end-to-end encrypted conversation service between you and Google.

| Area | Implementation |
| --- | --- |
| Workspace storage | Browser `localStorage`, encrypted before saving |
| Encryption | **AES-256-GCM** via the browser's Web Crypto API |
| Password-based key derivation | **PBKDF2-HMAC-SHA-256**, **260,000 iterations** |
| Salt / initialization vector | Random **16-byte salt** and **12-byte IV** per encryption |
| Protected content | Gemini API key, copilot instructions, chat history, models, and settings |
| Backup format | Password-encrypted JSON containing cryptographic metadata and ciphertext |
| Gemini requests | Direct browser-to-Google HTTPS API requests |
| Application backend | None |

### What stays local?

The encrypted vault is saved in the browser profile's storage. The application does not implement its own server-side accounts, cloud synchronization, or analytics backend. Encryption and decryption take place in your browser.

### What is shared with Google?

Your **Gemini API key and API request content** are sent directly to Google's Gemini service when loading models or generating responses. API requests can include the current conversation history and the selected copilot's system instructions. Google's handling of those requests is governed by its applicable API terms and policies.

### Important security limitations

- **Protect your API key.** The key and decrypted workspace exist in browser memory while unlocked. Browser extensions, compromised devices, or malicious scripts may present a risk.
- **Never embed a shared/private production API key in a publicly hosted copy.** This is a bring-your-own-key client; each user should provide their own key.
- **Keep strong passwords and separate backups.** A lost vault or backup password cannot be recovered by the application.
- **Use a trusted browser and secure context.** `http://localhost` or HTTPS is recommended for predictable Web Crypto behavior.
- **Local storage is not cross-device sync.** Browser data deletion, profile changes, or different origins can make the saved vault unavailable; encrypted backup export is the portability mechanism.
- **No independent security audit is claimed.** Encryption at rest reduces exposure of stored data but does not make an unlocked device or browser inherently secure.

## ⚙️ How It Works

```text
┌──────────────────────────────────────────────────┐
│                 Your web browser                 │
│                                                  │
│  index.html (HTML + CSS + JavaScript)            │
│            │                                     │
│            ├── Custom copilots                   │
│            ├── Conversations + model settings    │
│            ├── Live SSE response renderer        │
│            │                                     │
│            ├── Web Crypto                        │
│            │      ├── AES-256-GCM                │
│            │      └── PBKDF2-SHA-256             │
│            │             │                       │
│            │      Encrypted localStorage         │
│            │      Encrypted JSON import/export   │
│            │                                     │
│            └── HTTPS fetch + SSE ────────────────┼──► Gemini API
└──────────────────────────────────────────────────┘
```

The application currently uses the Google Generative Language API `v1beta` endpoints:

| Operation | Endpoint |
| --- | --- |
| Discover available models | `GET https://generativelanguage.googleapis.com/v1beta/models` |
| Stream generated text | `POST https://generativelanguage.googleapis.com/v1beta/models/{model}:streamGenerateContent?alt=sse` |

Available models and successful API calls depend on Google API availability, account entitlements, API-key restrictions, and quotas.

## 🗂️ Project Structure

```text
xsukax-Gemini-Copilot-Studio/
├── index.html    # Complete application: interface, styling, and logic
├── README.md     # Documentation
└── LICENSE       # GNU General Public License v3.0
```

All app styling, event handling, encryption, model discovery, and chat logic are contained inside **`index.html`**.

## 🧰 Troubleshooting

| Problem | What to try |
| --- | --- |
| **Web Crypto is unavailable** | Open in a modern browser and use `http://localhost:8000` or HTTPS. |
| **Network request failed / browser CORS issue** | Check internet access and API-key restrictions; try hosting the file on localhost rather than opening it as `file://`. |
| **No compatible models found** | Verify the API key and whether your account has access to models supporting `generateContent`. |
| **HTTP 400 / 403 / 429** | Review model compatibility, API permissions, usage limits, and quotas in Google AI Studio. |
| **Response stopped or incomplete** | Use **Retry last response**, or select another supported model. |
| **Vault password does not work** | Confirm the password for this specific local vault; otherwise restore a backup with its backup password. |
| **Chats are missing on another device** | Export an encrypted backup on the original device and import it on the second device. |
| **Storage failed** | Export a backup, free browser storage, and confirm site storage is allowed. |

## ❓ Frequently Asked Questions

**Is it free to run?**  
The application is open-source and has no hosting or app subscription requirement. Google's Gemini API may have free allowances, quotas, or usage charges depending on your account and model.

**Do I need to install Python, Node.js, or Docker?**  
No. A browser is enough for the application itself. Python in the example above is only an optional static-file server.

**Does the app work offline?**  
The interface and local vault can be opened without a dedicated application server, but model discovery and AI responses require an internet connection to Google.

**Can I use a different Gemini model for each copilot?**  
Yes. Copilots can use a preferred model or inherit the workspace default, and an individual chat can use another model.

**Can I back up everything, including my API key?**  
Yes. The encrypted JSON export contains the API key, copilots, chats, models, and workspace settings. Protect both the backup file and its password.

**Can I upload PDFs, images, or other attachments to a chat?**  
Not in the supplied version. The chat interface currently sends text messages and renders text responses; the import file picker is for encrypted workspace backups.

**Can multiple people share a synchronized workspace?**  
Not natively. Workspaces are browser-local. Encrypted export/import is supported, but live shared accounts and synchronization are not implemented.

## 🤝 Contributing

Contributions, improvements, and bug reports are welcome.

1. [Fork the repository](https://github.com/xsukax/xsukax-Gemini-Copilot-Studio/fork).
2. Create a branch for your change.
3. Keep the application self-contained unless the project intentionally adopts additional dependencies.
4. Test browser compatibility, encryption, model selection, and export/import behavior.
5. Submit a pull request explaining your change.

Please report bugs or suggest features via [GitHub Issues](https://github.com/xsukax/xsukax-Gemini-Copilot-Studio/issues). **Never include real API keys, passwords, or unencrypted personal chat contents in an issue.**

## 📄 License

**xsukax Gemini Copilot Studio** is licensed under the **GNU General Public License v3.0 (GPL-3.0-only)**.

You may use, study, modify, and redistribute the software under the terms of GPLv3. Distributions of modified covered works must follow the applicable GPLv3 obligations, including source-code availability and preservation of required notices. The software is provided **without warranty**.

See the full [LICENSE](LICENSE) file or the [GNU GPLv3](https://www.gnu.org/licenses/gpl-3.0.html).

Copyright © 2026 **xsukax**.

---

<div align="center">

**Built as a single file. Designed for specialized copilots. Encrypted for your browser.**

[GitHub Repository](https://github.com/xsukax/xsukax-Gemini-Copilot-Studio) · [Report an Issue](https://github.com/xsukax/xsukax-Gemini-Copilot-Studio/issues)

</div>
