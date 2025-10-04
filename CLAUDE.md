# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file HTML chess application designed for tabletop play on tablets/iPads. Two players sit across from each other with the device flat on a table between them. The game features:

- 2D top-down chess board with Unicode chess pieces (♔♕♖♗♘♙ / ♚♛♜♝♞♟)
- Timer displays duplicated and rotated so both players can read their opponent's time
- localStorage-based persistence (survives page refreshes)
- Move validation, check/checkmate/stalemate detection via chess.js library

## Architecture

The application is structured as a single HTML file (`tabletop-chess.html`) with inline CSS and JavaScript organized into classes:

### Core Classes

- **StorageManager** - Handles localStorage save/load/clear operations for game state
- **GameState** - Manages chess logic (via chess.js), timer state, move validation, game status checks
- **BoardRenderer** - Renders the 8×8 grid, handles piece selection, legal move highlighting, and click events
- **TimerDisplay** - Updates timer displays (4 timer elements: white top/bottom, black top/bottom), manages active player indication
- **ChessGame** - Main controller that initializes all components and wires up controls

### Key Design Decisions

1. **Dual Timer Display**: Each player's timer appears at both top and bottom of board (one rotated 180°) so both players can read all times without rotating their view

2. **localStorage Schema**:
   ```javascript
   {
     fen: "rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1",
     whiteTime: 600,
     blackTime: 600,
     lastUpdate: 1234567890,
     gameOver: false
   }
   ```

3. **Move Flow**: Select piece → highlight legal moves → click destination → update timer → save state → render

## External Dependencies

- **chess.js** (v0.10.3): Loaded from CDN, provides Chess() class for move validation and game state
  - Methods used: `move()`, `moves()`, `board()`, `get()`, `turn()`, `fen()`, `load()`, `reset()`, `in_checkmate()`, `in_draw()`, `in_stalemate()`, `in_check()`

## Development Notes

- This is a **single-file application** - all HTML, CSS, and JavaScript are in `tabletop-chess.html`
- No build process, package manager, or testing framework
- Open directly in browser (no server required)
- Uses vmin units throughout for responsive sizing across different screen sizes
- Timer update interval: 100ms (see TimerDisplay constructor)
- Default game time: 600 seconds (10 minutes) per player

## Common Modifications

**Changing default time**: Update `whiteTime` and `blackTime` initialization in GameState constructor (line ~225-226) and reset() method (line ~301-302)

**Changing board colors**: Modify `.square.light` and `.square.dark` background colors in CSS (line ~51-57)

**Adjusting piece size**: Change font-size in `.square` class (line ~45)

## Testing

No automated tests. Test manually by:
1. Open `tabletop-chess.html` in browser
2. Verify move validation, timer countdown, localStorage persistence
3. Test on target device (iPad) for size/readability
