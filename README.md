# 🤖 Desktop AI Chat Application (V2)
### A Study in Thread-Safe LLM Integration for Desktop Systems

This project presents a **desktop-based AI chat application** designed to explore **safe integration of Large Language Models (LLMs)** into graphical user interfaces.
The system focuses on **responsiveness, concurrency control, and persistent conversational state**, addressing common issues encountered when integrating blocking AI APIs into event-driven desktop applications.

The application is implemented using **Python and CustomTkinter**, with AI inference handled via the **Groq API**, and employs a **background worker + UI queue architecture** to ensure thread safety and system stability.

This project is an upgraded and architecturally improved version of my earlier Desktop AI Chatbot, redesigned to follow real desktop application patterns.

---

## ✨ Key Features

- 🖥️ Native Desktop GUI (no browser required)

- 💬 Persistent Chat Sessions

    - Chats saved locally as JSON

    - Auto-load most recent conversations

- 📂 Sidebar Session Management

    - Create, rename, delete chats

    - Live preview of recent messages

- ⚡ Fast LLM Responses using Groq API

- 🧵 Background Worker Threads

    - Blocking AI calls never freeze the UI

- 🔁 Thread-Safe UI Updates

    - UI queue pattern for main-thread rendering

- ✍️ Streaming AI Responses

    - Token-by-token style output for better UX

---

## Core Contributions

- ✅ Thread-safe LLM invocation in a GUI environment

- ✅ Separation of concerns between UI, AI inference, and persistence

- ✅ Persistent multi-session conversation storage

- ✅ Deterministic execution flow suitable for analysis and extension

- ✅ Executable desktop deployment

---

## System Architecture Overview

The application follows a multi-threaded producer–consumer design:

- The Main UI Thread is responsible for:

    - event handling

    - rendering

    - safe UI updates

- A Background Worker Thread performs:

    - blocking LLM API calls

    - response retrieval

- A UI Task Queue bridges the worker thread and the UI thread,
ensuring that all UI mutations occur on the main thread.

- A File-based persistence layer maintains long-term conversational state.

---
## Application Workflow


![AI Chat Application Workflow](assets/workflow.png)

### Execution Flow Summary
1. Initialization Phase (Main Thread)

    - Environment variables are loaded

    - AI client is initialized

    - Session index is created or restored

    - UI window and sidebar are rendered

2. User Interaction Phase (Main Thread)

    - User input is captured

    - Message is appended to the UI

    - Message is persisted to disk

    - Background worker thread is spawned

3. Inference Phase (Worker Thread)

    - Blocking LLM API call is executed

    - AI response is retrieved

    - UI update task is enqueued

4. UI Update Phase (Main Thread)

    - UI queue is processed

    - AI response is streamed to the chatbox

    - Response is persisted

    - Sidebar metadata is refreshed

This architecture ensures non-blocking UI behavior while maintaining deterministic state updates.

---

## Persistence Model

- sessions/index.json – session metadata and ordering
- sessions/{session_id}.json – complete chat history with timestamps

Atomic writes are used to prevent data corruption.

---

## 🧰 Tech Stack

| Technology         | Purpose                                               |
|--------------------|-------------------------------------------------------|
| Python             | Core programming language                             |
| CustomTkinter      | Desktop UI framework with modern widgets              |
| Groq API | LLM Inferences                      |                               
| dotenv             | Securely manage API keys                              |
| threading/os/queue | System utilities and multithreading support       |

---

## 📂 Project Structure

```
Desktop-AI-Chatbot-V2/
├── app.py
│
├──utils/
├── ui.py                  # UI logic and event handling
├── ai_client.py           # LLM client abstraction
├── workers.py             # Background inference workers
├── session_manager.py     # Persistent session management
├── helpers.py             # Environment & runtime helpers
│
├── assets/
│   ├── .env               # API key configuration
│   ├── Llama.ico
│   └── send.ico
│
├── sessions/
│   ├── index.json
│   └── <session_id>.json
│
└── README.md
```
---
## Author
**Pramit Acharjya**  
✨ Passionate about AI, automation, and building practical tools.  

📺 YouTube: [Kaiso Gaming & Tech](https://www.youtube.com/@KaisoGaming_AT)  
💻 GitHub: [@KaisoX24](https://github.com/KaisoX24)

---
## ⭐ Support

If you find this project useful, please **⭐ star this repo** to support future development!
---

## License
This project is licensed under the MIT License.
