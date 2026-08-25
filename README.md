import pygame
import random

pygame.init()

# Constants
WIDTH = 400
HEIGHT = 600
FPS = 60
GRAVITY = 0.5 * 60 * 60
JUMP_POWER = -10 * 60
SCROLL_THRESH = HEIGHT // 3

# Y-Axis Gaps
MAX_GAP = 85
MIN_GAP = 40

# X-Axis Gaps
MAX_X_GAP = 100
MIN_X_GAP = 30

# Colors
WHITE = (255, 255, 255)
GREEN = (50, 200, 50)
BLUE = (50, 150, 255)
BLACK = (0, 0, 0)

screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Doodle Jump")
clock = pygame.time.Clock()
font = pygame.font.SysFont("Arial", 24)


def draw_text(text, font, color, surface, x, y):
    textobj = font.render(text, True, color)
    textrect = textobj.get_rect()
    textrect.center = (x, y)
    surface.blit(textobj, textrect)


def find_min(platforms):
    highest_platform = platforms[0]
    for p in platforms:
        if p.y < highest_platform.y:
            highest_platform = p

    return highest_platform


player_w = 30
player_h = 30
player_x = WIDTH // 2
player_y = HEIGHT - 150
player_y_vel = 0
player_speed = 5 * 60

platforms = []

p_w = 60  # platform width
p_h = 15  # platform height
platforms.append(
    pygame.Rect(WIDTH // 2 - 30, HEIGHT - 50, p_w, p_h)
)  # initial platform

for i in range(9):
    last_p = platforms[-1]

    p_y = last_p.y - random.randint(MIN_GAP, MAX_GAP)

    x_offset = random.randint(MIN_X_GAP, MAX_X_GAP)
    direction = random.choice([-1, 1])  # Randomly choose left or right
    p_x = last_p.x + (x_offset * direction)

    p_x = p_x % (WIDTH - p_w)

    platforms.append(pygame.Rect(p_x, p_y, p_w, p_h))

score = 0
game_over = False

running = True
while running:
    dt = clock.tick(FPS) / 1000.0
    screen.fill(WHITE)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    if not game_over:
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            player_x -= player_speed * dt
        if keys[pygame.K_RIGHT]:
            player_x += player_speed * dt

        # Screen wrapping thing
        if player_x > WIDTH:
            player_x = -player_w
        elif player_x < -player_w:
            player_x = WIDTH

        # Apply Gravity
        player_y_vel += GRAVITY * dt
        player_y += player_y_vel * dt

        player_rect = pygame.Rect(player_x, player_y, player_w, player_h)

        # Check Collisions with Platforms
        for p in platforms:
            if p.colliderect(player_rect) and player_y_vel > 0:
                if player_rect.bottom <= p.centery + 10:
                    player_y_vel = JUMP_POWER

        if player_y < SCROLL_THRESH:
            player_y += abs(player_y_vel) * dt
            for p in platforms:
                p.y += abs(player_y_vel) * dt  # scroll platform by y-vel of player

                if p.y > HEIGHT:  # meaning platform is out of screen
                    # Find the highest platform, so lowest Y value, to recycle the off-screen platform
                    highest_p = find_min(platforms)

                    # Apply Y gap
                    p.y = highest_p.y - random.randint(MIN_GAP, MAX_GAP)

                    # Apply X gap
                    x_offset = random.randint(MIN_X_GAP, MAX_X_GAP)
                    direction = random.choice([-1, 1])
                    new_x = highest_p.x + (x_offset * direction)

                    p.x = new_x % (WIDTH - p_w)
                    score += 10

        if player_y > HEIGHT:
            game_over = True

        pygame.draw.rect(screen, GREEN, player_rect)
        for p in platforms:
            pygame.draw.rect(screen, BLUE, p)

        draw_text(f"Score: {score}", font, BLACK, screen, 60, 30)

    else:
        draw_text("GAME OVER", font, BLACK, screen, WIDTH // 2, HEIGHT // 2 - 40)
        draw_text(f"Final Score: {score}", font, BLACK, screen, WIDTH // 2, HEIGHT // 2)

    pygame.display.flip()

pygame.quit()
