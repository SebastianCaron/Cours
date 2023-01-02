# Divers
> Adaptation du Mémo créé par @romain_wallon & ajouts
## Recherche Dichotomique

Cette fonction recherche l'indice d'un élément dans un tableau trié par ordre
croissant en temps $`\mathcal{O}(\log(n))`$.
La valeur $'-1'$ est retournée si l'élément n'est pas présent.
Cet algorithme peut être facilement adapté pourvu que l'on dispose d'un ordre
sur les éléments à chercher.


```python
def binarySearch(array, left, right, elt):
    if(right >= left):
        middle = left + (right - left)//2
        if(array[middle] == elt):
            return middle
        if(elt < array[middle]):
            return binarySearch(array, left, middle-1, elt)
        return binarySearch(array, middle+1, right, elt)
    return -1

```

## Somme de Préfixes (Arbre de Fenwick)

Cette structure de données permet le calcul rapide de *sommes de préfixes* :
étant donnée une séquence de nombres $`x_1, ..., x_n`$, il s'agit de calculer
la séquence $`x_1, x_1 + x_2, ..., x_1 + ... + x_n`$.

```java
//JAVA
public class FenwickTree {
    int max;
    long[] tree;
    FenwickTree(int max) {
        this.max = Integer.highestOneBit(max) << 1;
        this.tree = new long[this.max];
    }
    void update(int x, long value) {
        for (; x < max; x += x & -x) tree[x] += value;
    }
    long read(int x) {
        long sum = 0;
        for (; x > 0; x -= x & -x) sum += tree[x];
        return sum;
    }
}
```

## Calcul de toutes les permutations possibles

À chaque appel à la fonction `computeNextPermutation`, une nouvelle permutation
des nombres entre `0` (inclus) et `size` (exclu) est calculée dans le tableau
`array`.
Notons que l'on peut utiliser cet algorithme pour calculer les permutations
de n'importe quelle séquence, en appliquant les permutations sur l'ensemble des
indices d'un tableau plutôt que sur ses éléments.

```python
array = []
size = 0

def computeNextPermutation():
    if(len(array) == 0):
        for i in range(size):
            array.append(i)
    fist = size - 1
    while(array[fist - 1] >= array[fist]):
        first -= 1
    second = size
    while(array[second - 1] <= array[first - 1]):
        second -= 1
    array[first -1], array[second - 1] = array[second - 1], array[first - 1]
    first += 1
    second = size
    while(first < second):
        array[first -1], array[second - 1] = array[second - 1], array[first - 1]
        first += 1
        second -= 1

```

