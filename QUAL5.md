# QUAL5 

## 1. Complexité des algorithmes

Évaluer l’efficacité d’un algorithme selon :

* **Temps d’exécution** (complexité temporelle)
* **Mémoire utilisée** (complexité spatiale)

### Types de croissance

| Nom            | Notation   | Exemple                               | Interprétation                |
| -------------- | ---------- | ------------------------------------- | ----------------------------- |
| Constante      | O(1)       | accès à un élément d’un tableau       | indépendant de n              |
| Linéaire       | O(n)       | parcours d’une liste                  | proportionnel à n             |
| Quadratique    | O(n²)      | double boucle imbriquée               | chaque élément comparé à tous |
| Logarithmique  | O(log n)   | recherche dichotomique                | division du problème par 2    |
| Linéarithmique | O(n log n) | tri fusion                            | combinaison de tri + division |
| Exponentielle  | O(2ⁿ)      | récursivité non optimisée (Fibonacci) | explosion du coût             |

### Exemples

* Recherche du **plus grand diviseur commun** :

`O(n)` → itération simple

```python
# PGCD O(n) - Itération simple
def pgcd_on(a, b):
    for i in range(min(a, b), 0, -1):
        if a % i == 0 and b % i == 0:
            return i
    return 1
```

`O(√n)` → amélioration en limitant la recherche

```python
# PGCD O(√n) - Optimisé
def pgcd_osqrtn(a, b):
    import math
    pgcd = 1
    for i in range(1, int(math.sqrt(min(a, b))) + 1):
        if a % i == 0 and b % i == 0:
            pgcd = max(pgcd, i, a//i if b % (a//i) == 0 else 1)
    return pgcd
```

* Recherche **dichotomique** :

```python
def recherche_dicho(arr, x):
    """Recherche dichotomique avec compteur d'itérations"""
    left, right = 0, len(arr) - 1
    iterations = 0
        
    while left <= right:
        iterations += 1
        mid = (left + right) // 2
            
        if arr[mid] == x:
            return mid, iterations, "O(1)" if iterations == 1 else f"O(log n) - {iterations} iter"
        elif arr[mid] < x:
            left = mid + 1
        else:
            right = mid - 1
        
    return -1, iterations, f"Non trouvé - {iterations} iter"
```

* Algorithme de **Fibonacci** :

```python
# Complexité temporelle: O(n)
# Complexité spatiale: O(n)
@profile
def fiboIT(n):
    fib = [0 for p in range(0, n+1)]
    fib[0]=0;fib[1]=1
    for i in range(2,n+1):
        fib[i]=fib[i-1]+fib[i-2]
    return(fib)

# Complexité temporelle: O(n)
# Complexité spatiale: O(1)
@profile
def fiboIsT(n):
    a=0;b=1
    r=0
    for i in range(2,n+2):
        r=a+b
        b=a
        a=r
    return(r)
```

## 2. Récursivité

Une fonction **s’appelle elle-même** jusqu’à atteindre un **cas de base**.

* Cas de base (terminaison)
* Cas récursif (réduction du problème)

### 🔹 Types de récursivité

| Type              | Description                                  | Exemple                    |
| ----------------- | -------------------------------------------- | -------------------------- |
| **Terminale**     | L’appel récursif est la dernière instruction | Factorielle tail-recursive |
| **Non-terminale** | Calculs après l’appel récursif               | Factorielle classique      |

### Exemples

#### Factorielle

```python
def fact(n):
    if n <= 1:
        return 1
    else:
        return n * fact(n - 1)
```

* Non-terminale
* Complexité : O(n)

#### PGCD (Euclide)

```python
def pgcd(a, b):
    if b == 0:
        return a
    else:
        return pgcd(b, a % b)
```

* Complexité : O(log(min(a, b)))

#### Tri fusion (MergeSort)

* Diviser le tableau en deux sous-tableaux, trier récursivement, puis fusionner.
* Complexité : **O(n log n)**, espace : **O(n)**

```python
def tri_fusion(arr):
    """
    Tri fusion récursif - Complexité O(n log n)
    """
    # Cas de base
    if len(arr) <= 1:
        return arr
    
    # Diviser
    mid = len(arr) // 2
    gauche = tri_fusion(arr[:mid])
    droite = tri_fusion(arr[mid:])
    
    # Conquérir (fusionner)
    return fusionner(gauche, droite)

def fusionner(gauche, droite):
    """
    Fusionne deux listes triées en une liste triée
    """
    resultat = []
    i = j = 0
    
    # Fusionner élément par élément
    while i < len(gauche) and j < len(droite):
        if gauche[i] <= droite[j]:
            resultat.append(gauche[i])
            i += 1
        else:
            resultat.append(droite[j])
            j += 1
    
    # Ajouter les éléments restants
    resultat.extend(gauche[i:])
    resultat.extend(droite[j:])
    
    return resultat

tableau = [64, 34, 25, 12, 22, 11, 90]
tableau_trie = tri_fusion(tableau)
print(f"Tableau trié    : {tableau_trie}")
```

#### Courbe de Koch

* Exemple graphique de récursion sur segments.
* La complexité croît exponentiellement avec la profondeur.

```python
from turtle import *

def koch(l, n):
    if n <= 0:
        forward(l)
    else:
        koch(l / 3, n - 1)
        left(60)
        koch(l / 3, n - 1)
        right(120)
        koch(l / 3, n - 1)
        left(60)
        koch(l / 3, n - 1)

koch(100, 2)
done()
```

## 3. Graphes et arbres

### Graphe

Structure composée :

* **Sommets (nœuds)**
* **Arêtes (ou arcs)** reliant ces sommets

| Type                 | Description              |
| -------------------- | ------------------------ |
| Orienté              | arcs avec sens           |
| Non orienté          | arêtes sans direction    |
| Pondéré              | chaque arête a un poids  |
| Connexe              | tous les sommets reliés  |
| Cyclique / Acyclique | présence ou non de cycle |

### Parcours de graphes

#### Parcours en profondeur (DFS)

* **Principe :** visiter les sommets le plus loin possible avant de revenir en arrière.
* Implémentations : récursive / itérative (pile)
* Complexité : **O(V + E)**

```python
def dfs(s):
    s.marked = True
    for n in s.neighbors:
        if not n.marked:
            dfs(n)

def dfs_iter(s):
    s.marked = True
    stack = [s]
    while stack:
        c = stack.pop(len(stack) - 1)
        for n in c.neighbors:
            if not n.marked:
                n.marked = True
                stack.append(n)
```

#### Parcours en largeur (BFS)

* **Principe :** visiter les sommets par “niveau” à partir d’une racine.
* Implémentation : file (queue)
* Complexité : **O(V + E)**

```python
def bfs(s):
    s.marked = True
    queue = [s]
    while queue:
        c = queue.pop(0)
        for n in c.neighbors:
            if not n.marked:
                n.marked = True
                queue.append(n)
```

#### Applications

* Vérifier la connexité d’un graphe
    ```python
    def est_connexe(graphe):
        BFS(start) # Ou DFS
        for node in self.__nodes:
            if not node.isMarked():
                return False  
                
        # Le graphe est connexe si on a visité tous les sommets
        return True
    ```
* Trouver les distances minimales (BFS)
    ```python
    def distance_minimale(depart, arrivee):
        if depart == arrivee:
            return 0
        
        queue = [(depart, 0)]  # (sommet, distance)
         = {depart}
        
        while queue:
            sommet_actuel, distance = queue.pop(0)
            visites
            for voisin in sommet_actuel.voisins:
                if voisin == arrivee:
                    return distance + 1
                
                if voisin not in visites:
                    visites.add(voisin)
                    queue.append((voisin, distance + 1))
        
        return -1  # Pas de chemin trouvé
    ```
* Détecter un **cycle** (DFS)
    Pour un sommet donné:
    ```python
    def hasCycle(self, start, node):
        node.mark()
        for n in node.getSuccessors():
            if not n.isMarked():
                if self.hasCycle(start, n) is not None:
                    return True
            elif n.isMarked() and n.getName() == start.getName():
                return True
        return None
    ```
    Ou Sur tout le graphe:
    ```python
    def a_un_cycle(graphe):
        visites = set()
        en_cours = set()  # Sommets en cours de traitement
        
        def dfs(sommet):
            if sommet in en_cours:
                return True  # Cycle détecté !
            
            if sommet in visites:
                return False  # Déjà traité, pas de cycle ici
            
            visites.add(sommet)
            en_cours.add(sommet)
            
            # Visiter tous les voisins
            for voisin in sommet.voisins:
                if dfs(voisin):
                    return True
            
            en_cours.remove(sommet)  # Fini de traiter ce sommet
            return False
        
        # Tester tous les sommets (au cas où le graphe n'est pas connexe)
        for sommet in graphe.sommets:
            if sommet not in visites:
                if dfs(sommet):
                    return True
        
        return False
    ```

## 4. Arbres

### Définitions

* **Arbre** = graphe non orienté, **connexe** et **acyclique**.
* **Feuille** : nœud sans successeur
* **Nœud** : sommet avec enfants
* **Racine** : sommet sans prédécesseur

### Arbre binaire

* Chaque nœud a au plus deux enfants : **gauche** et **droit**.

#### Parcours

| Type     | Ordre de visite          | Exemple          |
| -------- | ------------------------ | ---------------- |
| Préfixé  | Racine – Gauche – Droite | pour copier      |
| Infixé   | Gauche – Racine – Droite | trié pour un ABR |
| Postfixé | Gauche – Droite – Racine | pour supprimer   |

### Arbre binaire de recherche (ABR)

#### Propriétés

* Pour tout nœud `p` :

  * Les clés du sous-arbre gauche < clé de `p`
  * Les clés du sous-arbre droit > clé de `p`

#### Opérations

| Opération           | Principe                                  | Complexité |
| ------------------- | ----------------------------------------- | ---------- |
| **Recherche**       | Descendre à gauche/droite selon la clé    | O(h)       |
| **Insertion**       | Identique à la recherche, ajout d’un nœud | O(h)       |
| **Suppression**     | Plusieurs cas selon le nombre de fils     | O(h)       |
| **Parcours infixé** | Donne les clés triées                     | O(n)       |

> `h` est la hauteur d'un arbre, soit le nombre maximum d'arêtes (ou de niveaux) entre la racine et une feuille.

#### Exemple complet de code d'arbre de recherche binaire:

```python
class Node:
    def __init__(self, key, father):
        self.__key = key
        self.__father = father
        self.__left = None
        self.__right = None
        self.__marked = False
        self.__depth = 0

    def mark(self):
        self.__marked = True

    def unmark(self):
        self.__marked = False
        if self.__left:
            self.__left.unmark()
        if self.__right:
            self.__right.unmark()

    def getKey(self):
        return self.__key

    def isMarked(self):
        return self.__marked

    def setFather(self, father):
        self.__father = father
        if father:
            self.__depth = father.getDepth() + 1
        else:
            self.__depth = 0

    ...

class BinaryTree:
    def __init__(self):
        self.__root = None
        self.add(Node(15))
        self.add(Node(6))
        self.add(Node(18))
        self.add(Node(3))
        self.add(Node(7))
        self.add(Node(17))
        self.add(Node(20))
        self.add(Node(2))
        self.add(Node(4))
        self.add(Node(13))
        self.add(Node(9))

    def add(self, node):
        if not self.__root:
            self.__root = node
        else:
            current = self.__root
            while True:
                if node.getKey() < current.getKey():
                    if current.getLeft() is None:
                        node.setFather(current)
                        current.setLeft(node)
                        break
                    else:
                        current = current.getLeft()
                else:
                    if current.getRight() is None:
                        vertex.setFather(current)
                        current.setRight(vertex)
                        break
                    else:
                        current = current.getRight()

    def find(self, key):
        current = self.__root
        while True:
            if key < current.getKey():
                if current.getLeft() is None:
                    return None
                else:
                    current = current.getLeft()
            if key > current.getKey():
                if current.getRight() is None:
                    return None
                else:
                    current = current.getRight()
            if key == current.getKey():
                return current

    def findFatherOf(self, key):
        node = self.find(key)
        if node is None:
            return None
        else:
            return node.getFather()

    def leafsAtDepth(self, depth):
        queue = [self.__root]
        leafs = 0
        while len(queue) > 0:
            current = queue.pop(0)
            if current.isMarked():
                continue
            current.mark()
            if current.getLeft():
                queue.append(current.getLeft())
            if current.getRight():
                queue.append(current.getRight())

            if current.getDepth() == depth and current.getLeft() is None and current.getRight() is None:
                leafs += 1
        return leafs

    def BFS(self):
        queue = [self.__root]
        while len(queue) > 0:
            current = queue.pop(0)
            if current.isMarked():
                continue
            current.mark()
            if current.getLeft():
                queue.append(current.getLeft())
            if current.getRight():
                queue.append(current.getRight())
```

## 5. Formules et ordres de grandeur

| Algorithme                | Complexité temporelle | Complexité spatiale |
| ------------------------- | --------------------- | ------------------- |
| Recherche linéaire        | O(n)                  | O(1)                |
| Recherche dichotomique    | O(log n)              | O(1)                |
| Tri fusion                | O(n log n)            | O(n)                |
| DFS / BFS                 | O(V + E)              | O(V)                |
| Insertion ABR             | O(h)                  | O(1)                |
| Fibonacci récursif simple | O(2ⁿ)                 | O(n)                |
| Fibonacci itératif        | O(n)                  | O(1)                |
