



import pygame
import random
pygame.init()

screen = pygame.display.set_mode((700,500))
pygame.display.set_caption("pong")

doExit = False

p1x = 300
p1y = 425
bx = 350
by= 250
bVx = 3
bVy = 3
ball_size = 3

clock = pygame.time.Clock()


class brick:
    def __init__(self, xpos, ypos):
        self.xpos = xpos
        self.ypos = ypos
        self.color = (random.randrange(100, 250),random.randrange(100, 250),random.randrange(100, 250))
        self.isDead = False
    def draw(self):
        if not self.isDead:
            pygame.draw.rect(screen, self.color, (self.xpos, self.ypos, 100,50))
    #bounding box collision
    def collide(self, ball_x, ball_y):
        if not self.isDead:
            if (ball_x + ball_size > self.xpos and
                ball_x < self.xpos + 100 and
                ball_y + ball_size > self.ypos and
                ball_y < self.ypos + 50):
                self.isDead = True
                return True
        return False
       

 
b1 = brick(50, 50)
b2 = brick(175, 50)
b3 = brick(300, 50)
b4 = brick(425, 50)
b5 = brick(550, 50)
b6 = brick(50, 125)
b7 = brick(175, 125)
b8 = brick(300, 125)
b9 = brick(425, 125)
b10 = brick(550, 125)
while not doExit:# game loop----------------------
   
    #event queue stuff---------------
    clock.tick(60)
   
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            doExit = True
           
    #game logic will go here------------------
    keys = pygame.key.get_pressed()
    if keys[pygame.K_a]:
        p1x-=5
    if keys[pygame.K_d]:
        p1x+=5
       
    bx += bVx
    by += bVy
   

    if bx > p1x + 20 and by + 10 > p1y and by < p1y:
        bVy *= -1
       
       
    if b1.collide(bx, by):
        bVy *=-1
    if b2.collide(bx, by):
        bVy *=-1            
    if b3.collide(bx, by):
        bVy *=-1    
    if b4.collide(bx, by):
        bVy *=-1        
    if b5.collide(bx, by):
        bVy *=-1
    if b6.collide(bx, by):
        bVy *=-1
    if b7.collide(bx, by):
        bVy *=-1            
    if b8.collide(bx, by):
        bVy *=-1            
    if b9.collide(bx, by):
        bVy *=-1            
    if b10.collide(bx, by):
        bVy *=-1      
       
       
   
    if bx < 0 or bx + 20 > 700:
        bVx *= -1
    if by > 500 - 20 or by < 0:
        bVy *= -1
       
   
           
           
    #render section will go here-----------------------
    screen.fill((0,0,0))
   
    pygame.draw.rect(screen, (255, 255, 255), (p1x, p1y, 100,20),1)
   
    pygame.draw.circle(screen, (255, 255, 255), (bx, by), 10)
   
    b1.draw()
    b2.draw()
    b3.draw()
    b4.draw()
    b5.draw()    
    b6.draw()    
    b7.draw()
    b8.draw()
    b9.draw()
    b10.draw()    
   
    pygame.display.flip()
           
           
#end game loop    
           
pygame.quit()
