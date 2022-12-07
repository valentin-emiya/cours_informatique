---
layout: layout/post.njk 
title: "MPCI S2 : Programmation et Algorithmes"

tags: ['formation', 'MPCI']

eleventyNavigation:
  key: MPCI
  parent: Enseignements
  order: 3
---

{% prerequis "**Prérequis** :" %}

* [S1 MPCI : Programmation](https://ametice.univ-amu.fr/course/view.php?id=97114)
* [Bases de python]({{ '/cours/base-code' | url }})

{% endprerequis %}

Les cours ont lieu les mardi (8h-10h) et vendredi (8h-12h).

{% info %}
Ce cours fait partie du cours [Algorithme, code et théorie]({{ "/cours/algorithme-code-théorie" | url }}), qui contient un peu plus de choses.
{% endinfo %}

## Plan

Le cours est composée de 3 parties de 3 semaines chacune, entre-coupées de devoirs surveillés de ... 3 heures :

1. [partie *complexité*](./#partie-1)
2. DS1 : sur la partie complexité. Sur table
3. [partie *programmation objet*](./#partie-2)
4. DS2 : sur la partie programmation objet. Sur ordinateur
5. [partie *résolution de problèmes*](./#partie-3)
6. ET : porte sur l'intégralité du programme, voir un peu plus.

Chaque **vendredi** à partir de la semaine 2 les 15 ($=3+3+3+3+3$ minutes) premières minutes du cours seront consacrées à un test portant sur le programme de la semaine précédente.

{% note %}
Les divers contrôles intermédiaires seront à rendre directement sur [AMeTICE](https://ametice.univ-amu.fr/course/view.php?id=101942)
{% endnote %}

> TBD : parler de méthode de développement partie 1 tests / partie 2 : coverage & documentation en markdown / partie 3 : virtualenv

## Note

La note de cette UE résulte de cette formule :

$$
\max (\frac{CC+ DS + ET}{3}, ET)
$$

Avec :

* $CC = \frac{1}{2}(TUT + TEST)$ où :
  * $TUT$  est la moyenne formée des 2 notes de tutorats
  * $TEST$ est la moyenne des tests de début de séances ($6 = 3 + 3$ tests).
* $DS$ est la moyenne des DS1 et DS2
* $ET$ est l'examen terminal

## <span id="partie-0"></span> Partie 0 : Mise en place

{% note %}
Faites les mise ne place nécessaire pour suivre l'enseignement. S'il vous manque des connaissances, suivez les tutoriels et si vous avez encore des doutes après ça, n’hésitez pas à me contacter.
{% endnote %}

Nous allons coder tous nos algorithmes en python. Il est donc nécessaire d'avoir un système fonctionnel. Vérifiez donc avant le début du cours que :

1. [vous avez un système en état de marche]({{ '/tutoriels/installation-système' | url }})
2. [vous savez naviguer dans un système de fichiers]({{ '/tutoriels/fichiers-navigation' | url }})
3. Il pourra de plus être très utile de : [Savoir ouvrir une fenêtre terminal]({{ '/tutoriels/terminal'  | url }})

## <span id="partie-1"></span> Partie 1 : Complexité

### <span id="partie-1.1"></span> Semaine 1

#### <span id="partie-1.1.1"></span> Mardi

1. [Un algorithme ?]({{ "/cours/algorithme-code-théorie/algorithme/définition" | url }})
2. [Pseudo-code]({{ "/cours/algorithme-code-théorie/algorithme/pseudo-code" | url }})
3. [Fonctions]({{ "/cours/algorithme-code-théorie/théorie/fonctions" | url }})

#### <span id="partie-1.1.2"></span> Vendredi

Nous allons utiliser vscode pour la première fois ce TD. Faites les prérequis avec le début du cours.

{% prerequis "**Prérequis** :" %}

* [Installation et prise en main de vsc]({{ '/tutoriels/vsc-installation-et-prise-en-main' | url }})
* [Utiliser python avec vsc]({{ '/tutoriels/vsc-python' | url }})
* [Utiliser un terminal]({{ '/tutoriels/terminal-utilisation' | url }})

{% endprerequis %}

1. [Coder]({{ "/cours/algorithme-code-théorie/code/coder" | url }})
2. [Projet 1 : mise en œuvre d'un projet informatique]({{ "/cours/algorithme-code-théorie/code/projet-hello-dev" | url }})
3. [Projet 2 : pourcentage]({{ '/cours/algorithme-code-théorie/code/projet-pourcentages' | url}})

### <span id="partie-1.2"></span> Semaine 2

{% note %}
Le contrôle de vendredi portera sur la partie code. Il faudra rendre un (ou plusieurs) fichiers python sur AMeTICE.
{% endnote %}

#### <span id="partie-1.2.1"></span> Mardi

1. [Preuve d'algorithme]({{ "/cours/algorithme-code-théorie/algorithme/preuve-algorithme" | url }})
2. [Complexité max/min]({{ "/cours/algorithme-code-théorie/algorithme/complexité-max-min" | url }})

#### <span id="partie-1.2.2"></span> Vendredi

1. [Etude : exponentiation]({{ "/cours/algorithme-code-théorie/algorithme/étude-exponentiation" | url }})
2. [Projet : exponentiation]({{ "/cours/algorithme-code-théorie/code/projet-exponentiation" | url }})

> TBD : un projet supplémentaire à faire.

### <span id="partie-1.3"></span> Semaine 3

{% note %}
Le contrôle de vendredi portera sur la partie complexité et preuve d'algorithme. Il faudra rendre une copie.
{% endnote %}

#### <span id="partie-1.3.1"></span> Mardi

1. [Complexité d'un problème]({{ "/cours/algorithme-code-théorie/théorie/complexité-problème" | url }})
2. [Etude : mélanger un tableau]({{ "/cours/algorithme-code-théorie/algorithme/étude-mélange" | url }})

#### <span id="partie-1.3.2"></span> Vendredi

1. Complexité amortie
2. [Complexité en moyenne]({{ "/cours/algorithme-code-théorie/algorithme/complexité-moyenne" | url }})
3. [Etude : trier un tableau]({{ "/cours/algorithme-code-théorie/algorithme/étude-tris" | url }})
4. [Projet : tris]({{ "/cours/algorithme-code-théorie/code/projet-tris" | url }})

> TBD :
>
> * que faire lorsque les temps peuvent être très différents selon les cas -> amortie (on calcule tout finement : exemple des jets de dés (comme livre) . Finement avec ajout/enlever) ou moyenne (on mesure)
> * exemple compteur binaire (livre + https://www.lama.univ-savoie.fr/mediawiki/images/2/27/INFO602-Lesson-2.pdf) et généralisation aux lancés de dés. En cours passer rapidement sur l'amorti.
> * pour la complexité en moyenne : faire rapidement un exemple. Ils ont du déjà faire un tri en S1

## DS 1 (Semaine 4)

Devoir surveillé 1 : sur table.

Au programme :

* complexité (min/max/amortie/moyenne/problème)
* preuve d'algorithmes
* algorithmes de tris

## <span id="partie-2"></span> Partie 2 : Programmation Objet

### <span id="partie-2.1"></span> Semaine 5

{% info %}
Pas de contrôle cette semaine.
{% endinfo %}

{% attention %}
A partir de la partie 2, les contrôles de début séance seront à écrire en [markdown]({{ '/tutoriels/format-markdown' | url }}) et envoyé converti en html (ou pdf) sur AMeTICE.
{% endattention %}

#### <span id="partie-2.1.1"></span> Mardi

1. [Mémoire et espace de noms]({{ "/cours/algorithme-code-théorie/code/mémoire-espace-noms" | url }})
2. [Classes et objets]({{ "/cours/algorithme-code-théorie/code/programmation-objet/classes-et-objets" | url }})

#### <span id="partie-2.1.2"></span> Vendredi

> TBD : un projet complet du code normal à la programmation objet.

1. [black et code coverage]({{ "/tutoriels/style-couverture" | url }})

2. projet code

### <span id="partie-2.2"></span> Semaine 6

#### <span id="partie-2.2.1"></span> Mardi

1. [Composition et agrégation]({{ "/cours/algorithme-code-théorie/code/programmation-objet/composition-agrégation" | url }})
2. [Héritage]({{ "/cours/algorithme-code-théorie/code/programmation-objet/héritage" | url }})

#### <span id="partie-2.2.2"></span> Vendredi

1. [Projet : composition et agrégation]({{ "/cours/algorithme-code-théorie/code/programmation-objet/projet-composition-agrégation" | url }})
1. [Projet : héritage]({{ "/cours/algorithme-code-théorie/code/programmation-objet/projet-héritage" | url }})

### <span id="partie-2.3"></span> Semaine 7

#### <span id="partie-2.3.1"></span> Mardi

1. [Programmation événementielle]({{ "/cours/algorithme-code-théorie/code/programmation-évènementielle" | url }})

#### <span id="partie-2.3.2"></span> Vendredi

1. [Projet : programmation événementielle]({{ "/cours/algorithme-code-théorie/code/projet-programmation-évènementielle" | url }})

Pour aller plus loin : [Projet : TDD]({{ "/cours/algorithme-code-théorie/code/programmation-objet/projet-TDD" | url }})

## DS 2 (Semaine 8)

Devoir surveillé 2 : sur ordinateur.

Au programme :

* code

## <span id="partie-3"></span> Partie 3 : Résolution de Problèmes

### <span id="partie-3.1"></span> Semaine 9

{% info %}
Pas de contrôle cette semaine.
{% endinfo %}

#### <span id="partie-3.1.1"></span> Mardi

> TBD : partie générale sur les structures de données. A quoi ça sert et comment s'en servir. Puis cas particulier des tableau/listes et des dictionnaires.
> TBD faire la complexité amortie de ajout/suppression dans une liste.

1. [Structure : liste]({{ "/cours/algorithme-code-théorie/algorithme/structure-liste" | url }})
2. [Fonctions de hash]({{ "/cours/algorithme-code-théorie/théorie/fonctions-hash" | url }})
3. [Structure : dictionnaire]({{ "/cours/algorithme-code-théorie/algorithme/structure-dictionnaire" | url }})

#### <span id="partie-3.1.2"></span> Vendredi

1. gloutons
2. projet gloutons

### <span id="partie-3.2"></span> Semaine 10

#### <span id="partie-3.2.1"></span> Mardi

Machine de Turing

#### <span id="partie-3.2.2"></span> Vendredi

> TBD : virtualenv et poetry.

fichiers et alignement de séquences ?

### <span id="partie-3.3"></span> Semaine 11

#### <span id="partie-3.3.1"></span> Mardi

NP-complétude

#### <span id="partie-3.3.2"></span> Vendredi

> TBD : sac à dos ? fractionnaire. puis optimal 1, puis optimal mais exponentiel en mémoire puis gloutons.

### semaine 12

Contrôle final : sur table.

Au programme :

* tout
* voir un peu plus

## tests

> TBD mettre en lien les annales.