---
title: "Drools, Tables de décision et Ruleflow"
date: 2015-08-30
tags: 
  - drools
  - jboss
  - ruleflow
  - "Table de décision"
  - BRMS
  - "Moteur de règles métiers"
  - Excel
description: "Comment faire marcher les tables de décision de Drools avec un ruleflow"
---
 ![img](/img/drools-dt-jbpmn/feature-drools-cercueil.png)
Vous voulez faire marcher une table de décision dans un ruleflow ? Vous vous y êtes essayé et maintenant vous dormez dans un cercueil ? Retrouvez votre âme perdue en lisant cet article !


## TL;DR
1. [Téléchargez l'exemple](https://github.com/richard-fagot/drools-6.2.0-dt-jbpmn) ;
2. Suivez les instructions indiquées dans le *README.md*.

## Ce qu'il faut savoir avant de commencer
*Drools* évolue beaucoup entre deux versions et il ne faut pas compter sur la retrocompatibilité. Ce qui marche dans une version peut ne plus fonctioner dans la version suivante et je ne parle même pas des versions SNAPSHOT.  

Dans ce tutoriel, il faudra utiliser la version *Drools 6.2.0.Final*.

## Le problème
Pour le développement d'un prototype, le client souhaitait un module avec des règles métier, si possible pas cher. Ça tombe bien, *Drools* est un BRMS open source et gratuit.  

Pour montrer qu'il est possible de personnaliser certaines règles facilement, nous avons ajouté une table de décision, simple, mais pour le prototype c'était suffisant et serait du plus bel effet.  

*Drools* propose deux façons de faire des tables de décisions avec des fichiers *Excel*. Dans les deux cas, chaque ligne du fichier donnera une règle basée sur un template à définir.  

La première, pas très sexy, consiste à faire précéder les lignes de données par le template de la règle à exécuter. Cela fait apparaître dans le fichier *Excel* des informations de nature technique, modifiable par quiconque édite le fichier, avec les séances de débogage obscures que cela implique.  

La seconde, attirante celle-ci, sépare les données d'un côté et le template de l'autre. On a un fichier *Excel* d'un coté qui contient uniquement les données : la table de décision elle-même telle qu'une personne lambda peut l'imaginer.  

Et un template de règle de l'autre coté qui servira de patron pour créer les règles sur la base de la table de décision.  

Naturellement, le choix à été de se jeter sur la seconde solution comme un junky sur un rail de cocaïne. Et là, ce fut le drame...  

Il se trouve que dans sa version *6.2.0* (la version stable officielle au moment du développement du prototype), *Drools*  nécessite de compiler la table de décision en passant par le code, au contraire de la version *6.4* qui, elle, permet de simplement déclarer le fichier *Excel* et le template dans le fichier de configuration *kmodule.xml*.  

En plus, la façon de faire ne permet pas d'utiliser facilement cette méthode dans le cadre d'un *Ruleflow*. Mais alors, vraiment pas...


## La solution
Avec *Drools 6.2.0.Final*, pour pouvoir utiliser des tables de décision dans le cadre d'un *Ruleflow*, il vaut mieux utiliser la première façon, à savoir, un fichier *Excel* unique, contenant à la fois les données et le template.  

La construction de ce fichier est basée sur la convention plutôt que sur la configuration alors il faut bien respecter les libellés et la position des cellules contenant les données et le template.  

L'avantage de cette solution, parce qu'il y en a quand même un, c'est que, une fois que la table de décision est bien formée, il suffit de la placer à côté des autres règles, et c'est tout. Pas de configuration supplémentaire, par de code, rien.  

Le système compile tout seul la table de décision pour générer l'ensemble des règles qui s'y rapporte.

## L'implémentation
Nous allons développer un petit système de règles métier permettant de déterminer la catégorie d'âge d'un tireur en [*Savate Boxe Française*](http://www.esprit-savate.fr). 

{{< highlight java>}}
public class Boxer {
  private String nom;
  private int age;
  private int poids;
  private CategorieAge ageCat;
  private CategoriePoids poidsCat;
      
   [...]
}
{{< / highlight>}}

La détermination de la catégorie d'âge se fait au moment opportun dans le ruleflow :D  

![Ruleflow](/img/drools-dt-jbpmn/ruleflow.png)

Le *RuleFlowGroup* visible dans les propriétés de la *Rule Task* est positionné à *agePoidsCat*. Cette information nous permettra d'indiquer à *Drools* à quel moment exécuter notre table de décision dans le déroulement du *Ruleflow*.

### La table de décision

Nous voici enfin au cœur du problème : la table de décision :  

![Table de décision](/img/drools-dt-jbpmn/dt.png)

Pour l'écrire il faut se montrer très rigoureux car il n'y a pas d'aide à la saisie (pas de complétion automatique), il faut écrire certains libellés exactement comme demandé, dont certains à une place bien précise par rapport aux données.

### Les méta-données
C'est le premier cartouche de table de décision, celui où on indique le package de la règle, les imports et le *RuleFlowGroup* (il existe d'autres méta données, voir la [documentation officielle](http://docs.jboss.org/drools/release/6.2.0.Final/drools-docs/html_single/index.html)).  

Le nom de la méta-donnée doit être placé dans une cellule et sa valeur dans la cellule d'à côté.  

Petite particularité pour l'import, il faut séparer les différentes valeurs par une virgule. Apparemment, il est possible de mettre chaque valeur dans une suite de cellules les unes en-dessous des autres, mais je n'ai pas testé.  

Vient ensuite le template de la règle et des données. 

### Déclaration de la règle
*Drools* va rechercher une cellule du type "*RuleTable \<rulename\>*". Le mot-clé *RuleTable* lui indique le début de la règle.  

Le mot *\<rulename\>* lui servira pour nommer les règles générées (ici, *setagecat*).  

Pour voir le nom des règles générées, supprimez le point-virgule dans la colonne action, rafraîchissez *Ecplise* et exécutez le projet. Dans la console vous verrez apparaître le nom des règles.  

Je vous conseille de mettre un seul mot, sans espace, sans caractère accentué ni spécial pour le *\<rulename\>*.

### Déclaration des types de colonnes
À la suite du mot-clé *RuleTable*, *Drools* va rechercher le type des colonnes. En général, comme ici, on utilise les types *CONDITION* et *ACTION* (il en existe d'autres [dans la doc](http://docs.jboss.org/drools/release/6.2.0.Final/drools-docs/html_single/index.html#d0e5258)). Rien de bien méchant, attention juste aux majuscules et aux fautes de frappes.

### Écriture du template
On souhaite obtenir pour chaque ligne de la table de décision une règle comme celle-ci :  

{{< highlight java >}}
 package rfagot.examples.drools_620_dt_jbpmn.rules

 import rfagot.examples.drools_620_dt_jbpmn.model.Boxer
 import rfagot.examples.drools_620_dt_jbpmn.model.CategorieAge


 rule "setagecat"
 ruleflow-group "agePoidsCat"
 dialect "mvel"

    when
        boxer : Boxer(age >= $1, age <= $2)
    then
        boxe.setAgeCat($param);
 end 
{{< / highlight >}}

On retrouve le nom du package (*RuleSet*), les imports, le *RULEFLOW-GROUP*, et le nom des règles à générer (*setagecat*).  

Le passage de la règle littérale au template dans la table de décision ne pose pas de problème. La particularité ici, réside dans la condition à plusieurs paramètres et aux fautes de frappe.  

L'écriture d'une condition à plusieurs paramètres est simple à comprendre. Dans les données on sépare les valeurs par une virgule et on les référence par `$1` et `$2` (on peut bien sûr mettre plus de deux paramètres). La subtilité vient du tableur.   

En français, le séparateur des décimaux est la virgule. Si vos paramètres sont des entiers comme ici, *Excel* les interprétera comme un nombre décimal et marquera la cellule comme tel et *Drools* ne sera pas capable d'interpréter correctement la cellule comme une suite de deux valeurs (ne me demandez pas pourquoi...). Pour que la cellule soit correctement interprétable par *Drools* il faut la marquer comme zone de texte :  

![Format de la cellule texte](/img/drools-dt-jbpmn/cellule-texte.png)  

Comme il n'y a pas de complétion automatique ni de compilation à la volée il faut être rigoureux sur l'écriture du template. Je vous conseille d'écrire une règle telle quelle doit être générée, de la tester et ensuite de créer la table de décision en faisant des copier-collers.

## L'exécution
Une fois la table de décision écrite et sauvegardée, le travail s'arrête là. Il n'y a pas de code à écrire ni de déclaration à faire dans le *kmodule.xml*. *Drools* s'occupe d'identifier les tables de décisions présentes dans les ressources et de générer les règles correspondantes.  

Exécutez la classe `Main.java` comme projet java. En sortie, dans la console vous devez avoir :  

{{< highlight console >}}
Pierre(12 ans, 40 kg) est Benjamins
Jacques(36 ans, 73 kg) est VeteransCombat
{{< / highlight >}}

**Attention** : les tables de décisions sont gourmandes en mémoire. Utilisez-les en connaissance de cause !  

Le projet d'exemple se trouve sur <https://github.com/richard-fagot/drools-6.2.0-dt-jbpmn>
