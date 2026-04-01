# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Browser-based retro games built as single-file HTML applications with no external dependencies. Each game is a standalone `.html` file using inline CSS and JavaScript.

## Running

Open any `.html` file directly in a browser. No build step, no server, no package manager.

```bash
start shooter.html    # Windows
open shooter.html     # macOS
```

## Architecture

### shooter.html — "RETRO BLASTER" (top-down shooter)
- **Rendering:** Canvas API at internal 400x300 resolution, CSS-scaled 2x to 800x600 with `image-rendering: pixelated` for retro look
- **Game loop:** `requestAnimationFrame` with delta-time (capped at 50ms)
- **State machine:** `MENU → PLAYING → GAME_OVER`, with wave sub-states `WAVE_INTRO → WAVE_ACTIVE → WAVE_CLEAR`
- **Entities:** Plain object literals in arrays (`bullets[]`, `enemies[]`, `particles[]`), filtered each frame to remove dead ones
- **Sprites:** All drawn procedurally with `ctx.fillRect` — no image assets
- **Code sections** are marked with `// === SECTION X: NAME ===` comments: Constants, State, Input, Utilities, Sprites, Factories, Update, Render, Game Management, Init

### tictactoe.html — Tic Tac Toe
- DOM-based (no canvas), CSS Grid layout
- Minimax AI opponent (plays optimally)
- Score tracking across rounds

## Conventions

- **No external dependencies.** Everything is vanilla HTML/CSS/JS in a single file per game.
- **Procedural pixel-art sprites** via canvas draw calls (fillRect, arc, etc.) — no image files.
- All tunable gameplay values (speeds, cooldowns, HP, colors) live in the constants section at the top of the file.
- Level progression is configured via `getLevelConfig(level)` which returns enemy count, speed, HP, spawn rate, and available enemy types.

## Git Workflow

- Remote: `origin` → `github.com/DuaaSalem/retro-blaster`
- Branch: `master`
- `gh` CLI is available at `/c/Program Files/GitHub CLI` (add to PATH: `export PATH="$PATH:/c/Program Files/GitHub CLI"`)

**IMPORTANT:** Commit and push to GitHub regularly as you work. After completing any meaningful change (new feature, bug fix, refactor, etc.), immediately commit with a clean, descriptive message and push to origin. This ensures we never lose progress and can always revert if needed. Do not batch up multiple unrelated changes into one commit — keep commits focused and atomic.
