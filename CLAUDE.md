# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Tamagotchi AI is a virtual pet game with AI-powered chat. The frontend is a single-page canvas-based app (vanilla JS in `index.html`), and the backend is a Node.js/Express server that proxies chat requests to the Anthropic Claude API.

## Development Commands

All commands run from the `server/` directory:

```bash
cd server
npm install          # Install dependencies
npm run dev          # Development mode (node --watch, auto-reloads)
npm start            # Production mode (node server.js)
```

The app serves on `http://localhost:3000`. No build step, linting, or test suite exists.

## Architecture

**Frontend (`index.html`)** — Single monolithic file (~2000 lines) containing all HTML, CSS, and JavaScript inline. Uses HTML5 Canvas for rendering with a game loop. Key sections:
- Pet drawing and stage-specific animations (~lines 413-928)
- Game state management and evolution logic (~lines 931-1070)
- Three minigames: Guess Direction, Memory Match, Dodge (~lines 1347-1650)
- Chat functionality with speech bubble UI (~lines 1750-1950)
- State persisted to localStorage under key `tamagotchi_ai_save_v2`

**Backend (`server/server.js`)** — Express server with two endpoints:
- `POST /api/chat` — Sends user message + pet state to Claude API (`claude-sonnet-4-20250514`). Constructs dynamic system prompts based on pet's evolution stage (EGG/BABY/CHILD/TEEN/ADULT), mood, and stats to give the pet stage-appropriate personality.
- `GET /api/health` — Health check.

**Data flow for chat**: Frontend sends message + full pet state + conversation history → Backend builds stage-specific system prompt → Claude API responds → Response displayed as speech bubble with sound effects.

## Key Game Mechanics

- **Evolution stages**: EGG (2min) → BABY (30min) → CHILD (60min) → TEEN (90min) → ADULT (permanent). Time thresholds are in milliseconds in the source.
- **Stats**: hunger, happiness, energy, hygiene, health — all 0-100, continuously decaying at different rates.
- **Offline simulation**: Up to 8 hours of offline stat decay applied on return.

## Configuration

`server/.env` must contain `ANTHROPIC_API_KEY`. Port defaults to 3000 (configurable via `PORT` env var).
