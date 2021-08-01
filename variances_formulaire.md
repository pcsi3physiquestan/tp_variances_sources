---
jupytext:
  encoding: '# -*- coding: utf-8 -*-'
  formats: ipynb,md:myst
  split_at_heading: true
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.10.3
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

On rappelle qu'on suppose qu'on a des mesurandes $X_i$ dont les valeurs mesurées sont $x_i$ et les incertitudes $u(X_i)$.

On veut déterminer le résultat de mesurage $y$ et l'incertitude $u(Y)$ d'un mesurande $Y$ dont on a posé la relation : $Y = f(X_i)$.

# Présentation

## Principe
Comme on l'a vu, on considère que les mesurandes sont assimilables à des variables aléatoires et qu les incertitudes sont des estimations des écart-types de ces variables aléatoires.

Le carré d'un écart-type est appelé _variance_ et lorsqu'on réalise une opérations entre deux variables aléatoires (ex : $X_1 + X_2$), des théorèmes mathématiques permettent, __sous conditions__, de relier les variances es $X_i$ à la variance de $Y$.

````{admonition} Exemple
:class: note
Dans le cas $Y = X_1 + X_2$, si les variables $X_1$ et X_2$ sont indépendantes (entre autre), alors, on peut montrer que :

$$
v_Y = v_{X_1} + v_{X_2}
$$

soit pour les écart-type :

$$
\sigma_Y = \sqrt{\sigma^2_{X_1} + \sigma^2_{X_2}}
$$

````

La __méthode de la propagation de la variance__ propose d'utiliser ces relations mathématiques entre variances pour calculer l'incertitude $u(Y)$ à partir des incertitudes $u(X_i)$.

## Hypothèses
On ne donne pas ici toutes les hypothèses précises nécessaires pour utiliser ces relations, d'autant qu'en général, on n'a pas la certitude qu'elles soient valables !

* Indépendance des mesurandes (c'est __fondamental__).
* Distribution statistique peu irrégulière
* La relation $Y=f(X_i)$ est linéaire ou proche.

## Cas à connaître
_Toutes ces expressions sont admises._

On peut ensuite utiliser une composition de ces différents cas.

### Somme
````{important} 
Si $Y = \alpha_1 X_1 + \alpha_2 X_2$ alors :

$$
\sigma_Y = \sqrt{\alpha_1 ^2 \sigma^2_{X_1} + \alpha_2 ^ 2\sigma^2_{X_2}}
$$
````

_Généralisation_ : 

Si $Y = \sum__i \alpha_i X_i $ alors :

$$
\sigma_Y = \sqrt{\alpha_i^2 \sigma^2_{X_i}}
$$

### Produit
````{important} 
Si $Y =  X_1^{\beta_1} \times X_2^{\beta_1}$ alors :

$$
\frac{\sigma_Y}{Y} = \sqrt{\beta_1 ^2 \frac{\sigma^2_{X_1}}{X_1^2} + \beta_2 ^2 \frac{\sigma^2_{X_2}}{X_2^2}}
$$
````

_Généralisation_ : 

Si $Y = \prod_i X_i^{\beta_i} $ alors :

$$
\frac{\sigma_Y}{Y} = \sqrt{\beta_i ^2 \frac{\sigma^2_{X_i}}{X_i^2}}
$$

````{attention} 
Le cas $Y=X^2$ n'est pas un produit car $X$ n'est pas indépendant de $X$.

````

### Fonction d'une variable
````{important} 
Si $Y = f(X)$ alors, si f n'est pas trop non linéaire :

$$
u(Y) = \left\vert \frac{\rm{d}Y}{\rm{dX}}(x_{mes}) \right\vert u(X)
$$
````

## Limites
L'avantage de la propagation des variances est la simplicité d'utilisation car il suffit d'appliquer une formule, __MAIS__ :

* ces formules ne sont pas expliquées
* elles nécessitent des hypothèses restrictives qui ne sont pas toujours vérifiées. La méthode de Monte-Carlo demande moins d'hypothèse (dans le cadre du programme, l'indépendance des variables est suffisantes).

Le cas $Y=f(X)$ est notamment très souvent mis en défaut (notamment quand la dérivée s'annule au voisinage de $x_{mes}$ ou en $x_{mes}$.