# Fruit
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


#MAIN PLAYER
class Player(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface((40, 60))
        self.image.fill(GREEN)
        self.rect = self.image.get_rect()
        self.rect.centerx = WIDTH / 2
        self.rect.bottom = HEIGHT - 10
        self.speedx = 0
        #self.radius(20)
        
        
    def update(self):
        self.speedx = 0
        keystate = pygame.key.get_pressed()
        if keystate[pygame.K_LEFT]:
            self.speedx = -15
        keystate = pygame.key.get_pressed()
        if keystate[pygame.K_RIGHT]:
            self.speedx = 15
        self.rect.x += self.speedx
        if self.rect.right > WIDTH:
            self.rect.right = WIDTH
        if self.rect.left < 0:
            self.rect.left = 0
            
            
        #def update(self):
            #self.rect.x += self.speedx
            #movement
            #for event in pygame.event.get():
                #if event.type == pygame.KEYDOWN:
                    #if event.key == pygame.K_LEFT:
                        #player.speedx = -8
                    #if event.key == pygame.K_RIGHT:
                        #player.speedx = 8

        
        
# SPRITES
all_sprites = pygame.sprite.Group()
player = Player()
fruits = pygame.sprite.Group()
all_sprites.add(player)
#for i in range (8):
    #fr = Fruit()
    #all_sprites.add(fr)
    #fruits.add(fr)
    

#RUNNING
running = True
while running:
    clock.tick(FPS)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

          
        #elif event.type == pygame.KEYDOWN
  
            
    all_sprites.update()
    screen.fill(BLACK)
    all_sprites.draw(screen)
    pygame.display.flip()
    
    clock.tick(60)
    
pygame.quit()
