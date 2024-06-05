import pygame
import random


#COLOR
RED = (255, 0, 0)
BLUE = (0, 0, 255)
GREEN = (0, 255, 0)
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)


WIDTH = 750
HEIGHT = 550
FPS = 60

#SETUP
pygame.init()
pygame.mixer.init()
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Catch The Fruit")
clock = pygame.time.Clock()



running = True
while running:
    all_sprites.update()
    clock.tick(FPS)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
            
    all_sprites.update()
    screen.fill(BLACK)
    all_sprites.draw(screen)
    pygame.display.flip()
    
    clock.tick(60)
    
pygame.quit()
            
