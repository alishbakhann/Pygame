Doodle Jump — Pygame

A simple Doodle Jump-style game made with Python and Pygame. The player moves left and right, automatically jumps on platforms, and earns points while climbing.

Requirements
Python 3.x
Pygame

Install Pygame:

pip install pygame


Run the game:

python doodle_jump.py

Controls
← Move left
→ Move right
Close the window to quit
Features
Automatic jumping and gravity
Randomly generated platforms
Screen scrolling
Horizontal screen wrapping
Score system
Game-over detection
How It Works

The player jumps automatically whenever they land on a platform. As the player reaches the top of the screen, the platforms scroll downward.

Platforms that leave the screen are recycled and placed above the highest platform. Each recycled platform increases the score by 10 points.

The game ends when the player falls below the bottom of the screen.

Project Structure
doodle-jump/
└── doodle_jump.py

Possible Improvements
Add images and animations
Add sound effects
Add a restart button
Add high-score saving
Add moving platforms
Add increasing difficulty
License

Free to modify and use for personal or educational projects.
