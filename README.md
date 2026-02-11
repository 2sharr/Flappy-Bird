# Flappy-Bird


### Files Description

#### **FlappyBird.java** (Main Game Class)
- **Package:** `flappyBird`
- **Size:** 5.2 KB
- **Lines:** 296

The core game class that handles:
- Game initialization and window setup (800x800 pixels)
- Bird physics and movement
- Obstacle (column) generation and collision detection
- Score tracking and game state management
- Event handling for user input

**Key Components:**
- `bird`: Rectangle object representing the player's bird (20x20 pixels)
- `columns`: ArrayList of obstacles the bird must avoid
- `gameOver`, `started`: State flags
- `score`: Player's current score
- `yMotion`: Vertical velocity of the bird

#### **Renderer.java** (Graphics Rendering)
- **Package:** `flappyBird`
- **Size:** 295 bytes
- **Lines:** 20

A lightweight JPanel extension that:
- Extends `javax.swing.JPanel` for custom rendering
- Calls the main FlappyBird's repaint method
- Handles the graphical display of the game

## Game Features

### Core Gameplay
- **Window Size:** 800x800 pixels
- **Bird Size:** 20x20 pixels
- **Obstacle Width:** 100 pixels
- **Obstacle Gap:** 300 pixels (variable heights)
- **Game Speed:** 10 pixels per frame movement

### Controls
- **Mouse Click:** Make the bird jump
- **Spacebar:** Make the bird jump (alternative control)

### Game Mechanics

1. **Starting the Game**
   - Game displays "Click to start!" message
   - Player must click the window or press spacebar to begin

2. **During Gameplay**
   - Bird falls due to gravity (yMotion increases by 2 every 2 ticks, max 15)
   - Bird jumps 10 units up when player provides input
   - Columns move from right to left at 10 pixels per frame
   - New columns are automatically generated as old ones exit the screen

3. **Scoring**
   - Score increases by 1 when the bird successfully passes through a column gap
   - Score detection is based on bird center alignment with column center

4. **Collision Detection**
   - Game ends if bird hits any column
   - Game ends if bird goes above the game area (y < 0)
   - Game ends if bird hits the ground (bottom 120 pixels reserved for ground)
   - Precise collision positioning adjusts bird location based on impact direction

5. **Game Over**
   - "Game Over!" message is displayed
   - Click or press spacebar to restart
   - Bird returns to center, columns reset, score resets to 0

### Visual Elements

- **Sky:** Cyan background
- **Ground:** Orange (120 pixels high at bottom)
- **Ground Line:** Green strip (20 pixels)
- **Bird:** Red square (20x20 pixels)
- **Obstacles:** Dark green columns
- **Text:** White Arial font
  - "Click to start!" (100pt) - displayed at start
  - "Game Over!" (100pt) - displayed on collision
  - Score (100pt) - displayed during gameplay at top center

## Physics & Gameplay Balance

### Gravity System
- Bird's y-motion increases by 2 pixels every 2 ticks (max velocity of 15 pixels)
- This creates a gravity-like effect with terminal velocity

### Obstacle Generation
- Columns are generated 300 pixels apart horizontally
- Each pair of columns (top and bottom) has a random gap
- Gap size varies between 50 and 350 pixels height
- 300-pixel vertical space gap between top and bottom obstacles

### Difficulty
- Constant obstacle approach speed maintains consistent challenge
- Random obstacle heights provide variety
- Bird's maximum falling speed prevents "free fall" feeling

## Technical Details

### Dependencies
- **Java Standard Library:**
  - `java.awt.*` - Graphics, colors, UI components, event handling
  - `java.util.ArrayList` - Dynamic obstacle storage
  - `javax.swing.*` - JFrame, JPanel, Timer framework

### Game Loop
- Uses `javax.swing.Timer` with 20ms interval (~50 FPS)
- `ActionPerformed` method handles physics updates and rendering
- Non-blocking event-driven architecture

### State Management
- `gameOver`: Boolean flag for game state
- `started`: Boolean flag to distinguish pre-start from active play
- `ticks`: Counter for timing-dependent operations
- Score persistence until game reset

## How to Run

### Compilation
```bash
javac flappyBird/*.java
