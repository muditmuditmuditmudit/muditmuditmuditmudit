Certainly! Here's a complete Flappy Bird game script written in Python using the Pygame library. This version is concise and beginner-friendly, making it ideal for learning purposes.


---

🐍 Flappy Bird in Python (Pygame)

📄 flappy.py

import pygame
import random
import sys

# Initialize Pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 400, 600
SCREEN = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Flappy Bird")

# Colors
WHITE = (255, 255, 255)
BLUE = (0, 0, 255)
GREEN = (0, 255, 0)

# Game variables
gravity = 0.5
bird_movement = 0
game_active = True
score = 0
high_score = 0
font = pygame.font.SysFont('Arial', 40)

# Bird
bird = pygame.Rect(100, HEIGHT // 2, 30, 30)

# Pipes
pipe_width = 70
pipe_height = random.randint(150, 450)
pipe_gap = 200
pipe_x = WIDTH
pipe_color = GREEN

# Clock
clock = pygame.time.Clock()



🕹️ Game Loop

def draw_pipes(pipe_x, pipe_height):
    bottom_pipe = pygame.Rect(pipe_x, pipe_height + pipe_gap, pipe_width, HEIGHT)
    top_pipe = pygame.Rect(pipe_x, 0, pipe_width, pipe_height)
    pygame.draw.rect(SCREEN, pipe_color, bottom_pipe)
    pygame.draw.rect(SCREEN, pipe_color, top_pipe)
    return bottom_pipe, top_pipe

def check_collision(bird, pipes):
    for pipe in pipes:
        if bird.colliderect(pipe):
            return False
    if bird.top <= -100 or bird.bottom >= HEIGHT:
        return False
    return True

def display_score(score, high_score):
    score_surface = font.render(f'Score: {score}', True, WHITE)
    high_score_surface = font.render(f'High Score: {high_score}', True, WHITE)
    SCREEN.blit(score_surface, (10, 10))
    SCREEN.blit(high_score_surface, (10, 50))

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE and game_active:
                bird_movement = 0
                bird_movement -= 10
            if event.key == pygame.K_SPACE and not game_active:
                game_active = True
                pipe_x = WIDTH
                bird.center = (100, HEIGHT // 2)
                bird_movement = 0
                score = 0

    SCREEN.fill(BLUE)

    if game_active:
        # Bird
        bird_movement += gravity
        bird.y += bird_movement
        pygame.draw.rect(SCREEN, WHITE, bird)

        # Pipes
        pipe_x -= 5
        if pipe_x < -pipe_width:
            pipe_x = WIDTH
            pipe_height = random.randint(150, 450)
            score += 1
            if score > high_score:
                high_score = score

        pipes = draw_pipes(pipe_x, pipe_height)

        # Collision
        game_active = check_collision(bird, pipes)

        # Score
        display_score(score, high_score)
    else:
        game_over_surface = font.render('Game Over', True, WHITE)
        SCREEN.blit(game_over_surface, (WIDTH // 2 - game_over_surface.get_width() // 2, HEIGHT // 2))

    pygame.display.update()
    clock.tick(60)




---

🚀 How to Run

1. Install Pygame:  

pip install pygame





2. Save the Script:  


3. Run the Game:  

python flappy.py





4. Play:  




---

📚 Additional Resources

LeonMarqs' Flappy Bird:   

FlapPyBird by sourabhv:   


Feel free to explore these repositories for more features, graphics, and enhancements.

Let me know if you need further assistance or modifications!

