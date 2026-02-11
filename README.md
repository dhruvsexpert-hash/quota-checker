# 🚀 Antigravity Quota Watcher

A sleek, real-time dashboard to monitor your Gemini (Antigravity) model quotas. Sign in with Google OAuth, view remaining quota per model, and track reset timers — all from a single-page web app.

## Features

- **Google OAuth 2.0** with PKCE — secure sign-in and token management
- **Real-time quota monitoring** — auto-refreshes every 5 seconds
- **Per-model breakdown** — remaining percentage, color-coded progress bars, and reset countdowns
- **Tier display** — shows your current plan tier (e.g. `LEGACY`, paid tiers)
- **Logout with token revocation** — revokes the Google token server-side on sign out
- **Dark, modern UI** — glassmorphism design with smooth animations

## Tech Stack

| Layer    | Technology                  |
|----------|-----------------------------|
| Backend  | Python, FastAPI, Uvicorn    |
| Frontend | Vanilla HTML/CSS/JS         |
| Auth     | Google OAuth 2.0 + PKCE     |
| Deploy   | Docker, Docker Compose      |

## Quick Start

### With Docker (recommended)

```bash
docker compose up --build -d
```

Open [http://localhost:8000](http://localhost:8000) in your browser.

### Without Docker

```bash
pip install -r requirements.txt
python main.py
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000) in your browser.

## How It Works

1. **Sign in** — Click "Sign in with Google" to authenticate via OAuth 2.0
2. **View quotas** — The dashboard fetches quota data from the Cloud Code API and displays per-model usage
3. **Auto-refresh** — Quotas update every 5 seconds automatically; click the refresh button for an instant update
4. **Sign out** — Click the logout button to revoke your token and return to the login screen

## Project Structure

```
quota_checker/
├── main.py               # FastAPI backend (auth, quota API, token management)
├── index.html            # Frontend (single-page dashboard UI)
├── requirements.txt      # Python dependencies
├── Dockerfile            # Container image definition
├── docker-compose.yml    # Docker Compose config with named volume for token persistence
└── README.md
```

## Token Storage

- Tokens are stored at `/token_store/antigravity_quota_token.json` inside the container
- A Docker **named volume** (`token_data`) persists tokens across container restarts
- No host filesystem dependency — the container is fully self-contained
