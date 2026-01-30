# Tamagotchi AI

A virtual pet game with AI-powered conversations using Claude LLM.

## Features

- 🥚 Raise your pet from an egg through 5 evolution stages: EGG → BABY → CHILD → TEEN → ADULT
- 💬 **Chat with your pet!** Each stage has a unique personality and speech style
- 🎮 Mini-games: Guess Direction, Memory Match, Dodge
- 📊 Track stats: Hunger, Happiness, Energy, Hygiene, Health
- 👗 Unlock accessories by solving math riddles (K-4 grade levels)
- 💾 Auto-save to localStorage with offline progress

## Chat Personalities by Stage

| Stage | Personality |
|-------|-------------|
| BABY | Cute baby talk, simple words, very affectionate |
| CHILD | Curious and playful, asks lots of questions |
| TEEN | Moody but thoughtful, developing opinions |
| ADULT | Wise and emotionally mature, grateful |

## Math-Locked Accessories

| Level | Accessories | Math Type |
|-------|-------------|-----------|
| 1 (Easy) | Sunglasses, Party Hat, Headphones | + / - up to 10 |
| 2 (Medium) | Star, Rainbow, Rocket | + / - up to 20 |
| 3 (Tricky) | Diamond, Fire, Lightning | + / - / × up to 12 |
| 4 (Challenge) | Unicorn, Dragon, Alien | + / - / × / ÷ up to 12 |

---

## Deployment (Vercel)

### 1. Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

Or connect your GitHub repo to Vercel for automatic deployments.

### 2. Set Environment Variables

In Vercel dashboard → Settings → Environment Variables:

```
ANTHROPIC_API_KEY=your_api_key_here
```

### 3. Share the URL

Your app will be available at `https://your-project.vercel.app`

---

## Local Development

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

### 4. Open the Game

Navigate to `http://localhost:3000` in your browser.

---

## Project Structure

```
tamagotchi-ai/
├── index.html          # Main game (frontend)
├── api/
│   └── chat.js         # Vercel serverless function for Claude API
├── server/
│   └── server.js       # Local Express server
├── supabase/
│   └── schema.sql      # Database schema (for future auth)
├── package.json        # Root dependencies for Vercel
├── vercel.json         # Vercel configuration
└── README.md
```

## API Endpoints

- `POST /api/chat` - Send a message to your pet
  - Body: `{ message, petState, conversationHistory }`
  - Returns: `{ response, stage, mood }`

---

## Future: Supabase Integration

The `supabase/schema.sql` file contains the database schema for:
- User authentication
- Pet data persistence across devices
- Unlocked accessories tracking
- Math riddle history

To set up:
1. Create a Supabase project at https://supabase.com
2. Run the schema.sql in the SQL Editor
3. Add Supabase credentials to environment variables
