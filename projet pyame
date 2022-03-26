import pygame, sys
import time
from pygame.locals import *
from random import randint
# randint(0,10) -> nb aléatoire entre 0 et 10

largeur = 600
hauteur = 600
taille = 20
temps_pour_avoir_une_new_balle  = 0

pygame.font.init()
pygame.display.init()
pygame.event.get()
pygame.mouse.get_pos()

def texte(text, couleur, coordonnée, taille):
        mytext = pygame.font.SysFont('arial', taille)
        mytext = mytext.render(text, False, couleur)
        fenetre.blit(mytext, coordonnée)
        
class Balle:
    def __init__(self):
        self.x = randint(0, largeur)
        self.y = randint(0, hauteur)        
        self.dx = randint(2,5)
        self.dy = randint(2,5)
        self.couleur = (randint(0,255), randint(0,255), randint(0,255))
        self.taille = taille

    def dessine(self):
        pygame.draw.circle(fenetre,self.couleur,(self.x,self.y),self.taille)    

    def bouge(self):
        self.x += self.dx
        self.y += self.dy
        
        if self.y < taille or self.y > hauteur - taille:
            self.dy = -self.dy
        
        if self.x < taille or self.x > largeur - taille:
            self.dx = -self.dx
        
        for balle in mes_balles:
            if ((self.x-balle.x)**2 + (self.y-balle.y)**2)**0.5 < self.taille + balle.taille:
                self.dx, balle.dx = balle.dx, self.dx
                self.dy, balle.dy = balle.dy, self.dy
    
    def collision(self):
        for balle in mes_balles:
            if ((balle_curseur.x-balle.x)**2 + (balle_curseur.y-balle.y)**2)**0.5 < balle_curseur.taille + balle.taille:
                mes_balles.remove(balle)
                

balle_curseur = Balle()
balle_curseur.taille = 7   

nbr_balles = int(input("nombre de balles max sur l'écran : "))


mes_balles = []
def apparition_new_balle(): 
    if temps_pour_avoir_une_new_balle % 47 == 0: 
        for k in range(1):
            new_balle = Balle()
            mes_balles.append(new_balle)
            

fenetre = pygame.display.set_mode((largeur, hauteur))
fenetre.fill([0,0,0])




pygame.display.flip()



while True:
    
    fenetre.fill([255,255,255])
    mx, my = pygame.mouse.get_pos()
    balle_curseur.x, balle_curseur.y = mx, my
    
    apparition_new_balle()
    
    for k in mes_balles:
        k.dessine()
        k.bouge()
    
    pygame.display.update()
        
    if len(mes_balles) == 0:
        
        while True :
            fenetre.fill([255,255,255])
            texte('YOU WIN !', [149,212,122], (200,100), 50)
            texte('(tape on "SPACE" to close the game)', [20,20,20], (100,500), 30)
            
            pygame.display.flip()
            
            for event in pygame.event.get():
                if event.type == KEYDOWN:
                    if event.key == K_SPACE:
                        sys.exit()

    
    
    if len(mes_balles) == nbr_balles:
        time.sleep(0.8)
        
        while True :
            fenetre.fill([255,255,255])
            texte('YOU LOSE, TRY AGAIN', [127,0,255], (80,80), 50)
            texte('(tape on "SPACE" to close the game)', [20,20,20], (100,500), 30)
           
            pygame.display.flip()
            
            for event in pygame.event.get():
                if event.type == KEYDOWN:
                    if event.key == K_SPACE:
                        sys.exit()
    
    pygame.display.flip()
        
    for event in pygame.event.get():
        if event.type == MOUSEBUTTONDOWN and event.button == 1 :
            for balle in mes_balles:
                balle.collision()
                
          
        if event.type == pygame.QUIT:
            pygame.display.quit()
            sys.exit()

    temps_pour_avoir_une_new_balle += 1
    time.sleep(0.02)
