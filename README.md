# 🧠 Intuition

A real-time, two-player number-guessing duel in the spirit of Mastermind. Each player picks a secret number, and you take turns cracking your opponent's before the clock runs out.

![React](https://img.shields.io/badge/React-Vite-61DAFB?logo=react&logoColor=black)
![FastAPI](https://img.shields.io/badge/FastAPI-WebSockets-009688?logo=fastapi&logoColor=white)
![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white)

## How to play

1. Pick a difficulty: **Easy** (4 digits), **Medium** (6) or **Hard** (8). You're matched with another player waiting at the same level, and each of you sets a secret number.
2. Players take turns guessing. Each guess comes back digit by digit:
   - 🟩 right digit, right position
   - 🟨 right digit, wrong position
   - ⬜ not in the number
3. The game runs on a **2-minute timer**. When time is up, the player with the most digits in the right position wins.

## How it's built

| Part | Details |
|---|---|
| **Backend** (`backend/main.py`) | FastAPI WebSocket server. Matchmaking queue per difficulty, turn enforcement, per-digit feedback, and a server-side countdown that ends the game. All state is in memory. |
| **Frontend** (`frontend/`) | React + Vite single-page app that talks to the backend over one WebSocket. |
| **Deploy** | The backend can also serve the built frontend, so the game runs on a single port. Example nginx and systemd files are included, and `DEPLOY.md` covers free-tier hosting. |

The server decides everything (turns, feedback, the timer and the winner), so a player can't cheat by editing the page.

## Run it locally

```bash
# backend
cd backend
pip install -r requirements.txt
uvicorn main:app --port 8765

# frontend (in a second terminal)
cd frontend
npm install
npm run dev
```

Open the URL Vite prints in two browser windows and start a game in each.
