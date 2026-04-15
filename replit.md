# SignSync - Sign Language Recognition System

## Overview

AI-powered sign language recognition system with NLP-based autocomplete. Built as a React + Vite frontend with Express backend in a pnpm workspace monorepo.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite + Tailwind CSS + shadcn/ui
- **Backend**: Express 5
- **Hand Detection**: MediaPipe Hands (browser-side)
- **NLP**: Custom N-gram model (bigram/trigram) for autocomplete
- **TTS**: Web Speech API (browser-side)
- **Database**: PostgreSQL + Drizzle ORM (available but not used for core features)
- **Validation**: Zod
- **API codegen**: Orval (from OpenAPI spec)

## Architecture

### Frontend (artifacts/sign-language)
- **Webcam Feed**: Uses MediaPipe Hands for real-time hand landmark detection in the browser
- **Gesture Classification**: Sends detected landmarks to backend API for classification
- **Sentence Builder**: Accumulates detected words into running sentences
- **Autocomplete Panel**: Shows NLP-predicted next words with confidence scores
- **Text-to-Speech**: Browser SpeechSynthesis API for reading sentences aloud
- **Language Support**: English and Hindi toggle
- **History**: Stores completed sentences in localStorage

### Backend (artifacts/api-server)
- **POST /api/classify-gesture**: Classifies hand landmarks into sign language words using geometric analysis
- **POST /api/autocomplete**: Returns word suggestions using N-gram language model
- **GET /api/supported-gestures**: Returns list of all supported gestures
- **POST /api/sentence-stats**: Returns sentence statistics and completeness

### Supported Gestures (16 words)
hello, yes, no, thank you, please, help, water, food, I, you, want, good, sorry, stop, love, go

### NLP Autocomplete
- Bigram and trigram models trained on conversational sentence corpus
- Supports both English and Hindi
- Returns top 5 suggestions with confidence scores
- Keyboard shortcuts (1-5) for quick selection

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas
- `pnpm --filter @workspace/api-server run dev` — run API server locally
- `pnpm --filter @workspace/sign-language run dev` — run frontend locally

## Pages

- `/` — Main translation page with webcam, sentence builder, autocomplete
- `/guide` — Reference guide for all supported gestures
- `/history` — History of translated sentences

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
