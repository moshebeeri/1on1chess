# 1on1chess.com - Tabletop Chess for Two Players

A single-file HTML chess application designed for face-to-face play on tablets and iPads. Two players sit across from each other with the device flat on a table between them.

## 🎮 Live Demo

Visit **[1on1chess.com](https://1on1chess.com)** to play now!

## ✨ Features

### Core Gameplay
- **2D Chess Board** - Clean top-down view with Unicode chess pieces (♔♕♖♗♘♙ / ♚♛♜♝♞♟)
- **Move Validation** - Full chess rules via chess.js library
- **Check/Checkmate/Stalemate Detection** - Complete game state tracking
- **Visual Check Indicator** - Red glowing animation on king when in check

### Tabletop-Optimized Interface
- **Dual Timer Displays** - Each player's clock visible from both sides (rotated 180°)
- **Time Controls** - Popular formats with increment support:
  - 10+0 (Rapid)
  - 5+3, 3+2 (Blitz)
  - 1+0 (Bullet)
  - 15+10, 30+0 (Classical)
- **Active Clock Highlighting** - Green highlight shows whose turn it is

### Piece Rotation Modes
- **Fixed Mode** - Traditional view (black pieces always rotated)
- **Turn-based Mode** - All pieces rotate to face the current player's perspective

### Move Input
- **Click-to-Move** - Select piece, then destination
- **Drag-and-Drop** - Smooth piece dragging with visual feedback
- **Legal Move Highlighting** - Shows valid moves when piece is selected

### Game Management
- **Move History** - PGN notation with full game record
- **Navigation Controls** - Step through game history (first, prev, next, last)
- **Take Back** - Undo moves for teaching and learning
- **Flip Board** - Reverse board orientation
- **localStorage Persistence** - Games survive page refreshes

### Touch Gestures (Tablet)
- **Fullscreen Toggle** - Double two-finger tap or pinch-out gesture
- **Fullscreen Exit** - Double-click anywhere or click X button

### User Interface
- **Collapsible Sidebar** - All controls accessible but out of the way during play
- **Board Coordinates** - a-h files and 1-8 ranks labeled
- **Responsive Design** - vmin units scale to any screen size

## 🚀 Quick Start

### Play Online
Just visit **[1on1chess.com](https://1on1chess.com)**

### Run Locally
1. Clone the repository:
   ```bash
   git clone https://github.com/moshebeeri/1on1chess.git
   cd 1on1chess
   ```

2. Open `tabletop-chess.html` in your browser
   - No build process required
   - No server needed
   - Works offline

## 🛠️ Technologies

- **Pure HTML/CSS/JavaScript** - No frameworks, no dependencies (except chess.js)
- **[chess.js](https://github.com/jhlywa/chess.js)** (v0.10.3) - Chess move validation and game logic
- **localStorage API** - Game state persistence
- **CSS Grid & Flexbox** - Responsive layout
- **HTML5 Drag & Drop API** - Piece movement
- **Fullscreen API** - Immersive tablet experience

## 📱 Recommended Usage

1. **Device**: iPad or Android tablet (10"+ screen ideal)
2. **Orientation**: Place tablet flat on table between players
3. **Setup**:
   - Select time control
   - Choose rotation mode (turn-based recommended for new players)
   - Enter fullscreen for distraction-free play
4. **Play**: Each player sits on opposite sides of the table

## 🎯 Use Cases

- **Teaching Chess** - Use "Take Back" feature to correct mistakes
- **Casual Play** - Perfect for coffee shop games
- **Tournament Prep** - Practice with clock pressure
- **Travel** - Lightweight alternative to physical board

## 📂 Project Structure

```
.
├── tabletop-chess.html    # Complete application (single file)
├── CLAUDE.md              # AI assistant documentation
├── chat.md                # Development notes
└── README.md              # This file
```

## 🏗️ Architecture

Single-file application with inline CSS and JavaScript organized into classes:

- **StorageManager** - localStorage operations
- **GameState** - Chess logic, timer state, move validation
- **BoardRenderer** - Board rendering, piece selection, drag-and-drop
- **TimerDisplay** - Timer updates and active player indication
- **ChessGame** - Main controller, event wiring

## 🔧 Development

No build process needed. Edit `tabletop-chess.html` directly.

### Key Design Decisions

1. **Single File** - Easy deployment, works anywhere
2. **Dual Timers** - Both players can always see both clocks
3. **Turn-based Rotation** - Innovative feature for teaching/learning
4. **localStorage** - Simple persistence without backend

## 📄 License

MIT License - Feel free to use, modify, and distribute.

## 🤝 Contributing

Contributions welcome! This project was built with Claude Code as a learning exercise in creating accessible, tablet-optimized chess interfaces.

## 🙏 Credits

- Chess piece validation: [chess.js](https://github.com/jhlywa/chess.js)
- Built with [Claude Code](https://claude.com/claude-code)

---

**Play now at [1on1chess.com](https://1on1chess.com)** ♟️
