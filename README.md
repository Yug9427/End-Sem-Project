# 2048 Terminal Game 🎮🧩

[![C](https://img.shields.io/badge/Language-C-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![License](https://img.shields.io/badge/License-Public_Domain-red.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

A beautiful, colorful, terminal implementation of the classic 2048 puzzle game written in pure **C**, based on the legendary repository by [@mevdschee](https://github.com/mevdschee/2048.c).

![Gameplay Screenshot](https://github.com/mevdschee/2048.c/blob/main/debian_2048.png?raw=true)

## ✨ Features

- 🧠 Classic 2048 gameplay
- 🎨 Multiple color schemes:
  - Amber/Orange (Default)
  - Black & White (High Contrast)
  - Blue-Red Gradient
- 🎮 Multiple Control Schemes:
  - Arrow Keys
  - WASD
  - Vim-style HJKL
- 🧾 Real-time Score Tracking
- ☠️ Game Over Detection
- 🔁 Instant Restart with `R`
- 🧪 Built-in test/validation mode

## 🛠 Installation

### Requirements
- GCC Compiler
- Terminal with **256-color support** (recommended)

```bash
# Clone repository
git clone https://github.com/mevdschee/2048.c.git
cd 2048.c

# Compile with optimizations
gcc -O3 -o 2048 2048.c

# Install system-wide (optional)
sudo mv 2048 /usr/local/bin/
```

## 🚀 Usage

```bash
# Default mode
./2048
```
```bash
# Black & white theme
./2048 blackwhite
```
```bash
# Blue-red theme
./2048 bluered
```
```bash
# Run validation tests
./2048 test
```

## 📜 Game Rules

1. **Objective**
   - Combine number tiles to reach the **2048** tile.

2. **Merging Mechanics**
   - Matching tiles merge and double in value: `2 + 2 = 4`, `4 + 4 = 8`, etc.

3. **Scoring**
   - Points earned = new tile value on merge.

4. **New Tiles**
   - After every valid move, either `2` (90%) or `4` (10%) is added in a random empty cell.

5. **Game Over**
   - When there are **no empty spaces** and **no valid merges**.

## 🎨 Color Schemes

| Scheme      | Command             | Style                          |
|-------------|---------------------|---------------------------------|
| Default     | `./2048`            | Amber/orange tones              |
| Black/White | `./2048 blackwhite` | High contrast grayscale         |
| Blue/Red    | `./2048 bluered`    | Gradient from blue to red       |

## 🧠 Technical Deep Dive

### 🗂️ Board Representation

- Grid is a `4x4` matrix: `board[x][y]`
- Stores tile exponents:
  - Value `2` stored as `1` (2^1), `4` as `2` (2^2), etc.
  - Final display uses: `tile = (value > 0) ? (1 << value) : 0`

---

## 🔧 Function Breakdown (Brief Overview)

### `void drawBoard()`
Draws the game board using Unicode box-drawing characters and colors based on the current color scheme.

### `void addRandom()`
Adds a `2` (90%) or `4` (10%) tile at a random empty cell.

### `int countEmpty()`
Returns the number of empty tiles (`0`) on the board.

### `void rotateBoard()`
Rotates the board 90° clockwise to help unify move logic.

### `void rotateBoardBack()`
Restores board to original orientation after move operation.

### `int slideArray(int *array)`
Slides and merges a single row towards the left.

### `int moveLeft()`
Slides all rows to the left. Returns true if a tile moved or merged.

### `int moveRight()`
Rotates board 180°, slides left, then rotates back.

### `int moveUp()`
Rotates board 90° left, slides left, then rotates back.

### `int moveDown()`
Rotates board 90° right, slides left, then rotates back.

### `int gameEnded()`
Checks whether the game has ended (no moves or empty cells).

### `void restartGame()`
Resets board and score to start a new game.

### `void printColor()`
Initializes ANSI color escape sequences based on selected scheme.

### `void clearScreen()`
Clears terminal screen using ANSI codes.

### `void initGame()`
Initializes game state, adds two random tiles.

### `void drawTile(int x, int y, int value)`
Renders individual tile at (x, y) with color and value.

### `void drawScore()`
Prints the current score to the screen.

### `int testGame()`
Runs automated test to validate core logic and board consistency.

### `void readInput()`
Reads input keys (`WASD`, arrows, `HJKL`, etc.) and maps to movements.

### `int main(int argc, char *argv[])`
Main entry point. Parses CLI args, initializes game loop, handles themes and test mode.

---

## ⚙️ Directional Movement Strategy

All movement is reduced to **leftward movement** using board rotation:

| Direction | Pre-Rotation         | Post-Move Logic             | Rotation Reversal         |
|-----------|----------------------|-----------------------------|----------------------------|
| ← Left    | No rotation          | Slide each row left         | None                       |
| ↑ Up      | Rotate Left (90° CCW)| Slide each row left         | Rotate Right (90° CW)     |
| → Right   | Rotate 180°          | Slide each row left         | Rotate 180°                |
| ↓ Down    | Rotate Right (90° CW)| Slide each row left         | Rotate Left (90° CCW)     |

This keeps movement logic DRY (Don't Repeat Yourself) and efficient.

---

## 🪄 Future Enhancements & Ideas

- Add **undo/redo functionality**
- Save/load game state to file
- Support **terminal animations** (smooth tile transitions)
- High score tracking across sessions
- AI auto-play mode for experiments

---

## 📚 Acknowledgements

- Original implementation by [@mevdschee](https://github.com/mevdschee/2048.c)
- Inspired by [2048 by Gabriele Cirulli]
- This version extends the original with added color themes, multiple controls, and documentation.

---

Enjoy the retro-terminal feel while exercising your brain with **2048 in C**! 🧠💻
