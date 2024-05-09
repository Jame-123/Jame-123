- 👋 Hi, I’m @Jame-123
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Jame-123/Jame-123 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import sys
import random

# Initialize pygame
pygame.init()

# Set up the screen
WIDTH, HEIGHT = 600, 400
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Pygame Racing Game")

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)

# Player properties
player_width = 50
player_height = 80
player_color = RED
player_x = WIDTH // 2 - player_width // 2
player_y = HEIGHT - player_height - 20
player_speed = 5

# Enemy properties
enemy_width = 50
enemy_height = 50
enemy_color = WHITE
enemy_speed = 7

# List to store enemies
enemies = []

# Add initial enemy
def add_enemy():
    enemy_x = random.randint(0, WIDTH - enemy_width)
    enemy_y = -enemy_height
    enemies.append([enemy_x, enemy_y])

# Function to move enemies
def move_enemies():
    for enemy in enemies:
        enemy[1] += enemy_speed

# Function to draw player
def draw_player():
    pygame.draw.rect(screen, player_color, (player_x, player_y, player_width, player_height))

# Function to draw enemies
def draw_enemies():
    for enemy in enemies:
        pygame.draw.rect(screen, enemy_color, (enemy[0], enemy[1], enemy_width, enemy_height))

# Function to check collisions
def check_collision():
    for enemy in enemies:
        if (player_x < enemy[0] + enemy_width and
            player_x + player_width > enemy[0] and
            player_y < enemy[1] + enemy_height and
            player_y + player_height > enemy[1]):
            return True
    return False

# Main game loop
running = True
clock = pygame.time.Clock()
score = 0

while running:
    screen.fill(BLACK)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_x -= player_speed
    if keys[pygame.K_RIGHT]:
        player_x += player_speed

    # Move and draw enemies
    move_enemies()
    draw_enemies()

    # Check collisions
    if check_collision():
        print("Game Over!")
        running = False

    # Draw player
    draw_player()

    # Add new enemy randomly
    if random.randint(0, 100) < 3:
        add_enemy()

    # Increase score for each frame
    score += 1

    # Update display
    pygame.display.update()
    clock.tick(60)

# Quit pygame
pygame.quit()
sys.exit()
