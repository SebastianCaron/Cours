# Programmation Dynamique
> Adaptation du Mémo créé par @romain_wallon
## Principe

L'idée de cette approche est de mettre en cache les résultats déjà calculés
(dans un tableau ou une *map*, par exemple).
Deux approches existent, mais parfois seule l'une d'elles peut s'appliquer.
**ATTENTION : Garder des solutions en cache est coûteux en mémoire, et il
faut toujours vérifier que la taille du problème permet d'appliquer cette
approche.**

### Mémoïsation

C'est une approche *top-down* : on commence par le problème posé, puis on
descend jusqu'au(x) problème(s) de base.

```python
cache = {}
def fiboRecursifDynamique(n):
    if(n in cache.keys()):
        return cache[n]
    else:
        if(n < 2):
            return 1
        else:
            value = fiboRecursifDynamique(n-1) + fiboRecursifDynamique(n-2)
            cache[n] = value
            return value
```

### Tabulation

C'est une approche *bottom-up* : on commence par le problème de base, puis on
remonte jusqu'au problème posé.
```python
cache = {}
def fibonacci(n):
    if(n < 2):
        return 1
    cache[0] = 1
    cache[1] = 1
    for i in range(2,n):
        cache[i] = cache[i-1] + cache[i - 2]
    return cache[n]
```

## Problème du sac à dos

Il s'agit de choisir quels objets prendre parmi un ensemble d'objets de
différentes valeurs pour maximiser la valeur totale des objets choisis, tout
en faisant en sorte que le poids total des objets ne dépasse pas un poids
maximum fixé.
La fonction retourne la valeur optimale du sac à dos.

```python
def sacADos(poidsMax, poids, valeurs):
    nombre = len(poids)
    m = [range(0, nombre+1)][range(poidsMax + 1)]
    for i in range(nombre):
        for p in range(poidsMax):
            if((i == 0) or (p == 0)):
                m[i][p] = 0
            elif(poids[i - 1] <= p):
                m[i][p] = max(valeurs[i - 1] + m[i - 1][p - poids[i - 1]],m[i-1][p])
            else:
                m[i][p] = m[i - 1][p]
    return m[nombre][poidsMax]
```


