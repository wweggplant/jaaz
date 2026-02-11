# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Jaaz is an open-source multimodal creative assistant - a Canva AI alternative that supports local-first privacy-focused design workflows. It's a desktop application built with Electron, featuring a React frontend and FastAPI Python backend for AI-powered design generation.

## Architecture

This is a multi-component desktop application with these main parts:

- **`electron/`**: Electron main process and preload scripts
- **`react/`**: Vite-based React frontend with TypeScript  
- **`server/`**: FastAPI Python backend with AI services
- **Root package.json**: Electron app configuration and build scripts

### Key Architecture Components

**Frontend (React)**:
- Built with Vite, React 19, TypeScript
- Uses TanStack Router for navigation and TanStack Query for state management
- UI built with Radix UI components and Tailwind CSS
- Canvas functionality using Excalidraw and tldraw
- Internationalization with react-i18next

**Backend (Python)**:
- FastAPI server with WebSocket support for real-time communication
- LangGraph-based AI agent system for multimodal content generation
- Supports multiple AI providers (OpenAI, Anthropic, local models via ComfyUI)
- Structured with routers, services, models, and tools directories
- SQLite database with migration system

**Desktop Integration**:
- Electron app with IPC communication between main and renderer processes
- ComfyUI integration for local AI image generation
- Auto-updater functionality
- Cross-platform support (Windows, macOS, Linux)

## Development Commands

### Frontend Development
```bash
cd react
npm install --force
npm run dev
```

### Backend Development  
```bash
cd server
pip install -r requirements.txt
python main.py
```

### Full Development Setup
```bash
# From root directory
npm run dev  # Runs both frontend and backend concurrently
```

### Building
```bash
# Build React app
cd react && npm run build

# Build full Electron app
npm run start  # Builds React then starts Electron

# Platform-specific builds
npm run build:mac
npm run build:win
npm run build:linux
```

### Testing
```bash
# Frontend tests (in react/)
npm run test
npm run test:run

# Root level tests
npm test
npm run test:run
```

### Code Quality
Python code follows Black formatting (line length 88) and uses Ruff for linting as configured in `pyproject.toml`.

## Key Services and APIs

**AI Generation**: 
- Image generation via multiple providers in `server/tools/`
- Video generation tools in `server/tools/video_generation/`
- Agent-based workflows in `server/services/langgraph_service/`

**Canvas System**:
- Magic canvas functionality for AI-assisted design
- Real-time collaboration support
- Export capabilities to various formats

**Configuration Management**:
- Settings service for AI provider configurations
- Database service for persistent storage
- WebSocket service for real-time updates

## Requirements

- **Python**: >= 3.12 (specified in README.md)
- **Node.js**: For React frontend and Electron
- **Platform**: Windows, macOS, or Linux for desktop builds

## Important Development Notes

- Use `npm install --force` in react directory due to dependency conflicts
- Server requires Python 3.12+ for proper AI library compatibility
- ComfyUI integration requires additional setup for local AI generation
- WebSocket imports must remain in server/main.py for proper functionality