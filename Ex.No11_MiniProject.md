# Ex.No: 11  Mini Project 
### DATE:                                                                            
### REGISTER NUMBER : 212221240006
### AIM: 
To write a Python program to simulate the game using pygame to develop a side-scrolling obstacle game inspired by Flappy Bird.
### Algorithm:
Step 1: Start by importing Pygame and initializing it to enable game functionalities like graphics, sound, and event handling.

Step 2: Define constants for the game screen dimensions, bird size, pipe dimensions, gravity, flap strength, and frames per second (FPS).

Step 3: Set up the game screen with specified width and height, assign a window caption, and define colors for various game elements.

Step 4: Load images for the bird and background, then scale them to fit the specified dimensions.

Step 5: Set the bird’s initial vertical position and velocity, create an empty list for pipes, set the score to zero, and initialize a game-over flag.

Step 6: Implement helper functions for game mechanics, including creating pipes with gaps, resetting the game, drawing the bird and pipes on the screen, and moving pipes.

Step 7: Move each pipe leftward, remove pipes that exit the screen, and spawn new pipes; increase the score each time the player passes a pipe.

Step 8: Detect collisions between the bird and the top/bottom screen boundaries, or between the bird and pipes; if a collision occurs, end the game.

Step 9: In the main game loop, detect if the player presses the spacebar and apply a flap (upward force) to the bird by setting its velocity to a negative value.

Step 10: Update the bird’s vertical position by applying gravity, redraw all game elements, display the score, and update the screen.

Step 11: Control the game loop with a fixed frame rate (FPS) to ensure consistent gameplay speed and responsiveness.

Step 12: When a collision is detected, display a "Game Over" message with the final score, wait a few seconds, and close the game window.

### Program:
```
import pygame
import random

# Initialize pygame
pygame.init()

# Game settings
WIDTH, HEIGHT = 400, 600
PIPE_WIDTH = 70
PIPE_GAP = 150
BIRD_WIDTH, BIRD_HEIGHT = 40, 30
GRAVITY = 1
FLAP_STRENGTH = -10
FPS = 30

# Colors
WHITE = (255, 255, 255)
GREEN = (0, 200, 0)

# Initialize screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Flappy Bird - Player Controlled Object")
clock = pygame.time.Clock()

# Load images
bird_img = pygame.image.load('bird.jpeg')  # Replace 'bird.png' with your bird image file
background_img = pygame.image.load('backd.jpg')  # Replace 'background.png' with your background image file

# Scale images to fit
bird_img = pygame.transform.scale(bird_img, (BIRD_WIDTH, BIRD_HEIGHT))
background_img = pygame.transform.scale(background_img, (WIDTH, HEIGHT))

# Initialize game variables
bird_y = HEIGHT // 2
bird_velocity = 0
pipes = []
score = 0
game_over = False

# Functions for game mechanics

def create_pipe():
    y = random.randint(100, HEIGHT - 100 - PIPE_GAP)
    return {'x': WIDTH, 'top': y - PIPE_GAP, 'bottom': y + PIPE_GAP}

def reset_game():
    global bird_y, bird_velocity, pipes, score, game_over
    bird_y = HEIGHT // 2
    bird_velocity = 0
    pipes = [create_pipe()]
    score = 0
    game_over = False

def draw_bird():
    screen.blit(bird_img, (50, bird_y))  # Draw the bird image at (50, bird_y)

def draw_pipes():
    for pipe in pipes:
        # Draw top pipe as a green rectangle
        pygame.draw.rect(screen, GREEN, (pipe['x'], 0, PIPE_WIDTH, pipe['top']))
        # Draw bottom pipe as a green rectangle
        pygame.draw.rect(screen, GREEN, (pipe['x'], pipe['bottom'], PIPE_WIDTH, HEIGHT - pipe['bottom']))

def move_pipes():
    for pipe in pipes:
        pipe['x'] -= 5
    if pipes[0]['x'] + PIPE_WIDTH < 0:
        pipes.pop(0)
        pipes.append(create_pipe())
        global score
        score += 1  # Player passes a pipe

def check_collision():
    # Check collision with top and bottom of the screen
    if bird_y <= 0 or bird_y + BIRD_HEIGHT >= HEIGHT:
        return True
    # Check collision with pipes
    for pipe in pipes:
        if 50 + BIRD_WIDTH > pipe['x'] and 50 < pipe['x'] + PIPE_WIDTH:
            if bird_y < pipe['top'] or bird_y + BIRD_HEIGHT > pipe['bottom']:
                return True
    return False

# Main game loop

reset_game()
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()
            
    # Player bird control (space bar to flap)
    keys = pygame.key.get_pressed()
    if keys[pygame.K_SPACE]:
        bird_velocity = FLAP_STRENGTH
        
    # Update bird position and apply gravity
    bird_velocity += GRAVITY
    bird_y += bird_velocity

    # Move pipes and check for collisions
    move_pipes()
    game_over = check_collision()
    
    if game_over:
        break

    # Draw everything on the screen
    screen.blit(background_img, (0, 0))  # Draw background image
    draw_bird()
    draw_pipes()

    # Display score
    font = pygame.font.Font(None, 36)
    score_text = font.render(f"Score: {score}", True, WHITE)
    screen.blit(score_text, (10, 10))
    
    pygame.display.flip()
    clock.tick(FPS)

# Display game over message
screen.fill((0, 0, 0))  # Clear screen
game_over_text = font.render("Game Over", True, WHITE)
score_text = font.render(f"Final Score: {score}", True, WHITE)
screen.blit(game_over_text, (WIDTH // 2 - game_over_text.get_width() // 2, HEIGHT // 2 - 20))
screen.blit(score_text, (WIDTH // 2 - score_text.get_width() // 2, HEIGHT // 2 + 20))
pygame.display.flip()
pygame.time.wait(3000)  # Display game over screen for 3 seconds
pygame.quit()
```
### Output:

![Screenshot 2024-11-14 123406](https://github.com/user-attachments/assets/28ea9d51-628d-423a-b2d3-f38af596ac26)
![Screenshot 2024-11-14 123453](https://github.com/user-attachments/assets/9635af09-2691-4b48-9336-1bcbc6612743)


### Result:
Thus, the simple game was implemented using Python and the Pygame library to simulate a player-controlled object navigating through obstacles.
