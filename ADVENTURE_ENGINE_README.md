# Infinite AI Adventure Engine

An immersive, AI-powered choose-your-own-adventure game with real-time visuals, voice interaction, and dynamic storytelling.

## Features

### 🎭 AI-Driven Content Generation
- **Dynamic Narratives**: LLM-powered storytelling that adapts to your choices
- **NPC Generation**: Characters with unique personalities, goals, and relationships
- **Emergent Gameplay**: Every action creates meaningful consequences
- **World Evolution**: Environments change based on your decisions

### 🎨 Real-Time Visuals
- **Scene Generation**: AI creates atmospheric images for each story beat
- **Contextual Imagery**: Visuals reflect narrative tone and world state
- **Multiple Formats**: Supports various image sizes (portrait, landscape, etc.)

### 🎤 Voice Interaction
- **Voice Input**: Speak your actions using speech-to-text
- **Voice Narration**: AI responses are read aloud
- **Natural Dialogue**: Low-latency voice chat experience

### 📊 Dynamic Game Systems
- **Inventory**: Items with rarity (common, rare, epic, legendary) and quantities
- **Quests**: Dynamic quest tracking with priorities (low, normal, high)
- **Relationships**: NPC affinity tracking with status indicators
- **Reputation**: Faction standings that affect gameplay
- **Character Stats**: Health, gold, level, and experience

## How to Play

### Getting Started
1. Open the application in your browser
2. The game automatically initializes with a new story
3. Read the opening scene and the generated image

### Making Choices
- **Text Input**: Type your action in the input field and press Enter or click Send
- **Voice Input**: Click the microphone button to speak your action
  - Click again to stop recording
  - Your speech will be transcribed automatically

### Viewing Game State
- **Inventory Tab**: View your items with rarity badges and quantities
- **Quests Tab**: See active quests and their priorities
- **NPCs Tab**: Check relationship statuses and affinity meters
- **Reputation**: View faction standings (appears when available)

### Audio Controls
- **Play Narration**: Click the speaker icon to hear AI responses
- **Auto-Generation**: Audio is generated for each new scene

### Game Controls
- **New Game**: Click the refresh icon to start a fresh adventure
- **Health/Gold**: Displayed in the header for quick reference
- **Location/Time**: Shows your current location and time of day

## Game Mechanics

### Inventory System
- Items have rarity levels: common, rare, epic, legendary
- Quantity tracks consumables
- Items are added/removed based on your actions

### Quest System
- Quests appear automatically based on story developments
- Priority levels: low (optional), normal (recommended), high (urgent)
- Quests complete when objectives are fulfilled

### Relationship System
- Affinity scale: 0-100
  - 0-29: Hostile
  - 30-69: Neutral
  - 70-89: Friendly
  - 90-100: Ally
- Interaction count tracks encounters
- Affinity changes based on your choices

### Reputation System
- Faction reputation can be positive or negative
- Affects NPC reactions and prices
- Influences world events and quest availability

### Combat & Survival
- Health: 0-100, affected by hazards and combat
- Gold: Currency for purchases and rewards
- Experience: Gained through actions, affects level

## Technical Implementation

### Backend APIs

#### `/api/adventure/init`
Initializes a new game session with AI-generated opening scene.

**Request:** `POST`
```json
{}
```

**Response:**
```json
{
  "success": true,
  "sessionId": "session-id",
  "gameState": {...},
  "dialogues": [...],
  "inventory": [...],
  "quests": [...],
  "relationships": [...],
  "reputation": [...]
}
```

#### `/api/adventure/action`
Processes a player action and generates the next story beat.

**Request:** `POST`
```json
{
  "sessionId": "session-id",
  "action": "I look around the forest"
}
```

**Response:**
```json
{
  "success": true,
  "response": "The AI-generated narrative...",
  "gameState": {...},
  "inventory": [...],
  "quests": [...],
  "relationships": [...],
  "reputation": [...],
  "imagePrompt": "Visual description..."
}
```

#### `/api/adventure/image`
Generates a scene image based on narrative description.

**Request:** `POST`
```json
{
  "sessionId": "session-id",
  "description": "A dense forest with ancient trees..."
}
```

**Response:**
```json
{
  "success": true,
  "image": "base64-encoded-image-data"
}
```

#### `/api/adventure/tts`
Generates voice narration for text.

**Request:** `POST`
```json
{
  "text": "The text to narrate",
  "voice": "tongtong",
  "speed": 1.0
}
```

**Response:**
```json
{
  "success": true,
  "audio": "base64-encoded-wav-audio"
}
```

#### `/api/adventure/transcribe`
Transcribes voice input to text.

**Request:** `POST` (FormData)
```
audio: File (WAV/MP3/etc.)
sessionId: string
```

**Response:**
```json
{
  "success": true,
  "text": "Transcribed speech"
}
```

### Database Schema

```prisma
model GameSession {
  id          String    @id @default(cuid())
  playerState  GameState?
  inventory    Inventory[]
  quests       Quest[]
  relationships Relationship[]
  reputation   Reputation[]
  characters   Character[]
  worldStates  WorldState[]
  dialogues    DialogueHistory[]
}

model GameState {
  id              String   @id @default(cuid())
  sessionId       String   @unique
  session         GameSession @relation
  health          Int      @default(100)
  maxHealth       Int      @default(100)
  gold            Int      @default(0)
  level           Int      @default(1)
  experience      Int      @default(0)
  location        String?
  timeOfDay       String   @default("day")
  currentScene    String?
  currentImagePrompt String?
  lastAction      String?
}

model Inventory {
  id        String  @id @default(cuid())
  sessionId  String
  itemName  String
  description String?
  quantity  Int     @default(1)
  rarity    String  @default("common")
  itemType  String  @default("item")
}

model Quest {
  id          String  @id @default(cuid())
  sessionId   String
  title       String
  description String
  objectives  String  // JSON
  status      String  @default("active")
  priority    String  @default("normal")
}

model Relationship {
  id               String  @id @default(cuid())
  sessionId        String
  npcName          String
  npcRole          String?
  affinity         Int     @default(50)
  status           String  @default("neutral")
  interactionCount Int     @default(0)
}

model Reputation {
  id          String  @id @default(cuid())
  sessionId   String
  factionName String
  factionType String?
  reputation  Int     @default(0)
  description String?
}
```

## Technology Stack

- **Framework**: Next.js 15 with App Router
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS 4
- **UI Components**: shadcn/ui
- **Database**: Prisma ORM + SQLite
- **AI SDK**: z-ai-web-dev-sdk
  - LLM for narrative generation
  - Image Generation for scenes
  - TTS for voice narration
  - ASR for voice input

## Development

### Running the Development Server
```bash
bun run dev
```

### Running Linter
```bash
bun run lint
```

### Database Operations
```bash
bun run db:push      # Push schema changes to database
bun run db:generate  # Generate Prisma Client
bun run db:migrate   # Create migration
bun run db:reset     # Reset database
```

## Tips for Players

1. **Be Specific**: Describe your actions clearly for better AI responses
2. **Experiment**: Try unexpected choices—the game adapts!
3. **Pay Attention**: Note relationship changes and reputation shifts
4. **Explore**: Ask about your surroundings to discover secrets
5. **Build Connections**: Talk to NPCs and build relationships
6. **Manage Resources**: Your choices affect health, gold, and inventory
7. **Follow Quests**: High-priority quests often lead to major story developments
8. **Use Voice**: Voice input can feel more immersive and natural

## Future Enhancements

Potential features to add:
- [ ] Save/Load game sessions
- [ ] Multiple character classes
- [ ] Skill system
- [ ] Crafting mechanics
- [ ] Multiplayer campaigns
- [ ] Achievements system
- [ ] Story branches and endings
- [ ] Custom world generation settings
- [ ] Export story as a novel

## License

This project is built as a demonstration of AI-powered interactive storytelling.

---

Enjoy your infinite adventure! 🎮✨
