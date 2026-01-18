# Infinite AI Adventure Engine - Feature Documentation

## Table of Contents
- [Core Features](#core-features)
- [Game Systems](#game-systems)
- [AI & Media Integration](#ai--media-integration)
- [User Interface](#user-interface)
- [Data & Persistence](#data--persistence)
- [API Endpoints](#api-endpoints)

---

## Core Features

### 1. Dynamic Narrative Generation
**Overview**: AI-powered storytelling that adapts to player actions and choices
- Generates contextual story responses based on player input
- Maintains narrative coherence across sessions
- Supports multiple action types with specialized narrative responses
- Integrates character personalities, world states, and relationship dynamics

### 2. Character System
**Overview**: Comprehensive character management for player and NPCs
- **Player Character**: Tracks stats, inventory, relationships, quests, reputation
- **NPC System**: Full character profiles with personality, goals, motivations, and memory
- **Relationship Tracking**: Dynamic relationship scores (0-100) with each NPC
- **NPC Memory**: Remembers past interactions, world knowledge, secrets, and recent encounters

### 3. Action System
**Overview**: Five action types with specialized AI responses
- **Do**: Physical or mental actions by the player character
- **Say**: Dialogue that AI incorporates into narrative
- **See**: Observation and inspection of environment, objects, or characters
- **Story**: Player-directed narrative elements and background details
- **Wait**: Time advancement with potential random events

### 4. Visual Scene Generation
**Overview**: Real-time AI-generated images for game scenes
- 1344x768 resolution scene images
- Context-aware visual representations of current location
- Dynamic visual feedback based on story progression

### 5. Voice Interaction System
**Overview**: Complete voice input and output capabilities
- **Text-to-Speech (TTS)**: AI-generated narration in WAV format
- **Speech-to-Text (ASR)**: Voice input transcription for actions
- Multiple voice options with adjustable speed
- Base64 audio encoding for web compatibility

---

## Game Systems

### 1. Inventory System
**Overview**: Item management with tracking and usage
- Persistent inventory storage
- Item descriptions and metadata
- Integration with actions (use, equip, drop)

### 2. Quest System
**Overview**: Mission and objective tracking
- Active and completed quests
- Quest objectives and progress
- Main quests vs side quests distinction
- Dynamic quest updates based on story events

### 3. Reputation System
**Overview**: Global and faction-based reputation tracking
- Numerical reputation scores
- Faction-specific reputation
- Impact on NPC interactions and story outcomes

### 4. Relationship System
**Overview**: Character-to-character relationship dynamics
- Relationship scores with each NPC (0-100)
- Visual relationship indicators (color-coded badges)
- Relationship states: Hostile, Neutral, Friendly, Allied
- Relationship history tracking

### 5. World State System
**Overview**: Global world condition tracking
- Current location and environment state
- World events and flags
- Time and progression tracking
- Dynamic world changes based on player actions

### 6. NPC Memory System
**Overview**: NPCs remember and learn from interactions
- **Memory Field**: Records past interactions and events
- **Knowledge Field**: World knowledge and lore known to NPC
- **Secrets Known**: Secrets the NPC has discovered
- **Recent Interactions**: Log of recent encounters with player
- Influences NPC behavior, dialogue, and story development

### 7. Dialogue History System
**Overview**: Complete record of all interactions
- Narrative log with all story elements
- Player action history
- NPC dialogue history
- Searchable narrative database

---

## AI & Media Integration

### 1. Large Language Model (LLM) Integration
**SDK**: z-ai-web-dev-sdk LLM
- Generates dynamic narrative responses
- Context-aware story progression
- Multi-turn conversation support
- Character-specific dialogue generation
- World and lore generation

### 2. Vision Language Model (VLM)
**SDK**: Nano Banana Pro (Gemini 3 Pro)
- Scene understanding for image generation prompts
- Context-aware visual descriptions
- Image-text consistency

### 3. Image Generation
**SDK**: z-ai-web-dev-sdk Image Generation
- Real-time scene visualization
- High-resolution output (1344x768)
- Style consistency settings
- Base64 encoding for web delivery

### 4. Text-to-Speech (TTS)
**SDK**: z-ai-web-dev-sdk TTS
- WAV format audio output
- Multiple voice options
- Adjustable speech speed (0.5x - 2.0x)
- Base64 encoded audio delivery

### 5. Speech Recognition (ASR)
**SDK**: z-ai-web-dev-sdk ASR
- Base64 audio input processing
- Multi-format support (WAV, MP3, M4A, WEBM)
- High transcription accuracy
- Context-aware transcription

---

## User Interface

### 1. Main Menu Screen
**Features**:
- Start New Adventure
- Load Adventure (from saved games)
- Exit application
- Clean, modern design with shadcn/ui components

### 2. New Game Settings Screen
**Features**:
- **Setting**: World/environment type (e.g., Medieval Fantasy, Sci-Fi, Post-Apocalyptic)
- **Genre/Themes**: Narrative themes (e.g., Adventure, Horror, Mystery)
- **Plot Essentials**: Core story elements
- **Media Type**: Style inspiration (e.g., Game, Show, Movie, Book)
- Customizable world generation parameters

### 3. Game Interface (AI Dungeon Style)
**Components**:
- **Narrative Chat Log**: Scrollable story display with auto-scroll
- **Visual Scene Display**: Large image showing current location
- **Action Input**: Text field with voice recording button
- **Quick Action Buttons**: Do, Say, See, Story, Wait
- **Dynamic Sidebar**: Collapsible panels for Inventory, Quests, Relationships, Reputation

### 4. Sidebar Panels
**Inventory Panel**:
- List of player items
- Item descriptions
- Item counts and states

**Quests Panel**:
- Active quests with progress
- Completed quests history
- Quest objectives and status

**Relationships Panel**:
- List of NPCs with relationship status
- Color-coded badges (Red=Hostile, Gray=Neutral, Green=Friendly, Blue=Allied)
- Relationship score (0-100) with progress bar
- NPC character badge
- Interaction count

**Reputation Panel**:
- Faction reputation scores
- Global reputation status

### 5. Visual Design Elements
- Responsive design (mobile-first)
- Light/dark mode support
- Sticky footer with proper flex layout
- Touch-friendly interactive elements (44px minimum)
- Loading states and spinners
- Error handling with clear messages
- Toast notifications for user actions
- Subtle Framer Motion animations

### 6. Accessibility Features
- Semantic HTML (main, header, nav, section, article)
- ARIA support for screen readers
- Keyboard navigation
- Descriptive alt text for images
- sr-only class for screen reader content

---

## Data & Persistence

### 1. Database Schema (Prisma + SQLite)
**Models**:
- **GameSession**: Session tracking and metadata
- **GameState**: Player stats, location, progression
- **Inventory**: Item management
- **Quest**: Quest tracking and objectives
- **Relationship**: Character relationship data
- **Reputation**: Faction reputation tracking
- **Character**: Full character profiles with NPC memory
- **WorldState**: Global world conditions
- **DialogueHistory**: Complete narrative log

### 2. Game State Persistence
**Features**:
- Database transaction support for atomic updates
- Complete state serialization to JSON
- All player, NPC, and world states saved/loaded
- Relationship history preservation
- NPC memory persistence

### 3. Save/Load System (localStorage)
**Features**:
- Save current game state to localStorage
- Load previously saved games
- Delete saved games
- Multiple save slots support
- Automatic state serialization/deserialization
- SavedGame interface with metadata (name, date, summary)

### 4. NPC Memory Persistence
**Fields**:
- `memory`: Stringified JSON of remembered events
- `knowledge`: Stringified JSON of world knowledge
- `secretsKnown`: Stringified JSON array of secrets
- `recentInteractions`: Stringified JSON array of recent encounters
- All memory fields persisted in database and saved games

---

## API Endpoints

### 1. Initialize Adventure
**Route**: `POST /api/adventure/init`
**Purpose**: Generate initial world, characters, and game state
**Parameters**:
- setting (string): World/environment type
- genre (string): Narrative themes
- plotEssentials (string): Core story elements
- mediaType (string): Style inspiration
**Returns**: Complete initial game state with NPCs, quests, inventory, relationships

### 2. Process Player Action
**Route**: `POST /api/adventure/action`
**Purpose**: Process player actions and generate narrative response
**Parameters**:
- actionType (enum): 'do' | 'say' | 'see' | 'story' | 'wait'
- action (string): Player action description
- gameState (object): Current game state
**Returns**:
- AI-generated narrative response
- Updated game state (stats, inventory, quests, relationships, NPC memory)
- Suggested next actions

### 3. Generate Scene Image
**Route**: `POST /api/adventure/image`
**Purpose**: Generate visual representation of current scene
**Parameters**:
- sceneDescription (string): Scene context from narrative
- setting (string): World setting
**Returns**: Base64 encoded image (1344x768, JPEG/PNG)

### 4. Generate Narration Audio
**Route**: `POST /api/adventure/tts`
**Purpose**: Convert narrative text to speech
**Parameters**:
- text (string): Narrative text to speak
- voice (string): Voice selection
- speed (number): Speech speed (0.5-2.0)
**Returns**: Base64 encoded WAV audio

### 5. Transcribe Voice Input
**Route**: `POST /api/adventure/transcribe`
**Purpose**: Convert voice recording to text
**Parameters**:
- audio (FormData): Audio file upload (WAV, MP3, M4A, WEBM)
**Returns**: Transcribed text string

---

## Technical Stack

### Frontend
- **Framework**: Next.js 15 with App Router
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS 4
- **UI Components**: shadcn/ui (New York style)
- **Icons**: Lucide React
- **State Management**: React Hooks (useState, useRef, useEffect)
- **Theme**: next-themes for light/dark mode
- **Animations**: Framer Motion

### Backend
- **Runtime**: Bun
- **Database**: SQLite with Prisma ORM
- **AI SDK**: z-ai-web-dev-sdk
- **Caching**: Local memory caching

### Media
- **Audio**: MediaRecorder API for recording
- **Encoding**: Base64 for audio/image transfer
- **Formats**: WAV (audio), JPEG/PNG (images)

---

## File Structure

```
/home/z/my-project/
├── prisma/
│   └── schema.prisma              # Database schema with NPC memory
├── src/
│   ├── app/
│   │   ├── page.tsx               # Main game interface (menu, new-game, game screens)
│   │   └── api/
│   │       └── adventure/
│   │           ├── init/
│   │           │   └── route.ts   # Initialize adventure with settings
│   │           ├── action/
│   │           │   └── route.ts   # Process player actions with NPC memory
│   │           ├── image/
│   │           │   └── route.ts   # Generate scene images
│   │           ├── tts/
│   │           │   └── route.ts   # Text-to-speech
│   │           └── transcribe/
│   │               └── route.ts   # Speech-to-text
│   ├── components/
│   │   └── ui/                    # shadcn/ui components
│   └── lib/
│       ├── db.ts                  # Prisma client
│       └── worklog.md             # Development work log
└── package.json                   # Dependencies and scripts
```

---

## Status
✅ All features implemented and tested
✅ Database schema with NPC memory system
✅ Complete frontend with 3 screens
✅ 5 API endpoints using z-ai-web-dev-sdk
✅ Save/Load system with localStorage
✅ Voice interaction (TTS + ASR)
✅ Real-time image generation
✅ NPC memory and relationship tracking
✅ ESLint checks passed (no errors or warnings)
✅ Ready for gameplay testing
