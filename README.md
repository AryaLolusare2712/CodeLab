# CodeLab — Real-Time Collaborative IDE

> **Code Together. Ship Faster. Build Smarter.**

Codelab is a browser-based collaborative coding environment where teams can write, run, and debug code together in real time — powered by an embedded Google Gemini AI assistant that already knows your code.

---

## ✨ Features

### 🔴 Real-Time Collaboration
- Live multi-user code editing with **cursor presence** — see exactly where each teammate is
- Instant code sync via **WebSockets** — no refresh needed
- **Team chat** with in-editor code references
- **Git operation notifications** broadcast to all room members

### 🤖 AI Coding Assistant
- Powered by **Google Gemini 2.5 Flash**
- Context-aware — the AI automatically sees your current code file
- Multi-turn conversation history (last 10 messages retained)
- Ask for bug fixes, explanations, optimizations, or new features

### ▶️ Code Execution Engine
- Run code directly in the browser across **5 languages**:

| Language | Runtime |
|---|---|
| Python | `python3` |
| JavaScript | `node` |
| C++ | `g++ -std=c++17` |
| Java | `javac` + `java` |
| Rust | `rustc` |

- Sandboxed subprocess execution with configurable timeout (default 5s)
- Full stdout/stderr output with exit codes and execution time

### 👥 Role-Based Access Control
| Role | Edit | Run | Chat | Manage Members | Delete Session |
|---|---|---|---|---|---|
| Owner | ✅ | ✅ | ✅ | ✅ | ✅ |
| Developer | ✅ | ✅ | ✅ | ❌ | ❌ |
| Tester | ❌ | ✅ | ✅ | ❌ | ❌ |
| Client | ❌ | ❌ | ❌ | ❌ | ❌ |

### 🔐 Authentication
- Secure **JWT-based** auth with 7-day token expiry
- **bcrypt** password hashing with salt
- Register/login with username and password — no OAuth required

### 💾 Storage
- **Redis** as primary key-value store (sessions, users, TTL)
- **Automatic in-memory fallback** — works locally without Redis

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3, Flask, Flask-SocketIO |
| Real-time | Socket.IO (WebSockets, threading mode) |
| AI | Google Gemini 2.5 Flash (`google-generativeai`) |
| Auth | PyJWT, bcrypt |
| Storage | Redis + in-memory fallback |
| Frontend | Vanilla HTML/CSS/JS, CodeMirror 5 |
| Config | python-dotenv |

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- Node.js (for JavaScript execution)
- g++ (for C++ execution)
- Java JDK (for Java execution)
- Rust (for Rust execution)
- A [Google AI Studio](https://aistudio.google.com/app/apikey) API key

### Installation

**1. Clone the repository**
```bash
git clone https://github.com/AryaLolusare2712/CodeLab.git
cd codesync
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Configure environment variables**

Create a `.env` file in the project root:
```env
GOOGLE_API_KEY=your_google_api_key_here

# Optional
JWT_SECRET=your-secret-key-change-in-prod
EXEC_TIMEOUT=5
PORT=5000
```

**4. Run the server**
```bash
python app.py
```

**5. Open your browser**
```
http://localhost:5000
```

> If port 5000 is busy, the app automatically finds the next available port and prints it in the console.

---

## 📁 Project Structure

```
codesync/
├── app.py          # Full-stack backend (Flask + SocketIO + AI + execution)
├── index.html      # Frontend (single-file, no build step)
├── requirements.txt
├── .env            # Your API keys and config (not committed)
└── README.md
```

---

## 🔌 API Reference

### Auth
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and get JWT token |

### Sessions
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/sessions` | Create a new coding session |
| GET | `/api/sessions/:id` | Get session details |
| DELETE | `/api/sessions/:id` | Delete a session (owner only) |

### Code Execution
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/execute` | Execute code (returns stdout/stderr) |

### AI Assistant
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/ai/chat` | Chat with Gemini AI with code context |

### Health
| Method | Endpoint | Description |
|---|---|---|
| GET | `/health` | Server health check (Redis + AI status) |

---

## ⚡ WebSocket Events

| Event | Direction | Description |
|---|---|---|
| `join` | Client → Server | Join a coding session room |
| `code_delta` | Client → Server | Send code changes |
| `cursor` | Client → Server | Send cursor position |
| `team_chat` | Client → Server | Send a chat message |
| `git_op` | Client → Server | Broadcast a git operation |
| `snapshot` | Server → Client | Full session state on join |
| `code_update` | Server → Client | Live code changes from peers |
| `cursor_update` | Server → Client | Peer cursor positions |
| `presence` | Server → Client | List of active users in room |
| `team_message` | Server → Client | Incoming chat message |
| `notification` | Server → Client | Join/leave notifications |

---

## 🌍 Environment Variables

| Variable | Default | Description |
|---|---|---|
| `GOOGLE_API_KEY` | *(required for AI)* | Google Gemini API key |
| `JWT_SECRET` | `CodeLab-dev-secret` | Secret for signing JWT tokens |
| `REDIS_URL` | `redis://localhost:6379/0` | Redis connection URL |
| `EXEC_TIMEOUT` | `5` | Max seconds for code execution |
| `PORT` | `5000` | Server port (auto-increments if busy) |

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 🙏 Acknowledgements

- [Flask](https://flask.palletsprojects.com/) — backend framework
- [Flask-SocketIO](https://flask-socketio.readthedocs.io/) — WebSocket support
- [CodeMirror](https://codemirror.net/) — in-browser code editor
- [Google Gemini](https://ai.google.dev/) — AI assistant
- [Socket.IO](https://socket.io/) — real-time engine

---

<p align="center">Built with ❤️ at a hackathon</p>
