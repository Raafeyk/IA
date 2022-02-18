# IA
import pygame
pygame.init()

win = pygame.display.set_mode((1600, 900))

pygame.display.set_caption("First Game")

walkRight = [pygame.image.load('R1.png'), pygame.image.load('R2.png'), pygame.image.load('R3.png'), pygame.image.load('R4.png'), pygame.image.load('R5.png'), pygame.image.load('R6.png'), pygame.image.load('R7.png'), pygame.image.load('R8.png'), pygame.image.load('R9.png')]
walkLeft = [pygame.image.load('L1.png'), pygame.image.load('L2.png'), pygame.image.load('L3.png'), pygame.image.load('L4.png'), pygame.image.load('L5.png'), pygame.image.load('L6.png'), pygame.image.load('L7.png'), pygame.image.load('L8.png'), pygame.image.load('L9.png')]
bg = pygame.image.load('background.png')
char = pygame.image.load('standing.png')
platform_img= pygame.image.load("platform.png")
clock = pygame.time.Clock()
class player(object):
    def __init__(self,x,y,width,height):
        self.grav=1
        self.x = x
        self.y = y
        self.width = width
        self.height = height
        self.vel = 5
        self.isJump = True
        self.left = False
        self.right = False
        self.walkCount = 0
        self.jumpCount = -5

    def draw(self, win):
        if self.walkCount + 1 >= 27:
            self.walkCount = 0

        if self.left:
            win.blit(walkLeft[self.walkCount//3], (self.x,self.y))
            self.walkCount += 1
        elif self.right:
            win.blit(walkRight[self.walkCount//3], (self.x,self.y))
            self.walkCount +=1
        else:
            win.blit(char, (self.x,self.y))
list_x= []
list_y= []
list_x.append(100)
list_y.append(200)
list_x.append(500)
list_y.append(300)
list_x.append(1000)
list_y.append(400)



def redrawGameWindow():
    win.blit(bg, (0,0))
    for i in range (0, 3):
        win.blit(platform_img, (list_x[i], list_y[i]))
        man.draw(win)
    
    pygame.display.update()



man = player(200, 450, 64,64)
run = True
while run:
    clock.tick(30)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False

    keys = pygame.key.get_pressed()

    if keys[pygame.K_LEFT] and man.x > man.vel:
        man.x -= man.vel
        man.left = True
        man.right = False
    elif keys[pygame.K_RIGHT] and man.x < 1600 - man.width - man.vel:
        man.x += man.vel
        man.right = True
        man.left = False
        if man.x== 950:
            man.isJump = True
            man.right = False
            man.left = False
            man.walkCount = 0
            man.y= 450
            
    else:
        man.right = False
        man.left = False
        man.walkCount = 0
        
    if not(man.isJump):
        if keys[pygame.K_SPACE]:
            man.isJump = True
            man.right = False
            man.left = False
            man.walkCount = 0
    else:
        if man.jumpCount >= -10:
            neg = 1
            if man.jumpCount < 0:
                neg = -1
            man.y -= (man.jumpCount ** 2) * 0.5 * neg
            man.jumpCount -= 1
        else:
            man.isJump = False
            man.jumpCount = 10
            
    redrawGameWindow()
tile_size=50
def draw_grid():
    for line in range(0,10):
        pygame.draw.line(screen, (255, 255, 255), (0, line* tile_size), (screen_width, line*tile_size))
        pygame.draw.line(screen, (255, 255, 255), (line * tile_size, 0), (line * tile_size, screen_height))

if self.player_hitbox.colliderect(self.platform):
    self.platform= pygame.Rect(x, y, w, w)
    self.player_hitbox= pygame.Rect(x, y, w, w)


for event in pygame.event.get():

    if event.type == pygame.QUIT:

         run = False


         pygame.display.update()



        
    
                    



pygame.quit()
