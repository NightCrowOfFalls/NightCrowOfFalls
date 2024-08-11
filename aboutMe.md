Hello World 
------------
import pygame
import sys
import subprocess
import os

def install_dependencies():
    try:
        import pygame
    except ImportError:
        print("Pygame not found. Installing...")
        subprocess.check_call([sys.executable, "-m", "pip", "install", "pygame"])
    else:
        print("Pygame is already installed.")

install_dependencies()

pygame.init()

SCREEN_WIDTH, SCREEN_HEIGHT = pygame.display.Info().current_w, pygame.display.Info().current_h
BACKGROUND_COLOR = (0, 0, 0)  
TEXT_COLOR = (142, 123, 143)  
TEXT = "[NightCrow]"
FONT_SIZE = 100
TEXT_SPEED = 5

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT), pygame.FULLSCREEN)
pygame.display.set_caption("Bouncing Text")

font = pygame.font.Font(None, FONT_SIZE)

text_surface = font.render(TEXT, True, TEXT_COLOR)
text_rect = text_surface.get_rect()
text_rect.x = (SCREEN_WIDTH - text_rect.width) // 2
text_rect.y = (SCREEN_HEIGHT - text_rect.height) // 2

dx, dy = TEXT_SPEED, TEXT_SPEED

running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    text_rect.x += dx
    text_rect.y += dy

    if text_rect.left < 0 or text_rect.right > SCREEN_WIDTH:
        dx = -dx
    if text_rect.top < 0 or text_rect.bottom > SCREEN_HEIGHT:
        dy = -dy

    screen.fill(BACKGROUND_COLOR)

    screen.blit(text_surface, text_rect)

    pygame.display.flip()

    pygame.time.Clock().tick(60)

pygame.quit()
sys.exit()
