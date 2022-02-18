---
layout: page
title:  "étude / algorithmes d'exponentiation"
category: cours
tags: informatique cours 
author: "François Brucker"
---

> [Algorithme, code et théorie]({% link cours/algorithme-code-theorie/index.md %}) / [algorithmie]({% link cours/algorithme-code-theorie/algorithme/index.md %}) / [étude : l'exponentiation]({% link cours/algorithme-code-theorie/algorithme/etude-exponentiation.md %})
>
> prérequis :
>
>* [complexité max/min]({% link cours/algorithme-code-theorie/algorithme/complexite-max-min.md %})
>* [preuve d'algorithme]({% link cours/algorithme-code-theorie/algorithme/preuve-algorithme.md %})
{: .chemin}

On va étudier deux algorithmes permettant de calculer $a^b$  à partir de deux entiers $a$ et $b$. Pour chaque algorithme on étudiera son fonctionnement selon [3 axes]({% link cours/algorithme-code-theorie/algorithme/algorithmes.md %}#étude) :

* fonctionnement
* preuve
* complexité

> On utilisera le python comme langage de pseudo-code

## algorithme naïf {#algo-naif}

Le calcul *naïf* de l'exponentiel est basé sur sa définition mathématique, qui peut être décrite, pour deux entiers positifs $x$ et $y$,  par l'équation suivante :

$$
x^y = \left\{
    \begin{array}{ll}
        x \cdot x^{y-1} & \mbox{si } y > 0 \\
        1 & \mbox{sinon.}
    \end{array}
\right.
$$

> Ecrivez un algorithme récursif pour résoudre cette équation.
{: .a-faire}
{% details  une solution possible %}

```python
def puissance(nombre, exposant):
    if exposant == 0:
        return 1
    return nombre * puissance(nombre, exposant - 1)
```

Cet algorithme est exactement la transcription de la définition mathématique, il est donc correct.

{% enddetails %}

Pour cette étude, nous allons uniquement utiliser des algorithmes non récursifs (ils sont dit itératifs).

> Ecrivez un algorithme itératif pour calculer $x^y$  avec $x$ et $y$ deux entiers positifs.
{: .a-faire}
{% details une solution possible  %}

<style>
    table, td, tr, th, pre {
        padding:0;
        margin:0;
        border:none
    }
</style>
{% highlight python linenos %}

def puissance(nombre, exposant):
    résultat = 1
    compteur = exposant
    while compteur > 0:
        résultat *= nombre
        compteur -= 1
    return résultat

{% endhighlight %}
{% enddetails %}

C'est cet algorithme itératif que nous allons étudier maintenant.

### est-ce que ça marche ? {#marche-naïf}

On test l'algorithme itératif sur de petits exemples qui vont nous permettre d'appréhender son fonctionnement :

> On teste sur de petits nombres en se mettant à la place de l'ordinateur.
>
> * on numérote chaque ligne
> * on note sur une feuille les variables
> * on exécute ligne à ligne en notant les différents résultats.
> * à la fin on vérifie que `résultat` vaut bien ce qu'il doit valoir.
>
{: .note}

Les cas simples que l'on peut essayer sans peine, et permet de **tester les cas limites** :

* exposant vaut 0 ou 1
* nombre vaut 2 ou 3 (un peu plus que les cas triviaux)

Puis un cas un peu plus compliqué pour **tester si les boucles fonctionnent bien** :

* exposant vaut 2 ou 3
* nombre vaut 2 ou 3

> Vérifiez que l'algorithme donne bien les bons résultats sur les exemples ci-dessus.
{: .a-faire}

Une fois qu'on est convaincu que ça fonctionne, on prouvera sa finitude, sa preuve et on calculera sa complexité.

### preuve {#preuve-naif}

En deux temps. On commence par montrer qu'il se termine, puis on prouve qu'il calcule bien l'exponentiation.

#### finitude {#finitude-naif}

* `compteur` diminue strictement à chaque boucle et la condition d'arrêt est lorsqu'il vaut 0
* condition : il faut que `compteur` soit un nombre >= 0 pour que l'algorithme s'arrête. Donc `exposant` doit être un nombre positif.

> Pour des nombres, on préférera toujours des conditions d'arrêt larges (plus petit que, plus grand que, différent de) plutôt que des conditions sur l'égalité stricte. Ceci pour deux raisons majeures :
>
> * L'égalité entre réels n'existe pas en informatique par exemple.
> * dans l'exemple ci-dessus mettre des exposants négatifs ou des nombres réels ne fait pas boucler infiniment notre algorithme
>
{: .note}

#### preuve de l'algorithme

Le fonctionnement de l'algorithme est *à peu prêt* clair si les entrées sont des entiers : il multiplie $a$ par lui-même $b$ fois grâce à une boucle. Une preuve par récurrence doit donc fonctionner, mais essayons de faire une *jolie* preuve en exhibant un invariant de boucle.

> Si `nombre` et `exposant` sont des entiers naturels, on a l'invariant de boucle :
> `resultat * nombre ** compteur = nombre ** exposant` (en utilisant l'opération `**` qui signifie exposant en python.)
{: .note}

Prouvons cet invariant.

Juste avant la première itération de la boucle, `resulat = 1` et `compteur = exposant` notre invariant est donc vérifié. On suppose l'invariant vrai au début de la boucle $i$. Comme expliqué dans la partie sur les [preuves d'algorithmes]({% link cours/algorithme-code-theorie/algorithme/preuve-algorithme.md %}), on met un `'` aux variable après l'itération :

* `nombre' = nombre`
* `exposant' = exposant`
* `resulat' = resultat * nombre`
* `compteur' = compteur - 1`

On a alors :  `resultat' * nombre' ** compteur' = (resultat * nombre) * nombre ** (compteur - 1) = resultat * nombre ** compteur = nombre ** exposant = nombre' ** exposant'`

On a démontré notre invariant de boucle.

> Notre invariant est vrai avant et après chaque itération, il est donc également vrai à la fin de l'algorithme, lorsque `compteur = 0`. Et là : `resultat * nombre ** compteur = resultat = nombre ** exposant`
{: .note}

### complexité {#complexite-naif}

Ligne à ligne :

1. définition de la fonction : $\mathcal{O}(1)$
2. une affection : $\mathcal{O}(1)$
3. une affection : $\mathcal{O}(1)$
4. une boucle de $\mathcal{O}(\mbox{exposant})$ itération (`compteur` vaut initialement `exposant` et décrémente de $1$ à chaque itération)
5. une multiplication et une affection : $\mathcal{O}(1)$
6. une soustraction et une affection : $\mathcal{O}(1)$
7. retour de la fonction : $\mathcal{O}(1)$

Ce qui donne une complexité de :

$$
\begin{array}{lcl}
C & = & \mathcal{O}(1) + \\
&  & \mathcal{O}(1) + \\
& & \mathcal{O}(1) + \\
& & \mathcal{O}(\mbox{exposant}) \cdot ( \\
& & \mathcal{O}(1) + \\
& & \mathcal{O}(1)) + \\
& & \mathcal{O}(1)\\
& = & 3 \cdot \mathcal{O}(1) + \mathcal{O}(\mbox{exposant}) \cdot (2 \cdot \mathcal{O}(1)) + \mathcal{O}(1)\\
&=& 4 \cdot \mathcal{O}(1) + 2 \cdot \mathcal{O}\mbox({exposant})\\
&=& \mathcal{O}(1) + \mathcal{O}(\mbox{exposant})\\
C&=& \mathcal{O}(\mbox{exposant})\\
\end{array}
$$

## exponentiation indienne {#algo-rapide}

Aussi appelé [exponentiation rapide](https://fr.wikipedia.org/wiki/Exponentiation_rapide), cette façon de calculer l'exponentielle est basée sur l'équation suivante, pour deux entiers positifs $x$ et $y$ :

$$
x^y = \left\{
    \begin{array}{ll}
        1 & \mbox{si } y = 0 \\
        x \cdot x^{y-1}  &\mbox{si } y  \mbox{ est impair}\\
        x^{\frac{y}{2}}  \cdot x^{\frac{y}{2}} = (x^2)^{\frac{y}{2}}  &\mbox{si } y  \mbox{ est pair}\\
    \end{array}
\right.
$$

> Ecrivez un algorithme récursif pour résoudre cette équation.
{: .a-faire}
{% details  une solution possible %}

```python
def puissance(nombre, exposant):
    if exposant == 0:
        return 1
    elif compteur % 2 != 0:
        return nombre * puissance(nombre, exposant - 1)
    else:
        return nombre * nombre * puissance(nombre, exposant // 2)
    return 
```

On a utiliser deux choses :

* L'opérateur `%` signifie *modulo* en python : il retourne le reste de la division entière. L'algorithme s'en sert pour vérifier si `compteur` est pair (reste de la division entière par 2 vaut 0) ou impair (reste de la division entière par 2 vaut 1)
* la division entière `//` pour s'assurer que exposant reste un entier. Le type de `4 / 2` en python est un réel alors que le type de `4 // 2` est un entier.

Cet algorithme est exactement la transcription de la définition mathématique, il est donc correct.

{% enddetails %}

Pour cette étude, nous allons uniquement utiliser des algorithmes non récursifs (ils sont dit itératifs).

> Ecrivez un algorithme itératif utilisant l'exponentiation indienne pour résoudre $x^y$  avec $x$ et $y$ deux entiers positifs.
{: .a-faire}
{% details une solution possible  %}

<style>
    table, td, tr, th, pre {
        padding:0;
        margin:0;
        border:none
    }
</style>
{% highlight python linenos %}

def puissance(nombre, exposant):
    resultat = 1
    compteur = exposant

    while compteur > 0:
        if compteur % 2 != 0:
            resultat *= nombre
            compteur -= 1
        else:
            nombre *= nombre
            compteur /= 2

    return resultat

{% endhighlight %}
{% enddetails %}

C'est cet algorithme itératif que nous allons étudier maintenant.

### est-ce que ça marche ? {#marche-rapide}

Comme pour l'algorithme naïf, on vérifie que tout fonctionne avec les cas simples :

* exposant vaut 0 ou 1
* nombre vaut 2 ou 3 (un peu plus que les cas triviaux)

Enfin, comme l'algorithme vérifie si `compteur` est pair ou impair, on peut essaier un exposant un peu plus grand, par exemple :

* `exposant = 7`
* `nombre = 2` (pas trop grand pour pouvoir calculer facilement les résultats de tête)

> Vérifiez que l'algorithme donne bien les bons résultats sur les exemples ci-dessus.
{: .a-faire}

### preuve de finitude {#finitude-rapide}

De même que pour l'algorithme simple, `compteur` diminue strictement à chaque boucle (ou il diminue de `-1` ou il est divisé par 2). Si `exposant` est un entier naturel en entrée, `compteur` reste entier après chaque boucle (on ne le divise par 2 que s'il est pair) et est strictement plus petit : l'algorithme va s'arrêter à un moment.

### preuve de l'algorihtme {#preuve-rapide}

On va montrer que l'invariant de l'algorithme naïf fonctionne aussi. En notant `compteur_initial`, la valeur de compteur en entrée de l'algorithme, on a l'invariant suivant : `resultat * nombre ** compteur = nombre_initial ** exposant`

#### conditions initiales {#invariant-rapide-init}

Juste avant la première itération de la boucle, `resulat = 1` et `compteur = exposant` notre invariant est donc vérifié.

#### preuve de l'invariant {#invariant-rapide-preuve}

On suppose l'invariant vrai au début de la boucle d'itération $i$. Regardons comment les variables ont été modifiées lors de cette itération :

* si compteur est impair on a :
  * `compteur' = compteur - 1`
  * `resultat' = resultat * nombre`
  * `nombre' = nombre`
  * l'invariant vaut alors en fin d'itération : `resultat * nombre ** compteur = (resultat * nombre) * nombre ** (compteur - 1) = resultat' * nombre' ** compteur'`
* si compteur est impair on a :
  * `compteur' = compteur - 1`
  * `resultat' = resultat`
  * `nombre' = nombre * nombre`
  * l'invariant vaut alors en fin d'itération : `resultat * nombre ** compteur = resultat * (nombre * nombre) ** (compteur / 2)  = resultat' * nombre' ** compteur'`

Dans tous les cas, l'invariant est toujours vérifié puisqu'en début de boucle notre invariant vaut `resultat * nombre ** compteur = nombre_initial ** exposant`.

#### preuve de l'algorithme {#preuve-rapide}

Notre invariant est vrai avant et après chaque itération, il est donc également vrai à la fin de l'algorithme, lorsque `compteur = 0`. Et là : `resultat * nombre ** compteur = resultat = nombre_initial ** exposant`

### complexité {#complexite-rapide}

Pourquoi s'embêter avec la parité de compteur ? Parce que ça permet d'aller vachement plus vite !

On va le démontrer petit à petit, mais commençons par analyer ligne à ligne la complexité :

1. définition de fonction $\mathcal{O}(1)$
2. une affectation : $\mathcal{O}(1)$
3. une affectation : $\mathcal{O}(1)$
4. 
5. une comparaison en $\mathcal{O}(1)$ et $k$ itérations de boucle
6. une opération de division entière et un test : $\mathcal{O}(1)$
7. une opération et une affectation : $\mathcal{O}(1)$
8. une opération et une affectation : $\mathcal{O}(1)$
9. 
10. une opération et une affectation : $\mathcal{O}(1)$
11. une opération et une affectation : $\mathcal{O}(1)$
12. 
13. un retour de fonction : $\mathcal{O}(1)$

Ce qui donne une complexité de :

$$
\begin{array}{lcll}
C & = & \mathcal{O}(1) + &\\
&  & \mathcal{O}(1) + &\\
&  & \mathcal{O}(1) + &\\
&  & k \cdot (\mathcal{O}(1) + &\\
& & \mathcal{O}(1) + &\\
& & \mathcal{O}(1) + &\mbox{(ligne 7 ou ligne 10)}\\
& & \mathcal{O}(1) + & \mbox{(ligne 8 ou ligne 11)}\\
& & \mathcal{O}(1)) +&\\
& & \mathcal{O}(1)&\\
&=& 3 \cdot \mathcal{O}(1) + k \cdot (5\cdot \mathcal{O}(1)) + \mathcal{O}(1)&\\
&=& 4 \cdot \mathcal{O}(1) + k \cdot 5 + &\\
C&=&\mathcal{O}(k)&\\
\end{array}
$$

La complexité est de l'ordre du nombre de fois où l'on rentre dans la boucle `while` : c'est à dire le nombre de fois où `compteur` a été modifié sans être égal à 0.

#### nombre de fois où compteur est impair

Si à l'itération numéro $i$ compteur est impair, il sera pair à l'itération $i + 1$ car `compteur' = compteur - 1` dans ce cas là.

On a donc que : **le nombre d'itérations où compteur est impair est au pire égal au nombre de fois où il est pair**

#### nombre de fois où le compteur est pair

A chaque fois où compteur est pair, on le divise par 2. Si $k$ est le nombre de fois où le compteur a été pair, on a que : $2^k \leq \mbox{nombre}$ (avec  `nombre` le paramètre d'entrée).

Comme `nombre` est un entier, il existe un nombre $p$ tel que $2^p \leq \mbox{nombre} < 2^{p + 1}$.

On ne peut donc pas diviser par 2 `nombre`, ou un nombre plus petit que lui, plus de `p` fois. Et $p$ vaut la partie entière de $\log_2(\mbox{nombre})$. En effet :

$$
\begin{array}{lcccl}
    2^p &\leq &\mbox{nombre} &<& 2^{p + 1}\\
    \log_2(2^p) &\leq &\log_2(\mbox{nombre}) &< &\log_2(2^{p + 1}) \mbox{ (car la fonction est croissante)} \\
    p &\leq &\log_2(\mbox{nombre}) &<& p + 1
\end{array}
$$

> Pour tout nombre k, le nombre de fois où l'on peut diviser un nombre $x$ par $k$ est $\log_k(x)$

On a donc que : **le nombre d'itérations où compteur est pair est au pire égal à $\log_2(\mbox{nombre})$**

#### nombre de fois où l'on rentre dans la boucle

Le nombre de fois où l'on rentre dans la boucle est égal au nombre de fois où le compteur est pair plus le nombre de fois où le compteur est impair, c'est donc au pire égal à deux fois le nombre de fois où compteur est pair, c'est à dire $2 \cdot \log_2(\mbox{compteur})$ pour la valeur initiale de compteur.

Comme `compteur` vaut initialement `exposant`, le nombre de fois où l'on rentre dans la boucle est de l'ordre de $\mathcal{O}(\log_2(\mbox{exposant}))$ donc en $\mathcal{O}(\ln(\mbox{exposant}))$.

Comme les autres lignes sont en $\mathcal{O}(1)$ on a une complexité de l'algorithme en $\mathcal{O}(\ln(\mbox{exposant}))$.

Cette complexité est très faible ! Comparez par exemple : $2^{16} = 65536$ opérations et $\log_2(65536) = 16$ opérations.

Cette différence va aller exponentiellement lorsque compteur augmente, par exemple entre $2^{100} = 1267650600228229401496703205376$ et $100$ opérations

## conclusions

* la procédure utilisée pour l'étude de ces deux algorithmes est générale, vous pouvez (et devez) l'appliquer à l'étude de tout nouvel algorithme.
* il ne faut jamais penser que l'on ne peut pas faire mieux pour un algorithme. Si vous ne connaissiez pas l'exponentiation indienne, il vous aurait été difficile de penser que l'on peut faire mieux que l'algorithme naïf pour calculer une exponentielle
* un algorithmicien ferait beaucoup de sacrifices pour obtenir une complexité en $\mathcal{O}(\ln(n))$ tellement c'est efficace.