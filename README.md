# Générateur LaTeX3 de sujets pour des tournois de calcul

Ce document LaTeX3 permet de générer des sujets uniques pour les séances annuelles du tournoi de calcul du lycée. Ils se composent de 4 étapes de 10min chacune, et les qualifiés du premier tour participent au second tour dans la catégorie dans laquelle ils ont réussi.

Le générateur permet de composer des sujets pour chaque année. Pour cela, il suffit de jouer sur le paramètre suivant du préambule :

    \def\year{2027}

La valeur précédente correspond à l'année scolaire 2026-2027 (le tournoi ayant lieu en Mars pour la semaine des Mathématiques).

Afin de générer des sujets pour le premier ou le second tour, il suffit de changer le paramètre suivant dans le préambule :

    \def\tour{1} % valeur acceptée : 1 ou 2

Enfin, le générateur compile également les corrigés intégraux, afin de faciliter le travail de correction. Pour cela, il faut changer le booléen suivant :

    \setboolean{solution}{true} % valeur acceptée : true ou false

---

D'un point de vue plus technique, les sujets sont générés en utilisant notamment la macro `\int_rand:nn` de LaTeX3. Afin d'assurer la reproductibilité des sujets, la graine pour l'aléatoire est initialisée dans le préambule en concaténant le numéro du tour avec le numéro de l'année. Ainsi, pour les exemples ci-dessus, on a passé le nombre `12027` à la macro `\sys_gset_rand_seed:n`.

Afin de créer les corrigés, le générateur fait usage des macros `\numexpr` ou `\fpeval` lorsque c'est nécessaire. Les valeurs générées par les macros d'aléatoire sont stockées dans des token list temporaires, définies par `\xdef` (pour forcer l'expansion et obtenir une valeur aléatoire fixée au moment de la définition). Ces token list temporaires sont par conventions appelées `\@@a`, `\@@b`, etc.

La génération de fractions aléatoires irréductibles se fait  l'aide du package `xint`, et de l'instruction `\xinteval{reduce(...)}}`.
