<div align="center">

<img src="image/logo_arena.png" alt="Chess Arena logo" width="100" />

# ♟️ Chess Arena

**A multiplayer chess platform where you can play online against real opponents, challenge Stockfish 16, and track your stats.**

[**🌐 Live Demo**](https://prismatic-lamington-297b85.netlify.app/)

![Node.js](https://img.shields.io/badge/Node.js-18+-339933?logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?logo=express)
![Socket.io](https://img.shields.io/badge/Socket.io-4-010101?logo=socketdotio)
![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose-47A248?logo=mongodb&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue)

</div>

---

## 📖 About

**Chess Arena** is our final year group project at **[College Name]**. It is a full-stack web app that lets players sign up, find an opponent in real time with a chosen time control, play against the Stockfish 16 engine, and view their profile, statistics and awards.

<!--
📸 Screenshots: create a `screenshots/` folder, add your images, then uncomment:

| Home | Multiplayer | Play vs AI |
|------|-------------|------------|
| ![Home](screenshots/home.png) | ![Multiplayer](screenshots/multiplayer.png) | ![AI](screenshots/ai.png) |
-->

## ✨ Features

- 🌐 **Real-time online multiplayer** — matchmaking queue with **10, 15 and 20 minute** time controls, powered by Socket.io
- 🤖 **Play against AI** — Stockfish 16 (NNUE, WebAssembly) running directly in the browser
- ♟️ **Complete chess rules** — legal move validation, check/checkmate, castling, en passant and promotion (via chess.js)
- 🕒 **Game clocks** for both players
- 📋 **PGN / FEN** — save and load game notation
- 👤 **Authentication** — sign up / log in with JWT and bcrypt-hashed passwords
- 🧑‍💼 **User profile** — edit username, email and upload a profile picture
- 📊 **Statistics** — wins, losses, draws and win rate for Classical, Blitz and Bullet
- 🏅 **Awards & milestones** page
- 📈 **Elo rating** system (K-factor 32, default rating 1200)
- 📱 Mobile-friendly board controls
- 🐳 Docker, Vercel and Netlify deployment configs included

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML, CSS, JavaScript, jQuery, [chessboard.js](https://chessboardjs.com/), [chess.js](https://github.com/jhlywa/chess.js), Vite |
| Backend | Node.js, Express |
| Real-time | Socket.io |
| Database | MongoDB with Mongoose |
| Auth | JSON Web Tokens, bcrypt |
| File uploads | Multer |
| Chess engine | Stockfish 16 (NNUE, WASM) |
| DevOps | Docker, PM2, Vercel, Netlify, Railway |

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- [MongoDB](https://www.mongodb.com/) — a local instance or a free [MongoDB Atlas](https://www.mongodb.com/atlas) cluster
- Git

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/chess-arena.git
cd chess-arena

# 2. Install dependencies
npm install

# 3. Configure environment variables
cp .env.example .env        # Windows: copy .env.example .env
# then open .env and fill in your values
```

### Environment variables

| Variable | Description |
|----------|-------------|
| `MONGO_URI` | MongoDB connection string |
| `JWT_SECRET` | Secret key used to sign login tokens (use a long random string) |

### Stockfish network file (for Play vs AI)

The Stockfish NNUE network file (`nn-5af11540bbfe.nnue`, ~38 MB) is **not included in this repository**. Download it from the official Stockfish network list and place it in `js/engine/`:

```
js/engine/nn-5af11540bbfe.nnue
```

See <https://tests.stockfishchess.org/nns> (search for the file name above). Without this file, the multiplayer mode works but *Play vs AI* will not.

### Run locally

Open **two terminals**:

```bash
# Terminal 1 — backend (API + Socket.io) on http://localhost:3000
node server.js

# Terminal 2 — frontend (Vite dev server)
npm run dev
```

Then open the URL shown by Vite (usually `http://localhost:5173`).

> When the site is opened from `localhost`, the frontend automatically talks to the local backend at `http://localhost:3000`.

### Run with Docker

```bash
docker build -t chess-arena .
docker run -p 3000:3000 --env-file .env chess-arena
```

## 🎮 How to Play

1. **Sign up** and **log in** from the home page.
2. **Multiplayer:** choose a time control (10 / 15 / 20 min) and wait to be matched. Open the site in a second browser window to test with yourself.
3. **vs AI:** open *Play Against AI* to play Stockfish 16.
4. Move pieces by dragging and dropping them on the board.
5. Visit **Profile**, **Stats** and **Awards** to see your progress.

## 🔌 API Overview

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/auth/signup` | Create a new account | ❌ |
| POST | `/auth/login` | Log in and receive a JWT | ❌ |
| GET | `/auth/profile` | Get current user's profile | ✅ |
| POST | `/auth/updateProfile` | Update username, email, profile picture | ✅ |
| GET | `/auth/stats` | Get current user's statistics | ✅ |
| POST | `/auth/logout` | Log out | ❌ |
| GET | `/matches` | List stored matches | ❌ |

**Socket.io events:** `want_to_play`, `match_made`, `sync_state`, `sync_state_from_server`, `game_over`, `game_over_from_server`, `total_players_count_change`.

## 📁 Project Structure

```
chess-arena/
├── routes/                  # Express routes (auth, profile, stats)
├── models/                  # Mongoose models (User, Match)
├── js/                      # Board logic, controls, timers
│   ├── engine/              # Stockfish 16 WASM + NNUE
│   ├── libs/                # chess.js, chessboard.js, jQuery
│   └── mobile/              # Mobile controls
├── css/                     # Board & chessboard styles
├── image/ , img/            # Logos and board assets
├── uploads/                 # User profile pictures
├── server.js                # Express + Socket.io server
├── socket.js                # Standalone Socket.io server
├── index.html               # Home page
├── index_multiplayer.html   # Online multiplayer
├── index_AI.html            # Play vs Stockfish
├── login.html / signup.html # Authentication pages
├── profile.html             # User profile
├── stats.html               # Statistics
├── awards.html              # Awards & milestones
├── Dockerfile
├── vite.config.js
└── vercel.json
```

## 👥 Team

| Name | Role | GitHub |
|------|------|--------|
| Ashish | [Role] | [@username](https://github.com/username) |
| [Name 2] | [Role] | [@username](https://github.com/username) |
| [Name 3] | [Role] | [@username](https://github.com/username) |

**Under the guidance of:** [Guide / Professor name]

## 🔮 Future Improvements

- [ ] Rating updates after every multiplayer game
- [ ] Reconnection handling for dropped players
- [ ] Puzzles and tutorials
- [ ] Adjustable AI difficulty levels
- [ ] In-game chat and friend challenges

## 🙏 Acknowledgements

- [Stockfish](https://stockfishchess.org/) — open-source chess engine
- [chess.js](https://github.com/jhlywa/chess.js) and [chessboard.js](https://chessboardjs.com/) — move validation and board UI

## 📄 License

Distributed under the MIT License. See [LICENSE](LICENSE) for more information.

---

<div align="center">⭐ If you like this project, please give it a star! ⭐</div>
