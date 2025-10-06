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
def koch_segments(x1, y1, x2, y2, profondeur):
    """
    Génère les segments de la courbe de Koch récursivement
    Complexité : O(4^profondeur) - croissance exponentielle
    
    Args:
        x1, y1: point de départ
        x2, y2: point d'arrivée
        profondeur: niveau de récursion (0 = segment simple)
    
    Returns:
        Liste de segments [(x1,y1,x2,y2), ...]
    """
    # Cas de base : segment simple
    if profondeur == 0:
        return [(x1, y1, x2, y2)]
    
    # Calcul des points intermédiaires
    dx = x2 - x1
    dy = y2 - y1
    
    # Premier tiers
    x_a = x1 + dx/3
    y_a = y1 + dy/3
    
    # Deuxième tiers
    x_b = x1 + 2*dx/3
    y_b = y1 + 2*dy/3
    
    # Sommet du triangle équilatéral
    import math
    x_c = (x_a + x_b)/2 - (y_b - y_a) * math.sqrt(3)/2
    y_c = (y_a + y_b)/2 + (x_b - x_a) * math.sqrt(3)/2
    
    # Récursion sur les 4 segments
    segments = []
    segments.extend(koch_segments(x1, y1, x_a, y_a, profondeur-1))
    segments.extend(koch_segments(x_a, y_a, x_c, y_c, profondeur-1))
    segments.extend(koch_segments(x_c, y_c, x_b, y_b, profondeur-1))
    segments.extend(koch_segments(x_b, y_b, x2, y2, profondeur-1))
    
    return segments

x1, y1 = 0, 0
x2, y2 = 300, 0
prof = 3  # Profondeur de récursion
segments = koch_segments(x1, y1, x2, y2, prof)
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
    ```
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
