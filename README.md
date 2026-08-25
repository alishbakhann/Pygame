# Doodle Jump 🎮

A simple *Doodle Jump-style platform game* built with *Python and Pygame*. The player jumps automatically between randomly generated platforms while the screen scrolls upward. The goal is to keep climbing and achieve the highest score possible.

## Features

* 🟦 Randomly generated platforms
* 🟩 Automatic jumping when landing on platforms
* ⬅️➡️ Left and right player movement
* 🔄 Screen wrapping — the player can move off one side and appear on the other
* 📜 Vertical screen scrolling
* 🏆 Score system
* 💀 Game-over detection
* 🎲 Random platform positioning and spacing

## Requirements

Make sure you have:

* Python 3.x
* Pygame

Install Pygame using:

bash
pip install pygame


## How to Run

1. Clone the repository:

bash
git clone <your-repository-url>


2. Move into the project directory:

bash
cd <project-folder>


3. Run the game:

bash
python doodle_jump.py


If your system uses python3:

bash
python3 doodle_jump.py


## Controls

| Key            | Action     |
| -------------- | ---------- |
| ⬅️ Left Arrow  | Move left  |
| ➡️ Right Arrow | Move right |
| ❌ Close Window | Exit game  |

The player automatically jumps whenever they successfully land on a platform.

## How the Game Works

### Player Physics

Gravity continuously pulls the player downward:

python
player_y_vel += GRAVITY * dt
player_y += player_y_vel * dt


When the player lands on a platform while falling, their vertical velocity is reset to the jump power:

python
player_y_vel = JUMP_POWER


This creates the automatic bouncing effect.

### Platform Generation

Platforms are created with random vertical and horizontal gaps:

python
p_y = last_p.y - random.randint(MIN_GAP, MAX_GAP)


Their horizontal position is also randomized so that every game can have a different layout.

### Screen Scrolling

When the player reaches the upper portion of the screen, the platforms move downward instead of allowing the player to continue moving upward indefinitely.

Platforms that leave the bottom of the screen are recycled and placed above the highest platform.

### Scoring

Every time an old platform is recycled and a new platform is generated, the score increases by *10 points*.

## Game Over

The game ends when the player falls below the bottom of the screen.

The final score is then displayed:

text
GAME OVER
Final Score: 120


## Project Structure

text
Doodle-Jump/
│
├── doodle_jump.py
└── README.md


## Technologies Used

* *Python*
* *Pygame*
* *Random module*

## Future Improvements

Some features that could be added:

* 🎨 Better player and platform graphics
* 🔊 Jumping and game-over sound effects
* 🎵 Background music
* ❤️ Lives system
* 🏅 High-score tracking
* 📈 Increasing difficulty
* 🧍 Animated player character
* ⏸️ Pause and restart buttons
* 📱 Improved controls for different screen sizes

## Author

*Alishba Khan*








Built as a Python/Pygame game project.
