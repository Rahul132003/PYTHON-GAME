# PYTHON-GAME
FLAPPY BIRD GAME USING PYTHON  

This is a simple, self-contained clone of the popular mobile game Flappy Bird, built using Python and the Pygame library. The game simulates the core endless runner mechanics where a bird must navigate through gaps in scrolling pipes by flapping its wings to avoid obstacles. It's designed for beginners to understand game development concepts like event handling, collision detection, physics simulation (gravity), and rendering. The game runs in a window and uses basic shapes (rectangles) for graphics—no external assets like images or sounds are required, making it lightweight and easy to modify.

Key Components and How They Work
Initialization and Setup:

Pygame Initialization: The code starts by importing necessary modules (pygame, random, sys) and initializing Pygame. Constants are defined for dimensions (e.g., SCREEN_WIDTH = 400, SCREEN_HEIGHT = 600), physics (e.g., GRAVITY = 0.5, FLAP_STRENGTH = -8), and visuals (e.g., colors like BLUE for the bird).
Display and Clock: A window is created with pygame.display.set_mode(), captioned "Flappy Bird Clone". A clock ensures consistent FPS, and fonts are loaded for text rendering.
Colors and Rectangles: Pygame uses Rect objects for positioning and collision checks. Everything is drawn with pygame.draw.rect() for simplicity.
Bird Class:

Represents the player-controlled bird.
Attributes: Position (x, y), velocity (starts at 0), and a Rect for its bounding box (30x30 pixels, fixed at x=50 for left-side positioning).
Methods:
flap(): Instantly sets velocity to a negative value (-8) to simulate an upward jump.
update(): Applies gravity by increasing velocity downward each frame, then updates the y-position. The Rect is refreshed for collision purposes.
draw(): Renders the bird as a blue rectangle on the screen.
Physics: Mimics real gravity—velocity accumulates over time, making the bird fall faster if not flapping.
Pipe Class:

Represents the obstacles (pairs of top and bottom pipes with a gap).
Attributes:
x position (starts off-screen to the right).
Random height for the top pipe (between 100 and ~350 pixels to ensure a navigable gap of 150 pixels).
Two Rect objects: one for the top pipe (from top of screen to height) and one for the bottom (from height + GAP to bottom of screen).
passed flag: Tracks if the bird has flown past this pipe for scoring.
Methods:
update(): Moves the pipe left by PIPE_SPEED (3 pixels per frame). Updates both rects' positions.
draw(): Renders both pipe rects as green rectangles.
off_screen(): Checks if the pipe has fully scrolled off the left side (x + width < 0) for removal to save memory.
Generation: Pipes are added dynamically when the last one is ~200 pixels from the right edge, ensuring steady spacing.
Main Game Loop (main() function):

Event Handling: Processes user input via pygame.event.get():
Quit on window close.
Spacebar: Calls bird.flap() if not game over.
R key: Restarts the game (resets bird, pipes, score, and game_over flag).
Update Logic (only if not game over):
Updates the bird's position.
Spawns new pipes as needed.
Iterates through pipes: Updates positions, removes off-screen ones, increments score if bird passes (pipe.x + width < bird.x and not passed), and checks collisions.
Collision Detection: Uses rect.colliderect() for bird vs. top/bottom pipes. Also checks if bird.y < 0 (ceiling) or bird.y + height > screen height (ground).
Rendering:
Fills screen with white.
Draws bird and all pipes.
Overlays score text at top-left.
If game over: Displays "Game Over!", final score, and restart instructions centered on screen.
Loop Control: Runs until quit, flipping the display and ticking the clock for 60 FPS.
Helper Function (draw_text):

Renders text using Pygame's font system and blits it to the screen at specified coordinates. Used for score, game over messages, etc.
Entry Point:

The if __name__ == "__main__": block calls main() when the script is run directly.
