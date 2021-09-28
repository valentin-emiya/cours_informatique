---
layout: page
title:  "Héritage"
category: cours
tags: mie
authors: 
  - François Brucker
  - Célia Châtel
---

Présentation du mécanisme d'héritage. 

## principe de l'héritage

principe. 

factorisation de code : mieux de factoriser les les fonctionnalités. Surout que ça concerve l'implémentation. 

comportement par défaut (__str__, est un exemple)

dans les bibliothèques : ils donnent une classe t nous on la particuliarise (GUI)



### Exercice 1

L'idée est juste de présenter avec quelque chose de simple et facile à se représenter la notion d'héritage. On donnera l'UML des classes dans tous les cas et le code seulement s'il est lié à l'héritage.

Classe `Point` :

![point]({{ "img/point.png"}})

Rien de particulier, pour la classe `Polygon` qui est une agrégation avec points :

![polygon]({{ "img/polygon.png"}})

C'est bien une agrégation puisque utilise des objets `Point` comme attribut mais ces points existent indépendamment du polygone et on les ajoute dans l'attribut `vertices` lors de la création de l'objet.

Classe `Triangle`:

![triangle]({{"img/triangle.png"}})

L'héritage arrive ici. On fait une version restreinte du polygone très simple. La classe `Triangle` hérite de `Polygon`, on appelle donc le constructeur de ce dernier lors de la création d'un `Triangle`.

Ceci est explicite en python :


~~~ python
class Triangle(Polygon):
  def __init__(self, point1, point2, point3):
    super().__init__([point1, point2, point3])
~~~

Le mot clé `super()` désigne la classe parente, ici `Polygon`.Ce mot clé permet d'utiliser toutes les méthodes de la classe parente, ici `__init__`. Remarquez que l'on utilise la méthode `__init__` sans utiliser le premier paramètre (`self`) qui est implicitement l'objet courant. 

L'UML complet donne donc :

![polygone_uml_entier]({{ "img/polygone_uml_entier.png" }})

### Exercice 2

La classe `Personnage` ne pose normalement pas de problèmes :

![personnage]({{ "img/personnage.png" }})

On précise le code de `taper` et `se_faire_taper` qui permet à chacun de se faire taper comme il l'entend :


~~~ python
def taper(self, personnage):
    personnage.se_faire_taper(self)

def se_faire_taper(self, personnage):
    self.set_vie(self.get_vie() - personnage.get_attaque())
~~~


On ajoute la guerrière :

![guerriere]({{ "img/guerriere.png"}})

On donne ci-après une partie du code de la guerrière  (on a en particulier pas écrit la méthode `bloque` qui fait le tirage pour savoir si on bloque ou pas). Faites attention et comprenez bien : 

  -  l'appel à `super().__init__()` au début du constructeur de la classe fille,
  - qu'on ajoute un attribut à la guerrière par rapport au personnage normal,
  - la méthode `se_faire_taper(personnage)` utilise la méthode `se_faire_taper` de la classe `Personnage` seulement si la guerrière ne bloque pas le coup. Le `super().methode_de_la_mere()` permet d'accéder à la méthode de la classe mère même de même nom qu'une méthode (différente) de la classe fille.


~~~ python
class Guerriere(Personnage):
    def __init__(self, vie, attaque, blocage):
        super().__init__(vie, attaque)
        self.blocage = blocage

    def se_faire_taper(self, personnage):
        if not self.bloque(personnage):
            super().se_faire_taper(personnage)
~~~

Prenez le temps de faire des exemples d'utilisation et de vérifier que tous les cas marchent. En particulier qu'est-ce qui est appelé quand on fait `guerriere.se_faire_taper(bonhomme)` avec un objet `guerriere` de la classe `Guerriere` ?

Le magicien permet de montrer l'ajout d'une méthode qui n'était pas du tout dans la classe mère :

![magicien]({{ "img/magicien.png"}})

Le code n'est pas difficile, on se passera donc de l'écrire complètement. Il faut :

  - ajouter une méthode `lancer_sort`
  - ajouter un paramètre et son attribut associé `attaque_magique` au constructeur
  - ajouter une méthode `se_faire_toucher_par_un_sort(magicien)` avec un paramètre de type Magicien dans la classe Personnage.

> **Nota Bene :** Ces exemples sur l'héritage sont un peu forcés. C'est parce que l'héritage n'est que très peu utilisé en code pure. Il est même considéré comme préjudiciable dans la plupart des cas (voir )[là](https://codeburst.io/inheritance-is-evil-stop-using-it-6c4f1caf5117) ou encore [là](http://neethack.com/2017/04/Why-inheritance-is-bad/)). 
> >Un cas d'utilisation reconnu est cependant lorsque l'on veut utiliser des classes définies dans un module quelconque et la mettre un peu à notre sauce. Comme dans des bibliothèques graphiques par exemple.

## points de vigilance

Toujours très aimé mais l'intérêt est plus réduit qu'on ne peu le penser. Avant de faire de l'héritage regardez si une composition et un agrégation ne feraient pas mieux le travail.


attention : aux variable de la classe qui ne doivent pas être redéfini dans l'héritage (mais on ne sais pas lesquelles c'est...)
En python `__variable`  n'est pas passée aux descendants.

Si l'on redéfini toutes les classes de la classe mere sans les utililser : pas un bon signe.

héritage multiple autorisé en python, mais c'est très compliqué. règle de u diamant : c'est fait pour simplifier le code pas le rendre necore plus compliqué.


## variables de classe

parler des variables de classes. 
