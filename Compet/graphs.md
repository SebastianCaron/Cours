# Théorie des Graphes

## Classe Graphe


Cette classe utilise un dictionnaire pour stocker les sommets adjacents à un sommet ainsi que le poids de l'arrête qui les connecte.

```python
class Graphe:

    def __init__(self, o = False)-> None:
        """
        o -> orienté ?
        """
        self.adj = {}
        self.oriented = o
    
    def ajouterSommet(self, s):
        self.adj[s] = {}

    def ajouterArc(self, s1, s2, p = 1):
        self.adj[s1][s2] = p
        if self.oriented == False:
            self.adj[s2][s1] = p

    def supprArc(self, s1, s2):
        del(self.adj[s1][s2])

    def isArc(self, s1, s2):
        return s2 in self.adj[s1].keys()

    def sommets(self):
        return list(self.adj.keys())

    def voisins(self, s):
        return list(self.adj[s].keys())
```
> NB : Si aucun poids n'est spécifié, il sera de 1.

## Exemple :
<br>
<center>
    <img src = "https://doc.infoforall.fr/activite/snt/images/reseaux/graphes/graphe_non_oriente_1.png" width = '400'>
</center>
<br>

```python
# Initialise un Graph Non Orienté
graph = Graphe()

# On Ajoute les sommets
graph.ajouterSommet("A")
graph.ajouterSommet("B")
graph.ajouterSommet("C")
graph.ajouterSommet("D")
graph.ajouterSommet("E")
graph.ajouterSommet("F")
graph.ajouterSommet("G")

# On ajoute les Arretes

# A -> B & B -> A car graphe non orienté
graph.ajouterArc("A", "B")
graph.ajouterArc("A", "C")
graph.ajouterArc("A", "D")
graph.ajouterArc("B", "C")
graph.ajouterArc("B", "F")
graph.ajouterArc("D", "F")
graph.ajouterArc("D", "E")
graph.ajouterArc("E", "F")
graph.ajouterArc("E", "G")
graph.ajouterArc("F", "G")

# Pour Récuperer le poids d'une arrête :

# A -> B = 1
graph.adj["A"]["B"]
# B -> A = 1
graph.adj["A"]["B"]

# D -> G  : KeyError
graph.adj["A"]["G"]

# Voisins de G :
graph.voisins("G")  # ["E", "F"]
```

# Algorithme de Dijkstra
Cet algorithme détermine le coût du plus court chemin entre deux noeuds dans un
graphe.

```python
def dikjstra(g, d):
    sommets = g.sommets()

    sommetsExplores = {}
    distances = {}
    distances2 = {}
    parents = {}

    for s in sommets:
        sommetsExplores[s] = 0
        distances[s] = float("inf")
        distances2[s] = float("inf")
        parents[s] = None

    distances[d] = 0
    distances2[d] = 0

    e = d

    while(len(sommetsExplores) > 0):
        for v in g.voisins(e):
            k = g.adj[e][v] + distances[e]
            if(k < distances[v]):
                distances[v] = k
                distances2[v] = k
                parents[v] = e
        del(sommetsExplores[e])
        del(distances2[e])
        if len(sommetsExplores) != 0:
            e = min(distances2, key=distances2.get)
    return distances, parents
```
### Fonctionnement :
- Le dictionnaire sommetsExplores permet d'enregistrer quels sommets sont explorés ( 1 = exploré, defaut = 0). <br>
- On initialise toutes les distances à l'infini sauf pour le sommet de départ. <br>
- Tant qu'il y a des sommets a explorer, pour chaque voisin du sommet en cours, on met a jour le coût et son prédécesseur s'il est inférieur. On passe le sommet en cours à "exploré" ( = 1).<br>
- On creer un dictionnaire contenant les sommets restant a explorer. Le sommet avec la coût le plus faible devient le sommet en cours


## Afficher les Résultats :

```python
def cheminMin(g, d, a):
    distances, parents = dikjstra(g, d)

    chemin = []
    if distances[a] == float("inf"):
        return -1, []
    else:
        z = a
        while(z != None):
            chemin.insert(0, z)
            z = parents[z]
    return distances[a], chemin
```
### Fonctionnement :
- On récupere les résultats fournits par l'algorithme de Dijkstra.
- On creer une liste contenant le chemin entre les deux sommets.
- On récupere le parent du sommet d'arrivé, puis le parent du parent du sommet d'arrivé etc... Jusqu'a obtenir le sommet de départ. 
- On retourne la distance calculé pour le sommet d'arrivé et le chemin jusqu'a celui ci.
