# NEXIS 4.0

Created by Dani — Free to use and share (non-commercial only)

---

## What is this?

NEXIS is a fully local AI assistant with an agent loop architecture.  
The LLM itself decides when and which tool to use — no keyword-based routing.  
Everything runs on your own machine — no cloud, no data sharing, full control.

---

##⚠️ First Launch — Windows Security Warning

If you downloaded NEXIS as a zip file, **Smart App Control** or **SmartScreen** may block it from running.  
Windows automatically flags files downloaded from the internet as potentially unsafe.

**This is not a virus. This is normal Windows behavior for zip files.**

### How to fix it? (2 methods)

**Method 1 — Automatic (recommended):**  
Run `NEXIS_setup.bat` first. It will automatically unblock all files for you.  
After that, `NEXIS_start.bat` will launch without any issues.

**Method 2 — Manual (if the .bat itself won't open):**

1. Right-click `NEXIS_start.bat`
2. Select **Properties**
3. At the bottom of the window: check **"Unblock"**
4. Click **OK**
5. Now run `NEXIS_setup.bat` — it will handle the rest of the files automatically

You only need to do this **once**.

---

## 🚀 Features

- Fully local execution — no internet required in default mode
- **Agent loop architecture** — the LLM decides tool usage autonomously
- Web search, file search, image input, code execution
- Conversation history with sidebar — browse and reload past sessions
- SQLite-based two-level memory system
- Optional Advanced Mode with web search context
- PIN-code access protection
- Animated sidebar and thinking indicator

---

## ⚙️ Modes

**Default Mode**  
Fully local, no internet connection.  
Concise answers, fast responses. Recommended for everyday use.

**Advanced Mode (optional)**  
Enables web search — results are included as context for the LLM.  
Longer, structured answers.

- Enable via the **⚙ Settings** panel in the sidebar
- Or type `enable advanced` in the chat
- Disable with `disable advanced`

---

## 🤖 Agent Loop

NEXIS 4.0 uses a real agent loop — keyword-based routing is gone.

**How it works:**
1. The LLM receives the user request + descriptions of all available tools
2. If a tool is needed, the LLM signals it in `TOOL_CALL: <tool> | <query>` format
3. The loop runs the tool and feeds the result back to the LLM
4. The LLM produces the final answer based on the tool result
5. If no tool is needed, it replies directly (`FINAL:` prefix)
6. A maximum step count prevents infinite loops

**Available tools** (the LLM decides when to use them):
- `web_search` — searches the web via DuckDuckGo
- `memory_lookup` — retrieves relevant past context
- `safe_execute` — runs sandboxed Python code
- `file_search` — searches files on the local system
- `vision` — processes uploaded images

Type `help` in the chat to see the current tool list at runtime.

---

## 🧠 Memory System

NEXIS uses a two-level SQLite memory system:

- **Session history** — keeps context within the current conversation (automatic)
- **Long-term memory** — persists across sessions via semantic search
- Stored in: `memory/nexis_memory.db`

Click the **☰ button** (top-left) to open the sidebar:

- Browse past conversations
- **New Chat** — start a fresh session (saves the current one automatically)
- **Clear History** — wipe the current session's memory

---

## 🔒 Security

- No data is uploaded or shared anywhere
- Everything runs locally on your machine
- Internet access is **off by default**
- System-level actions are **restricted by default**
- PIN protection — stored locally, hashed with SHA-256, never sent anywhere

---

## 📦 Installation

### 1. Install Python (if you don't have it)

Download from: https://www.python.org/downloads/  
**Important:** during install, check **"Add Python to PATH"**.

### 2. Run the setup

Double-click `NEXIS_setup.bat`.  
It will unblock all files, install dependencies, and launch NEXIS.

### 3. Launch later

Double-click `NEXIS_start.bat`.

---

## 🤖 Adding a Model

NEXIS uses a local AI model in GGUF format.  
Download your preferred model (e.g. from HuggingFace) and place it in the `models/` folder.  
NEXIS will find and load it automatically on next launch.

Recommended: any instruction-tuned GGUF model compatible with `llama-cpp-python`.

---

## 🔑 PIN Code

PIN lock can be enabled in **⚙ Settings**.  
Must be 4–8 digits. Stored locally, hashed with SHA-256. Never sent anywhere.  
3 failed attempts will close the application.

---

## 💬 System Commands

These are handled locally without going through the LLM:

| Command | Effect |
|---|---|
| `enable advanced` | Switch to Advanced Mode |
| `disable advanced` | Switch back to Default Mode |
| `clear history` / `new chat` | Clear current session memory |
| `agent status` | Check if the agent loop is active |
| `help` | List available tools and commands |

---

## 📋 Requirements

- Python 3.10 or newer
- Windows 10 / 11
- A `.gguf` model file placed in the `models/` folder

**Dependencies** (installed automatically by setup):
- `llama-cpp-python`
- `customtkinter`
- `requests`
- `duckduckgo-search`
