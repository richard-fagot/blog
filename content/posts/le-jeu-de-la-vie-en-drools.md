---
title: "Drools, Le jeu de la vie"
date: 2015-09-17
tags: 
- drools
- jboss
- BRMS
- "Moteur de règles métiers"
- "Le jeu de la vie"
- "Conway's Game Of Life"
---
![img](/img/drools-jeu-de-la-vie/feature-drools-game-of-life.gif)

Un collègue m'a montré son implémentation du *jeu de la vie* suite à son autoformation en *Haskell*.  
  
Simple et élégante, comme on peut s'y attendre en *Haskell*, cela m'a donné l'idée de le faire en *Drools*. 

## TL,DR

1. [Téléchargez l'exemple](https://github.com/richard-fagot/drools-6.2.0-ConwaysGameOfLife) ;
2. Suivez les instructions indiquées dans le *README.md*.

## Le contexte
Lorsqu'on suit les tutoriaux pour apprendre à faire du *Drools* (ou du *JRules* aussi d'ailleurs), il y a un exemple qui est systématiquement présenté pour illustrer ce qu'on peut faire avec un *BRMS* : la suite de Fibonacci.   
    
Bien que permettant d'illustrer la récursivité, j'ai toujours trouvé cet exemple peu ludique et peu motivant.  
    
Au contraire, le *jeu de la vie* est un exemple ludique et motivant car le résultat de l'exécution du moteur de règle peut se voir sous la forme d'une animation bien sympathique.

## Le jeu de la vie
Le jeu de la vie est un automate cellulaire inventé en 1970 par *John H. Conway*. Ce dernier essaya de simplifier un machine qui pourrait s'auto-reproduire, inventée par *John Von Neumann*. Il y parvint avec un certain succès vu que le jeu de la vie est probablement l'automate cellulaire le plus connu au monde !  
    
Son travail déboucha sur deux règles simples :

* une cellule morte qui possède exactement 3 voisines devient vivante ;
* une cellule vivante qui possède moins de 2 ou plus de 3 voisines meurt.

Pour plus d'information, je vous invite à consulter [l'article wikipedia](https://fr.wikipedia.org/wiki/Jeu_de_la_vie).


## L'implémentation
Le jeu de la vie se résume en deux règles.  
    
Ça tombe bien, *Drools* est un moteur de règles et il ne nous faudra pas plus que ces deux règles exactement pour implémenter notre solution.  
    
Tout repose sur les cellules :

{{< highlight java >}} 
public final class Cell {
    public static final boolean DEAD = false;
    public static final boolean ALIVE = true;
    
    private final int posX;
    private final int posY;
    
    private boolean state;

    ...
}
{{< / highlight>}}

Ces dernières ont une position dans le plan et un état *vivant* ou *mort*.  
    
On en crée tout un lot remplissant un espace 2D, certaines vivantes, d'autre mortes, aléatoirement. Et on pousse tout ça dans la *Working Memory*.  
    
L'implémentation des deux règles du jeu de la vie se fait de façon relativement directe. On prend une cellule et on compte le nombre de cellules vivantes autour d'elle. Ce décomptage nécessite une petite subtilité de *Drools* par l'utilisation d'un accumulateur.  
    
**Règle qui ramène à la vie une cellule morte s'il y a exactement 3 cellules vivantes prononçant des incantations du livre des morts autour d'elle :**

{{< highlight java >}} 
when
  currentCell : Cell(state == Cell.DEAD)
  nbNeighbours : Number( this == 3) from accumulate (
    $cell : Cell((state == Cell.ALIVE)
    && (
      ((posX == (currentCell.posX - 1)) 
        && (posY == (currentCell.posY + 1)))
      || ((posX == currentCell.posX)
        && (posY == (currentCell.posY + 1)))
      || ((posX == (currentCell.posX + 1))
        && (posY == (currentCell.posY + 1)))
                   
      || ((posX == (currentCell.posX - 1))
        && (posY == currentCell.posY))
      || ((posX == (currentCell.posX + 1))
        && (posY == currentCell.posY))
                   
      || ((posX == (currentCell.posX - 1))
        && (posY == (currentCell.posY - 1)))
      || ((posX == currentCell.posX )
        && (posY == (currentCell.posY - 1)))
      || ((posX == (currentCell.posX + 1))
        && (posY == (currentCell.posY - 1)))
                   
    ))
        
    , count($cell))
        
    then
        currentCell.state = Cell.ALIVE; 
{{< / highlight >}}

Habituellement, on trouve autant d'instance de règles que de combinaisons d'objets qui exécutent cette règle. L'accumulateur permet d'avoir une seule instance de règle pour l'ensemble des objets qui correspondent aux critères indiqués.  
  
Ici, on récupère toutes les cellules vivantes qui entourent la cellule courante et on applique la fonction `count()` (il en existe d'autre, comme `sum()` par exemple).  
    
Pour une règle plus lisible, il aurait été préférable d'appeler une méthode que se charge de retourner l'ensemble des voisins vivants autour d'une cellule donnée mais, ici, je souhaitais illustrer l'accumulateur et rester dans l'idée d'implémenter le jeu de la vie entièrement en *Drools*.  
    
**Règle qui tue une cellule vivante s'il y a trop ou trop peu de cellules vivantes autour d'elle pour lui donner des croquettes au saumon :**  
    
{{< highlight java >}} 
when
  currentCell : Cell(state == Cell.ALIVE)
  nbNeighbours : 
    Number( this < 2 || this > 3) from accumulate (
    $cell : Cell((state == Cell.ALIVE)
      && (
      ((posX == (currentCell.posX - 1)) 
        && (posY == (currentCell.posY + 1)))
      || ((posX == currentCell.posX)
        && (posY == (currentCell.posY + 1)))
      || ((posX == (currentCell.posX + 1)) 
        && (posY == (currentCell.posY + 1)))
                   
      || ((posX == (currentCell.posX - 1)) 
        && (posY == currentCell.posY))
      || ((posX == (currentCell.posX + 1)) 
        && (posY == currentCell.posY))
                   
      || ((posX == (currentCell.posX - 1)) 
        && (posY == (currentCell.posY - 1)))
      || ((posX == currentCell.posX )
        && (posY == (currentCell.posY - 1)))
      || ((posX == (currentCell.posX + 1))
        && (posY == (currentCell.posY - 1)))
                   
        ))
        
        , count($cell))
        
    then
        currentCell.state = Cell.DEAD;  
{{< / highlight >}}

## L'exécution

{{< figure src="/img/drools-jeu-de-la-vie/LeJeuDeLaVie.gif#center" alt="Le jeu de la vie" class="center">}}
  
Pour rendre la chose plus ludique et attrayante j'ai ajouté une visualisation graphique des différents calculs portés par *Drools*.  
    
Exécutez la classe `Main.java` comme projet java et émerveillez-vous devant le miracle des multiples résurrections !  
    
Le projet d'exemple se trouve sur <https://github.com/richard-fagot/drools-6.2.0-ConwaysGameOfLife>
