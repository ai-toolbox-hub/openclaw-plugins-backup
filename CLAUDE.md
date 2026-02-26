```
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.
```

## Repository Overview

This repository is a **multi-component project** focused on OpenClaw backup solutions and related tools:

1. **Root directory**: Backup solutions analysis and documentation (Markdown files)
2. **clawpal/**: Tauri-based desktop companion app for OpenClaw (Rust + React/TypeScript)
3. **openclaw/**: OpenClaw AI assistant main project (Node.js/TypeScript)

---

## OpenClaw Main Project (openclaw/ directory)

### Overview
OpenClaw is a personal AI assistant that runs on your own devices, supporting multiple messaging channels (WhatsApp, Telegram, Slack, Discord, etc.) and voice interaction.

### Key Details
- **CLAUDE.md**: Symlinked to `AGENTS.md` with comprehensive guidelines (runs `pnpm openclaw` commands)
- **Package Manager**: pnpm (v10.23.0)
- **Node Version**: ≥22.12.0
- **Main Documentation**: `README.md`, `VISION.md`, `SECURITY.md`

### Development Commands

```bash
cd openclaw/

# Install dependencies
pnpm install

# Run CLI in development
pnpm openclaw <command>
pnpm dev                      # Run in dev mode

# Build
pnpm build

# Check / Lint
pnpm check                    # Format + lint + typecheck
pnpm format:fix               # Auto-format code
pnpm lint:fix                 # Auto-fix lint issues

# Test
pnpm test                     # Run all tests (vitest)
pnpm test:fast                # Run unit tests only
pnpm test:coverage            # Run with coverage (V8)
pnpm test:e2e                 # Run e2e tests
pnpm test:live                # Run live tests with real API keys

# Typecheck
pnpm tsgo                     # TypeScript checks
```

### Project Structure
- `src/`: Core application code (CLI, commands, web provider, media pipeline)
- `extensions/`: Channel plugins (WhatsApp, Telegram, Slack, etc.)
- `skills/`: AI skills
- `apps/`: Mobile apps (iOS, Android) + macOS app
- `docs/`: Documentation
- `test/`: Tests (vitest)

---

## ClawPal Desktop App (clawpal/ directory)

### Overview
A Tauri-based desktop companion app for OpenClaw that provides a visual interface for managing agents, models, and configurations.

### Tech Stack
- **Frontend**: React 18 + TypeScript + Tailwind CSS + Radix UI
- **Backend**: Rust + Tauri 2
- **Remote Management**: russh (SSH/SFTP)
- **Package Manager**: Bun

### Development Commands

```bash
cd clawpal/

# Install dependencies
bun install

# Development (Vite dev server + Tauri window)
bun run dev:tauri

# Build
bun run build:tauri

# Lint / Typecheck
bun run lint          # TypeScript typecheck
bun run typecheck     # Same as lint

# Tests (Rust backend)
cd src-tauri/
cargo test            # Run all Rust tests
cargo test cli_runner_test  # Run specific test file
cargo test remote_api       # Run specific test module

# Release
bun run release:dry-run  # Preview version bump + tag
bun run release          # Tag and push (triggers CI)
```

### Environment Variables
```bash
export CLAWPAL_OPENCLAW_DIR="$HOME/.openclaw"   # OpenClaw config directory (default)
export CLAWPAL_DATA_DIR="$HOME/.clawpal"        # ClawPal metadata directory
```

### Project Structure
- `src/`: React/TypeScript frontend
- `src-tauri/`: Rust backend + Tauri configuration
- `docs/plans/`: Implementation plans and design documents

---

## OpenClaw Backup Analysis (Root Directory)

### Core Documentation
- `备份方案分析.md`: Comprehensive analysis of current backup方案 and Rsync-based improvements
- `README.md`: Project overview and Rsync technical benefits
- `docs/`: Case studies, examples, and performance data

### Current OpenClaw Backup Capabilities
**Important**: OpenClaw and ClawPal lack comprehensive backup functionality. Current limitations:

| Feature | Status | Description |
|---------|--------|-------------|
| **Incremental Backup** | ❌ Not supported | No differential or incremental backup algorithm |
| **Configuration Backup** | ✅ Basic | Config file backup (5 versions: .bak, .bak.1, .bak.2, .bak.3, .bak.4) |
| **Data Backup** | ❌ Missing | No full system or user data backup |
| **Recovery Mechanism** | ❌ Manual only | No automated restore process |
| **Backup Scheduling** | ❌ None | No cron or schedule support |

### Rsync-Based Improvement Benefits
- **Incremental sync**: 70-90% reduction in transfer volume
- **Storage efficiency**: 50-80% improvement in storage utilization
- **Network resilience**: Resume on network failure (断点续传)
- **Faster recovery**: 60-80% reduction in restore time
- **Compression**: 30-60% reduction in network traffic

### Development and Collaboration
- **Documentation Language**: Chinese (主要面向中文用户)
- **File Format**: Markdown with structured headers
- **Version Control**: Git (each subcomponent is a separate repo)
