# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Claudable is a Next.js-based web app builder that integrates Claude Code, Cursor CLI, and other AI agents with a simple app building experience. It provides a web interface for creating, previewing, and deploying Next.js applications through AI assistance.

## Architecture

**Monorepo Structure:**
- `apps/web/` - Next.js frontend application (TypeScript, Tailwind CSS, shadcn/ui)
- `apps/api/` - FastAPI backend application (Python)
- `scripts/` - Node.js automation scripts for development workflow
- `data/` - SQLite database storage (auto-created)

**Backend (FastAPI):**
- SQLAlchemy ORM with SQLite (development) / PostgreSQL (production)
- Multiple CLI adapters: Claude Code, Cursor CLI, Codex CLI, Gemini CLI, Qwen Code
- WebSocket support for real-time chat
- Service integrations: GitHub, Vercel, Supabase

**Frontend (Next.js):**
- App Router with TypeScript
- Real-time chat interface with WebSocket connection
- Project management and live preview functionality
- Responsive design with Tailwind CSS and shadcn/ui components

## Development Commands

```bash
# Start both frontend and backend
npm run dev

# Start individual services
npm run dev:api    # Backend only (Python FastAPI)
npm run dev:web    # Frontend only (Next.js)

# Database operations
npm run db:backup  # Backup SQLite database
npm run db:reset   # Reset database (WARNING: deletes all data)

# Environment setup
npm run setup      # Full setup (dependencies + environment)
npm run clean      # Clean all dependencies and virtual environments
```

## Project Structure Details

**API Service Layer:**
- `app/services/cli/adapters/` - CLI tool integrations (Claude Code, Cursor, etc.)
- `app/services/` - Core services (GitHub, Vercel, filesystem operations)
- `app/api/` - FastAPI route handlers organized by feature
- `app/models/` - SQLAlchemy database models
- `app/core/` - Configuration, logging, WebSocket management

**Frontend Structure:**
- `app/` - Next.js App Router pages and components
- `components/` - Reusable UI components
- `contexts/` - React Context providers (Auth, GlobalSettings)
- `hooks/` - Custom React hooks
- `types/` - TypeScript type definitions

## Environment Configuration

The project uses automatic environment setup:
- `.env` files are auto-generated with available ports
- Frontend: http://localhost:3000 (or next available port)
- Backend: http://localhost:8080 (or next available port)
- Python virtual environment: `apps/api/.venv`

## CLI Agent Integration

The system supports multiple AI coding agents through adapter pattern:
- Claude Code (primary) - via Python SDK
- Cursor CLI - via subprocess execution
- Codex CLI - OpenAI integration
- Gemini CLI - Google AI integration
- Qwen Code - Alibaba open-source model

Each adapter implements the `BaseCLI` interface for consistent behavior across different AI agents.

## Key Technologies

- **Backend**: FastAPI, SQLAlchemy, WebSockets, asyncio
- **Frontend**: Next.js 14, React 18, TypeScript, Tailwind CSS
- **Database**: SQLite (development), PostgreSQL (production)
- **Deployment**: Vercel integration for frontend, various options for backend
- **AI Integration**: Multiple CLI agent adapters with unified interface