```markdown
# Space Game with Processing

This project is a space-themed game built using the Processing framework. Players can control an astronaut to avoid meteors and collect coins. The game features a main menu, configuration settings, and a high score system.

## Table of Contents
- [Features](#features)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Code Overview](#code-overview)
- [Classes Overview](#classes-overview)
- [License](#license)

## Features
- Main menu with options to start the game and configure settings
- Character selection and background customization
- Real-time score tracking and high score display
- Pause and resume functionality
- Music control (mute/unmute)
- Collision detection with meteors and coins
- Increasing difficulty levels

## Hardware Requirements
- Computer with a modern operating system
- Keyboard for controlling the game

## Software Requirements
- [Processing](https://processing.org/download/) (version 3.5.4 or later)
- Java Development Kit (JDK) if not bundled with Processing

## Installation
1. **Download and Install Processing:**
   - Download Processing from the [official website](https://processing.org/download/) and follow the installation instructions for your operating system.

2. **Clone the Repository:**
   ```sh
   git clone <repository-url>
   cd <repository-directory>
   ```

3. **Open the Project in Processing:**
   - Launch the Processing IDE.
   - Open the main `.pde` file from the cloned repository.

4. **Run the Sketch:**
   - Click the "Run" button in the Processing IDE to start the game.

## Usage
1. **Main Menu:**
   - Use the UP and DOWN arrow keys to navigate the menu options.
   - Press ENTER to select an option.
   - Press 'M' to mute or unmute the background music.

2. **Game Controls:**
   - Use the LEFT and RIGHT arrow keys to move the astronaut.
   - Press SPACE to pause or resume the game.
   
3. **Configuration:**
   - In the configuration menu, use the arrow keys to select characters and backgrounds.
   - Adjust the volume using the LEFT and RIGHT arrow keys.
   - Press ENTER to confirm your selections.

4. **Gameplay:**
   - Avoid meteors falling from the top of the screen.
   - Collect coins to increase your score.
   - The game difficulty increases with higher scores.

## Code Overview
The game is structured into several key sections:

- **Setup and Draw:**
  - `setup()`: Initializes the game, loads images and sounds, and sets up initial configurations.
  - `draw()`: The main game loop that updates the game state and renders graphics.

- **Key Presses:**
  - `keyPressed()`: Handles keyboard input for navigating menus and controlling the game.
  - `keyReleased()`: Resets movement flags when keys are released.

- **Collision Detection:**
  - `colisionChecker()`: Checks for collisions between the astronaut and meteors.
  - `coin_collet()`: Checks for collisions between the astronaut and coins.

- **Game Functions:**
  - `generate_meteor()`, `add_more_meteor_1()`, `add_more_meteor_2()`, `add_coin()`: Functions for generating and managing meteors and coins.
  - `reset()`: Resets the game state after a collision.

## Classes Overview

### ASTRO
Manages the astronaut character, including movement and rendering.

### METEOR
Represents meteors that the astronaut must avoid. Includes movement and collision detection.

### COIN
Represents coins that the astronaut can collect to increase the score.

### PLAYER
Holds player data, including the name and score. Used for high score tracking.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
