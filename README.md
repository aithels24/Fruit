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


# --------------------------------------------------------------------------------------------------------    

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
        
        
    def update(self):
        self.speedx = 0
        keystate = pygame.key.get_pressed()
        if keystate[pygame.K_LEFT]:
            self.speedx = -10
        keystate = pygame.key.get_pressed()
        if keystate[pygame.K_RIGHT]:
            self.speedx = 10
        self.rect.x += self.speedx
        if self.rect.right > WIDTH:
            self.rect.right = WIDTH
        if self.rect.left < 0:
            self.rect.left = 0
            
# --------------------------------------------------------------------------------------------------------       


class Fruits(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((30, 30))
        self.image.fill(RED)
        self.rect = self.image.get_rect() 
        self.rect.x = random.randint(0, WIDTH - self.rect.width)
        self.rect.y = random.randint(-100, -40)
        self.speed = 3
        
        
    def update(self):
        self.rect.y += self.speed
        if self.rect.top > HEIGHT:
            self.rect.x = random.randint(0, WIDTH - self.rect.width)
            self.y = random.randint(-100, -40)
            self.speed = random.randint(1, 5)
            self.reset()
            
        def update(self):
            self.rect.y += self.speedy
            self.rect.x += self.speedx
            if self.rect.top > HEIGHT + 10 or self.rect.left < -25 or self.rect.right > WIDTH + 20:
                
                self.rect.x = random.randrange(WIDTH - self.rect.width)
                self.rect.y = random.randrange (-100, -40)
                self.speedy = random.randrange(1, 8 )
        
    def reset(self):
        self.rect.x = random.randint (0, WIDTH - self.rect.width)
        self.rect.y = random.randint(-100, -40)
        self.speed = 3
        
# --------------------------------------------------------------------------------------------------------      


class Bomb(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((30, 30))
        self.image.fill(BLUE)
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, WIDTH - self.rect.width)
        self.rect.y = random.randint(-100, -40)
        self.speed = 3
        
        
    def update(self):
        self.rect.y += self.speed
        if self.rect.top > HEIGHT:
            self.rect.x = random.randint(0, WIDTH - self.rect.width)
            self.y = random.randint(-100, -40)
            self.speed = random.randint(1, 5)
            self.reset()


    def reset(self):
        self.rect.x = random.randint (0, WIDTH - self.rect.width)
        self.rect.y = random.randint(-100, -40)
        self.speed = 3
        
        
#------------------------------------------------------------------------------------------------------------
        
        
all_sprites = pygame.sprite.Group()
fruits_fall = pygame.sprite.Group()
bomb_fall = pygame.sprite.Group()
player = Player()
all_sprites.add(player)

for i in range(10):
    fruit = Fruits()
    all_sprites.add(fruit)
    fruits_fall.add(fruit)
for i in range(2):
    bomb = Bomb()
    all_sprites.add(bomb)
    bomb_fall.add(bomb)
    
running = True
while running:
    all_sprites.update()
    clock.tick(FPS)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        
        
    all_sprites.update()

    for bomb in bomb_fall:
        if pygame.sprite.collide_rect(player, bomb ): 
            bomb.reset()
    
    for fruit in fruits_fall:
        if pygame.sprite.collide_rect(player, fruit ): 
            fruit.reset()

            
    all_sprites.update()
    screen.fill(BLACK)
    all_sprites.draw(screen)
    pygame.display.flip()
    
    clock.tick(60)
    
pygame.quit()
            
