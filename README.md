# NEON ARENA — Ultimate Full-Stack Competitive Gaming Platform

<p align="center">
  <strong>A modern, responsive, competitive arcade gaming platform featuring real-time multiplayer, progression, tournaments, and 6 original playable games.</strong>
</p>

<p align="center">
  <img src="https://images.unsplash.com/photo-1550745165-9bc0b252726f?w=1200&auto=format&fit=crop&q=80" alt="NEON ARENA Banner" width="100%" />
</p>

---

## Table of Contents
1. [Platform Overview](#platform-overview)
2. [Design System & Reference Adaptations](#design-system--reference-adaptations)
3. [The 6 Playable Games](#the-6-playable-games)
4. [Platform Features](#platform-features)
   - [Progression, XP & Levels](#progression-xp--levels)
   - [Real-Time Multiplayer & Matchmaking](#real-time-multiplayer--matchmaking)
   - [Tournaments & Brackets](#tournaments--brackets)
   - [Quests & Daily Challenges](#quests--daily-challenges)
   - [Global & Competitive Leaderboards](#global--competitive-leaderboards)
   - [Friends & Social Presence](#friends--social-presence)
   - [Admin Control Center](#admin-control-center)
5. [Technology Stack](#technology-stack)
6. [Architecture & Monorepo Structure](#architecture--monorepo-structure)
7. [Quickstart & Local Setup](#quickstart--local-setup)
8. [Automated Test Suite](#automated-test-suite)
9. [Docker & Containerized Deployment](#docker--containerized-deployment)
10. [REST API & Socket.IO Reference](#rest-api--socketio-reference)

---

## 1. Platform Overview

**NEON ARENA** is an end-to-end competitive web gaming destination inspired by the top arcade portals on the web, re-imagined with a high-octane cyberpunk aesthetic, server-authoritative game validation, real-time multiplayer duels, and an immersive player progression loop.

Unlike static landing pages or frontend templates, **every part of NEON ARENA is genuinely functional**:
- **6 fully playable, original games** with fluid controls, responsive canvas rendering, sound synthesizers, and real score recording.
- **Real-time 1v1 multiplayer duels** using WebSockets, matchmaking queues, private invite codes, and Elo rating updates.
- **Persistent player progression** backed by 26 relational Prisma database models, awarding XP, levels, streak bonuses, and achievements.
- **Community tournaments** with automated bracket generation and match reporting.
- **Comprehensive administration dashboard** with platform telemetry, user moderation, report handling, and immutable audit logs.

---

## 2. Design System & Reference Adaptations

NEON ARENA establishes an original cyberpunk visual identity combining deep obsidian surfaces, glassmorphic panels, and selective glowing neon accents (cyan `#00f0ff`, electric violet `#8b5cf6`, magenta `#ec4899`, emerald `#10b981`, and restrained gold `#ffd700`).

### Design Inspirations & Improvements
| Reference | Original Principle | NEON ARENA Adaptation & Elevation |
|---|---|---|
| **BGAMES** | Dense game catalog, genre tags & cyan highlights | Searchable multi-facet filters, genre filters, favorites, recently played history, and personalized recommendations. |
| **Poki** | Engaging visual card discovery & featured tiles | Varied grid layouts, responsive layered game cards with animated hover glow, and featured game hero showcases. |
| **CrazyGames** | Organized left sidebar & multiplayer discovery | Collapsible glass sidebar integrating real-time player level/XP progress, quest notifications, tournaments, and friend presence. |
| **OnlineGames.io** | Geometric gradients & 3D gaming atmosphere | Lightweight Three.js interactive 3D hero canvas with glowing cyber geometric meshes and subtle mouse-following parallax. |
| **Kizi** | Accessible genre menus & category browsing | Deep filtering by genre, game mode (solo/multiplayer), difficulty, and competitive rating availability. |
| **now.gg** | Spacious dark canvas & strong modern typography | Obsidian backgrounds, high-contrast typography, and live player dashboard previews with real-time stats. |
| **Cyberix3D** | 3D game previews & extensible game systems | Modular deterministic game engines decoupled into `@neon-arena/game-engine`, enabling straightforward expansion with future titles. |

---

## 3. The 6 Playable Games

All 6 games are original implementations with responsive keyboard, mouse, and touch controls, custom Web Audio API sound synthesis, difficulty scaling, and server-verified score and XP rewards:

### 1. Tic-Tac-Toe Neon (`tic-tac-toe`)
- **Mode:** Solo (Adaptive Minimax AI with Easy / Medium / Hard) & Real-Time Multiplayer.
- **Features:** Instant matchmaking queue, 6-character private room codes, server-authoritative turn enforcement, live opponent moves, rematch protocol, and competitive Elo stakes.
- **Controls:** Left Click / Tap on grid tiles.

### 2. Neon Snake (`snake`)
- **Mode:** Single-Player Arcade.
- **Features:** High-speed cyber serpent with radiant trails, pulsating energy pellets, dynamic speed increments every 5 pellets consumed, high-score tracking, and instant pause/resume.
- **Controls:** `WASD` / Arrow Keys / Touch swipe, `Space` / `P` to pause.

### 3. Cyber 2048 (`2048`)
- **Mode:** Single-Player Strategy / Puzzle.
- **Features:** Smooth tile-sliding animations, exponential color gradations from 2 to 2048, merge score calculations, undo detection, and game-over state verification.
- **Controls:** Arrow Keys / `WASD` / Swipe gesture, `R` to restart.

### 4. Neon Cyber Flap (`neon-flap`)
- **Mode:** Single-Player Precision Arcade.
- **Features:** Smooth physics-based impulse thrusters, gravitational acceleration, randomized neon beam obstacle columns, collision detection, and score milestones.
- **Controls:** `Spacebar` / Left Click / Tap to pulse thrusters.

### 5. Cyber Slice (`cyber-slice`)
- **Mode:** Single-Player Reflex Arcade.
- **Features:** Glowing particle blade trail drawn with mouse or touch, ballistic physics for flying cyber-fruits, explosive red hazard bombs, multi-slice combo multipliers, and 3 energy lives.
- **Controls:** Click & Drag / Touch & Swipe across moving targets.

### 6. Orbit Strike (`orbit-strike`)
- **Mode:** Single-Player 2D Physics Puzzle.
- **Features:** Drag-and-release slingshot launcher, predictive trajectory calculation arc, impulse launch velocity, 2D physics restitution with crystal fortress blocks, and star ratings based on shots fired.
- **Controls:** Click & Drag slingshot backwards to aim, Release to fire.

---

## 4. Platform Features

### Progression, XP & Levels
- **Dynamic XP Formula:** Non-linear scaling based on $100 \times \text{level}^{1.45}$.
- **Verified Transactions:** All score submissions are verified server-side against session timestamps to eliminate spoofing.
- **Anti-Duplication:** Idempotency keys protect reward claims.
- **Animated Feed:** Level-up notifications, reward toasts, and instant XP progress bar updates.

### Real-Time Multiplayer & Matchmaking
- **Socket.IO Real-Time Gateway:** Token-authenticated WebSockets with fallback.
- **1v1 Matchmaking Queue:** Automated pairing for Tic-Tac-Toe.
- **Custom Game Rooms:** Create and join matches with 6-character room codes.
- **Rematch Workflow:** One-click rematch protocol without disconnecting.
- **Disconnect Resilience:** 15-second grace window to reconnect before forfeit.

### Tournaments & Brackets
- **Single-Elimination Brackets:** Automated 4, 8, or 16 player bracket structures.
- **Registration Flow:** Live countdown timers, registration deadlines, and XP prize pools.
- **Interactive Bracket Viewer:** Visual tournament tree showing matchup progression and winners.

### Quests & Daily Challenges
- **Rotating Missions:** Daily quests (e.g. "Score 500 in Snake", "Play 3 matches") and weekly challenges.
- **Progress Tracking:** Automatic progress increments upon game completion.
- **Instant Claiming:** Real-time XP claiming with celebratory sound and particle effects.

### Global & Competitive Leaderboards
- **Global XP Ladder:** Top players ranked by total experience points and level.
- **Game-Specific High Scores:** Filterable by all 6 games.
- **Competitive Elo Ladder:** Ranks ranging from Bronze $\rightarrow$ Silver $\rightarrow$ Gold $\rightarrow$ Platinum $\rightarrow$ Diamond $\rightarrow$ Master $\rightarrow$ Champion.
- **Friends Filter:** Compare achievements and scores against your social circle.

### Friends & Social Presence
- **Real-Time Presence:** Live indicators for Online, In-Game, and Offline statuses.
- **Friend Requests:** Search users by username, send/accept/decline requests.
- **Match Invites:** Send real-time game invitations directly to online friends.
- **Community Safety:** Report and block mechanisms for toxic behavior.

### Admin Control Center
*(Restricted to `ADMIN` accounts, e.g. `admin`)*
- **Real-Time Telemetry:** Platform metrics (active users, total sessions, matches played, average score).
- **User Management:** Paginated player directory with role promotion (`PLAYER` $\rightarrow$ `MODERATOR` $\rightarrow$ `ADMIN`) and ban/unban capabilities with customizable durations and reasons.
- **Moderation Queue:** View and resolve user reports with audit tracking.
- **Tournament Creator:** Instant generation of tournaments with custom player caps and XP prizes.
- **Audit Logs:** Immutable audit log stream recording all administrative actions.

---

## 5. Technology Stack

### Frontend (`apps/web`)
- **React 18** with **TypeScript** & **Vite**.
- **Tailwind CSS** with custom cyberpunk neon styling and animations.
- **Three.js** for interactive 3D hero canvas.
- **Lucide React** for modern vector icons.
- **Canvas Confetti** for celebration and level-up rewards.
- **Zustand** for client-side state (authentication, sound, active game states).
- **TanStack React Query** for server-state synchronization and caching.
- **Socket.IO Client** for real-time multiplayer and presence.
- **Web Audio API** procedural synthesizer (zero audio asset latency).

### Backend (`apps/api`)
- **Node.js** & **Express** in **TypeScript**.
- **Socket.IO** server with JWT authentication and game room lifecycle manager.
- **Prisma ORM** with **PostgreSQL** (production) and **SQLite** (local out-of-the-box development).
- **Redis** for matchmaking queues, session storage, and rate limiting.
- **Bcrypt** for secure password hashing.
- **Zod** for end-to-end type validation.
- **Helmet, CORS, Cookie-Parser, and Express-Rate-Limit** for enterprise security.

### Monorepo Packages
- `@neon-arena/shared`: Common enums, types, Elo formulas, progression math, socket events.
- `@neon-arena/validation`: Zod schemas for auth, profile, session, tournament, social, admin.
- `@neon-arena/game-engine`: Pure game logic for all 6 games (TTT minimax, Snake step/collision, 2048 merge/slide, Flap collision, Slice geometry, Orbit Strike trajectory).
- `@neon-arena/config`: Game catalog definitions, quests, achievements, avatars.

---

## 6. Architecture & Monorepo Structure

```
neon-arena/
├── apps/
│   ├── api/                    # Express REST API & Socket.IO server
│   └── web/                    # React 18 + Vite frontend application
├── packages/
│   ├── shared/                 # Core interfaces, enums, math
│   ├── validation/             # Zod validation schemas
│   ├── game-engine/            # Deterministic game rules & simulation
│   └── config/                 # Game metadata, quest & achievement definitions
├── prisma/
│   ├── schema.prisma           # Active schema (configured with SQLite for dev)
│   ├── schema.postgresql.prisma# PostgreSQL schema for Docker & Cloud
│   └── seed.ts                 # Database seeder (demo users, quests, games)
├── infrastructure/
│   ├── docker/                 # Production Dockerfiles (API & Web)
│   └── nginx/                  # Nginx reverse proxy configuration
├── docs/                       # Technical specifications (Architecture, API, Multiplayer)
└── docker-compose.yml          # Containerized production stack
```

---

## 7. Quickstart & Local Setup

### Prerequisites
- **Node.js 20+** or **Node.js 22 LTS**
- **npm 10+**

### 1. Clone & Install Dependencies
```bash
git clone https://github.com/neon-arena/neon-arena.git
cd neon-arena
npm install
```

### 2. Configure Environment
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```
*(Default environment is pre-configured with SQLite `dev.db` for instant local execution without needing external database services)*

### 3. Initialize & Seed Database
```bash
# Push database schema
npm run db:push

# Seed games, quests, achievements, and demo accounts
npm run db:seed
```

### 4. Start Development Servers
Run both backend API (`localhost:4000`) and frontend Web (`localhost:5173`) concurrently:
```bash
npm run dev
```

Or run services individually:
```bash
npm run dev:api    # Starts API server on http://localhost:4000
npm run dev:web    # Starts Web client on http://localhost:5173
```

Open **`http://localhost:5173`** in your browser!

### Demo Accounts Seeded
| Username | Password | Role | Description |
|---|---|---|---|
| `admin` | `Admin123!` | `ADMIN` | Full administrative access & dashboard |
| `cyber_ninja` | `Password123!` | `PLAYER` | Level 5 competitive player (Rating 1450) |
| `pixel_queen` | `Password123!` | `PLAYER` | Level 3 casual player (Rating 1280) |
| `neon_reaper` | `Password123!` | `PLAYER` | Level 2 arcade enthusiast (Rating 1190) |
| `retro_samurai` | `Password123!` | `PLAYER` | Level 1 new recruit (Rating 1200) |

---

## 8. Automated Test Suite

NEON ARENA includes a comprehensive automated test suite powered by **Vitest**:
- **Game Engine Unit Tests:** Deterministic AI minimax decisions, snake movements, 2048 tile merging, collision detections, slice math, and slingshot trajectory mechanics.
- **Progression Math Tests:** Level requirements, Elo calculation fairness, transaction integrity.
- **API Authentication Tests:** Registration, login, duplicate detection, invalid credentials.
- **End-to-End Scenario Tests:** Complete competitive multiplayer flow (register two users, join queue, match found, play moves, server victory detection, Elo and XP updates, and match history verification).
- **Frontend Web Tests:** Catalog validation, sound synthesizer safety, auth store actions.

Run all tests across all workspaces:
```bash
npm test
```

### Test Results
```
✓ tests/progression.test.ts (5 tests)
✓ tests/gameEngine.test.ts (12 tests)
✓ tests/apiAuth.test.ts (7 tests)
✓ tests/e2eScenario.test.ts (5 tests)
✓ src/tests/webApp.test.ts (7 tests)

Test Files  5 passed (5)
Tests       36 passed (36)
```

---

## 9. Docker & Containerized Deployment

To run the entire platform with PostgreSQL, Redis, API, and Nginx Web in Docker:

```bash
# Build and run containers in background
docker compose up -d --build

# View container logs
docker compose logs -f

# Shut down containers
docker compose down
```

Services exposed:
- **Web Application & Reverse Proxy:** `http://localhost:80`
- **Backend API:** `http://localhost:4000`
- **PostgreSQL Database:** `localhost:5432`
- **Redis Cache:** `localhost:6379`

---

## 10. REST API & Socket.IO Reference

For detailed documentation, consult the dedicated guides in `/docs`:
- [Architecture & Design Details](docs/ARCHITECTURE.md)
- [REST API Endpoint Specification](docs/API.md)
- [Multiplayer & Socket.IO Specification](docs/MULTIPLAYER.md)

---

## License
MIT License. Built for the competitive gaming community.
<img width="1916" height="912" alt="image" src="https://github.com/user-attachments/assets/0fcdfcb6-8c51-4e0a-9a87-7de5803e444e" />
<img width="1917" height="917" alt="image" src="https://github.com/user-attachments/assets/e7660488-62ed-4933-9d1a-5308d3063ab3" />
<img width="1902" height="897" alt="image" src="https://github.com/user-attachments/assets/33103c36-0f12-4af7-8913-b504ae6a29b0" />
<img width="1905" height="847" alt="image" src="https://github.com/user-attachments/assets/93355958-1009-494b-9966-c1b9e7351d16" />
<img width="1912" height="872" alt="image" src="https://github.com/user-attachments/assets/a1995fee-8ce3-48fc-b240-e00ee6788879" />

