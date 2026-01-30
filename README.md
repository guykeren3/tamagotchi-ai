# Tamagotchi AI

A virtual pet game with AI-powered conversations using Claude LLM.

## Features

- 🥚 Raise your pet from an egg through 5 evolution stages: EGG → BABY → CHILD → TEEN → ADULT
- 💬 **Chat with your pet!** Each stage has a unique personality and speech style
- 🎮 Mini-games: Guess Direction, Memory Match, Dodge
- 📊 Track stats: Hunger, Happiness, Energy, Hygiene, Health
- 👗 Unlock accessories as your pet evolves
- 💾 Auto-save to localStorage with offline progress

## Chat Personalities by Stage

| Stage | Personality |
|-------|-------------|
| BABY | Cute baby talk, simple words, very affectionate |
| CHILD | Curious and playful, asks lots of questions |
| TEEN | Moody but thoughtful, developing opinions |
| ADULT | Wise and emotionally mature, grateful |

## Setup

### 1. Install Dependencies

```bash
cd server
npm install
```

### 2. Configure API Key

```bash
cd server
cp .env.example .env
```

Edit `.env` and add your Anthropic API key:

```
ANTHROPIC_API_KEY=your_actual_api_key_here
```

### 3. Run the Server

```bash
cd server
npm start
```

Or for development with auto-reload:

```bash
npm run dev
```

### 4. Open the Game

Navigate to `http://localhost:3000` in your browser.

## Project Structure

```
tamagotchi-ai/
├── index.html          # Main game (frontend)
├── README.md
└── server/
    ├── server.js       # Express server with Claude API
    ├── package.json
    ├── .env.example    # Environment template
    └── .gitignore
```

## API Endpoints

- `POST /api/chat` - Send a message to your pet
  - Body: `{ message, petState, conversationHistory }`
  - Returns: `{ response, stage, mood }`

- `GET /api/health` - Health check endpoint

## How the AI Works

The server constructs a dynamic system prompt based on:
- Pet's current stage (determines personality)
- Current mood and stats (hungry, tired, etc.)
- Pet's age and history

This makes the pet's responses contextual and stage-appropriate!

## Tips

- Your pet can only chat after hatching from the egg
- Chat with your pet regularly to boost happiness
- The pet will mention if it's hungry, tired, or unwell
- Conversation history is maintained for context (last 10 messages)
