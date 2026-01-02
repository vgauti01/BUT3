# Notions Jetpack Compose - MyCampusTasks

Ce document résume de manière exhaustive les concepts clés de Jetpack Compose et de l'architecture Android moderne appris lors du développement de l'application MyCampusTasks.

---

## Fichiers du Projet

### Structure principale
- [`MainActivity.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MainActivity.kt) - Point d'entrée de l'application
- [`MyCampusTasksApp.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MyCampusTasksApp.kt) - Composable racine et TopAppBar
- [`MyCampusTasksApplication.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MyCampusTasksApplication.kt) - Singleton Application

### UI - Écrans et Composants
- [`ui/home/HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - Écran principal
- [`ui/task/TaskInput.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskInput.kt) - Formulaire de saisie
- [`ui/task/TaskItem.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskItem.kt) - Élément de liste
- [`ui/task/TaskList.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskList.kt) - Liste des tâches
- [`ui/task/TaskSwitch.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskSwitch.kt) - Switch online/offline

### UI - Navigation
- [`ui/navigation/NavigationDestination.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/NavigationDestination.kt) - Interface de destination
- [`ui/navigation/TaskNavigationDestination.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/TaskNavigationDestination.kt) - Destinations concrètes
- [`ui/navigation/TaskNavigationGraph.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/TaskNavigationGraph.kt) - Configuration NavHost

### UI - Thème
- [`ui/theme/Theme.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/theme/Theme.kt) - Thème Material3
- [`ui/theme/Color.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/theme/Color.kt) - Palette de couleurs
- [`ui/theme/Type.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/theme/Type.kt) - Typographie
- [`ui/theme/Shape.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/theme/Shape.kt) - Formes

### ViewModel
- [`viewmodel/TaskViewModel.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModel.kt) - Logique métier
- [`viewmodel/TaskViewModelFactory.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModelFactory.kt) - Factory pour injection

### Model - Données
- [`model/Task.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/Task.kt) - Entité Task (Room)
- [`model/TaskDao.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TaskDao.kt) - Data Access Object
- [`model/TaskDatabase.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TaskDatabase.kt) - Base de données Room
- [`model/DateTypeConverter.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/DateTypeConverter.kt) - Convertisseur Date

### Model - Repository
- [`model/TasksRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TasksRepository.kt) - Interface Repository
- [`model/OfflineTasksRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/OfflineTasksRepository.kt) - Implémentation Room
- [`model/OnlineTaskRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/OnlineTaskRepository.kt) - Implémentation API

### Model - API
- [`model/api/TaskApiService.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/api/TaskApiService.kt) - Interface Retrofit
- [`model/api/TaskDto.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/api/TaskDto.kt) - Data Transfer Objects
- [`model/api/RetrofitClient.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/api/RetrofitClient.kt) - Configuration HTTP

### Configuration
- [`AndroidManifest.xml`](app/src/main/AndroidManifest.xml) - Manifest Android
- [`build.gradle.kts`](app/build.gradle.kts) - Configuration Gradle (app)
- [`gradle/libs.versions.toml`](gradle/libs.versions.toml) - Versions des dépendances

---

## Table des Matières

1. [Composables - Les Briques de Base](#1-composables---les-briques-de-base)
2. [State et MutableState - La Gestion de l'État](#2-state-et-mutablestate---la-gestion-de-létat)
3. [API remember - La Mémorisation](#3-api-remember---la-mémorisation)
4. [rememberSaveable - Persistance de l'État](#4-remembersaveable---persistance-de-létat)
5. [Activity et Cycle de Vie](#5-activity-et-cycle-de-vie)
6. [Scaffold - Structure d'Écran](#6-scaffold---structure-décran)
7. [TopAppBar - Barre d'Application](#7-topappbar---barre-dapplication)
8. [Modifier - Configuration des Composables](#8-modifier---configuration-des-composables)
9. [Layouts - Column, Row, Box](#9-layouts---column-row-box)
10. [Composants Material3](#10-composants-material3)
11. [Flux de Données Unidirectionnel](#11-flux-de-données-unidirectionnel)
12. [ViewModel - Gestion de la Logique Métier](#12-viewmodel---gestion-de-la-logique-métier)
13. [StateFlow et MutableStateFlow](#13-stateflow-et-mutablestateflow)
14. [collectAsState - Pont entre Flow et Compose](#14-collectasstate---pont-entre-flow-et-compose)
15. [ViewModelFactory - Injection de Dépendances](#15-viewmodelfactory---injection-de-dépendances)
16. [Coroutines et viewModelScope](#16-coroutines-et-viewmodelscope)
17. [Navigation Compose](#17-navigation-compose)
18. [LocalContext et CompositionLocal](#18-localcontext-et-compositionlocal)
19. [Room Database - Persistance Locale](#19-room-database---persistance-locale)
20. [TypeConverter - Conversion de Types](#20-typeconverter---conversion-de-types)
21. [Migrations Room](#21-migrations-room)
22. [Repository Pattern](#22-repository-pattern)
23. [Application Singleton](#23-application-singleton)
24. [Retrofit - Appels Réseau](#24-retrofit---appels-réseau)
25. [Patterns Architecturaux](#25-patterns-architecturaux)

---

## 1. Composables - Les Briques de Base

### Qu'est-ce qu'un Composable ?

Un **Composable** est une fonction Kotlin annotée avec `@Composable` qui décrit une partie de l'interface utilisateur. C'est le concept fondamental de Jetpack Compose, le framework UI déclaratif d'Android.

```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello $name!")
}
```

### Paradigme Déclaratif vs Impératif

**Approche impérative (ancienne méthode avec XML) :**
```kotlin
// On dit COMMENT faire
val textView = findViewById<TextView>(R.id.textView)
textView.text = "Hello"
textView.setTextColor(Color.RED)
textView.visibility = View.VISIBLE
```

**Approche déclarative (Jetpack Compose) :**
```kotlin
// On dit CE QU'ON VEUT
@Composable
fun Greeting(name: String, isVisible: Boolean) {
    if (isVisible) {
        Text(
            text = "Hello $name!",
            color = Color.Red
        )
    }
}
```

Avec l'approche déclarative, on décrit l'état final souhaité de l'UI. Compose se charge de déterminer comment passer de l'état actuel à l'état désiré.

### Composition et Imbrication

Les composables peuvent s'imbriquer pour former des interfaces complexes :

```kotlin
@Composable
fun UserCard(user: User) {
    Card {                              // Composable Card
        Column {                        // Composable Column
            UserAvatar(user.avatarUrl)  // Composable personnalisé
            Text(user.name)             // Composable Text
            Text(user.email)            // Composable Text
        }
    }
}
```

### La Recomposition

La **recomposition** est le processus par lequel Compose ré-exécute les fonctions composables lorsque leurs entrées (paramètres ou état) changent.

```kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }

    // Ce bloc est recomposé à chaque changement de 'count'
    Column {
        Text("Count: $count")  // Recomposé quand count change
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

**Points importants sur la recomposition :**
- Compose est intelligent : il ne recompose que les parties qui ont changé
- Les composables doivent être **idempotents** : appelés plusieurs fois avec les mêmes paramètres, ils produisent le même résultat
- Les composables ne doivent pas avoir d'effets de bord (pas d'écriture dans des variables globales, pas d'appels réseau directs)

### Conventions de Nommage

- Les fonctions composables commencent par une **majuscule** : `HomeScreen`, `TaskItem`, `UserAvatar`
- Elles sont nommées comme des noms (pas des verbes) car elles décrivent "ce qui est affiché"
- Les paramètres de type fonction (callbacks) commencent par `on` : `onClick`, `onValueChange`, `onTaskAdded`

> **Voir dans le projet :**
> - [`MyCampusTasksApp.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MyCampusTasksApp.kt) - Composable racine
> - [`HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - Exemple de composable écran
> - [`TaskItem.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskItem.kt) - Exemple de composable réutilisable

---

## 2. State et MutableState - La Gestion de l'État

### Le Problème : État Non Observable

Dans une fonction normale, une variable locale est réinitialisée à chaque appel :

```kotlin
@Composable
fun BrokenCounter() {
    var count = 0  // Réinitialisé à 0 à chaque recomposition !

    Button(onClick = { count++ }) {  // count++ n'a aucun effet visible
        Text("Count: $count")        // Affiche toujours 0
    }
}
```

Problèmes :
1. La variable `count` est recréée à chaque recomposition
2. Même si on incrémente `count`, Compose ne sait pas qu'il doit recomposer

### La Solution : MutableState

`MutableState<T>` est un type spécial qui :
1. **Conserve** sa valeur entre les recompositions (quand combiné avec `remember`)
2. **Notifie** Compose quand sa valeur change, déclenchant une recomposition

```kotlin
@Composable
fun WorkingCounter() {
    // mutableStateOf crée un conteneur observable pour la valeur 0
    var count by remember { mutableStateOf(0) }

    Button(onClick = { count++ }) {  // Modifie la valeur ET déclenche une recomposition
        Text("Count: $count")        // Affiche la valeur mise à jour
    }
}
```

### State vs MutableState

```kotlin
// State<T> - Lecture seule
val readOnlyState: State<Int> = mutableStateOf(0)
val value = readOnlyState.value  // OK
// readOnlyState.value = 5       // ERREUR : pas de setter

// MutableState<T> - Lecture et écriture
val mutableState: MutableState<Int> = mutableStateOf(0)
val value = mutableState.value   // OK
mutableState.value = 5           // OK
```

### Syntaxe avec Délégation (`by`)

Kotlin permet d'utiliser la délégation de propriété pour simplifier l'accès :

```kotlin
// Sans délégation - syntaxe verbeuse
val counterState = remember { mutableStateOf(0) }
Text("Count: ${counterState.value}")
counterState.value = counterState.value + 1

// Avec délégation - syntaxe simplifiée
var counter by remember { mutableStateOf(0) }
Text("Count: $counter")
counter = counter + 1  // ou counter++
```

**Imports requis pour la délégation :**
```kotlin
import androidx.compose.runtime.getValue
import androidx.compose.runtime.setValue
```

Ces imports fournissent les opérateurs `getValue` et `setValue` qui permettent à Kotlin de déléguer les accès en lecture/écriture à l'objet `MutableState`.

### Types d'État Courants

```kotlin
// État simple
var isLoading by remember { mutableStateOf(false) }
var userName by remember { mutableStateOf("") }
var selectedIndex by remember { mutableStateOf(0) }

// État nullable
var selectedItem by remember { mutableStateOf<Item?>(null) }

// État avec liste (attention : voir mutableStateListOf pour les listes mutables)
var items by remember { mutableStateOf(listOf<String>()) }
// Pour modifier : items = items + "nouveau"  (crée une nouvelle liste)
```

> **Voir dans le projet :**
> - [`TaskInput.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskInput.kt) - Utilisation de `remember` et `mutableStateOf` pour les états du formulaire

---

## 3. API remember - La Mémorisation

### Le Problème Sans remember

Sans `remember`, même un `MutableState` serait recréé à chaque recomposition :

```kotlin
@Composable
fun BrokenWithState() {
    // PROBLÈME : un NOUVEAU MutableState est créé à chaque recomposition
    var count = mutableStateOf(0)
    // Même si on modifie count.value, la recomposition crée un nouveau MutableState(0)
}
```

### Comment remember Fonctionne

`remember` stocke une valeur dans la **composition** (l'arbre d'UI interne de Compose). Cette valeur persiste tant que le composable reste dans l'arbre.

```kotlin
@Composable
fun RememberExample() {
    // La lambda { mutableStateOf(0) } n'est exécutée qu'une seule fois
    // lors de la première composition
    var count by remember { mutableStateOf(0) }

    // Lors des recompositions suivantes, remember retourne
    // la même instance de MutableState
}
```

### Cycle de Vie de remember

```
Première composition :
  → remember exécute la lambda { mutableStateOf(0) }
  → Stocke le résultat dans la composition
  → Retourne la valeur (MutableState avec value = 0)

Recompositions suivantes :
  → remember retrouve la valeur stockée
  → Retourne la même instance (pas d'exécution de la lambda)

Sortie de la composition (composable retiré de l'écran) :
  → La valeur stockée est supprimée
  → Si le composable réapparaît, remember exécutera à nouveau la lambda
```

### remember avec Clés

On peut forcer `remember` à recalculer sa valeur quand certaines dépendances changent :

```kotlin
@Composable
fun FilteredList(filter: String, items: List<Item>) {
    // Recalculé uniquement quand 'filter' ou 'items' change
    val filteredItems = remember(filter, items) {
        items.filter { it.name.contains(filter) }
    }
}
```

### Cas d'Utilisation Courants

```kotlin
// 1. État local d'un composable
var isExpanded by remember { mutableStateOf(false) }

// 2. Calculs coûteux à mettre en cache
val sortedList = remember(unsortedList) {
    unsortedList.sortedBy { it.name }  // Trié une seule fois par liste
}

// 3. Objets qui ne doivent pas être recréés
val dateFormatter = remember {
    SimpleDateFormat("dd/MM/yyyy", Locale.getDefault())
}

// 4. Lambdas capturant des valeurs
val callback = remember(id) {
    { doSomethingWith(id) }
}
```

---

## 4. rememberSaveable - Persistance de l'État

### Le Problème : Changements de Configuration

Quand l'utilisateur fait pivoter son téléphone, Android détruit et recrée l'activité. Avec `remember`, l'état est perdu :

```kotlin
@Composable
fun LostOnRotation() {
    // PROBLÈME : perdu lors de la rotation de l'écran
    var text by remember { mutableStateOf("Mon texte") }
}
```

### La Solution : rememberSaveable

`rememberSaveable` utilise le mécanisme de sauvegarde d'état d'Android (`SavedInstanceState`) pour persister la valeur :

```kotlin
@Composable
fun SurvivedRotation() {
    // Survit à la rotation et autres changements de configuration
    var text by rememberSaveable { mutableStateOf("Mon texte") }
}
```

### Ce que rememberSaveable Sauvegarde

Par défaut, `rememberSaveable` peut sauvegarder automatiquement :
- Types primitifs : `Int`, `Long`, `Float`, `Double`, `Boolean`, `Char`, `Byte`, `Short`
- `String`
- `Bundle`
- `Parcelable` (si la classe implémente `Parcelable`)
- `Serializable`

```kotlin
// Fonctionne directement
var count by rememberSaveable { mutableStateOf(0) }
var name by rememberSaveable { mutableStateOf("") }
var isEnabled by rememberSaveable { mutableStateOf(true) }
```

### Types Personnalisés avec Saver

Pour des types complexes, on utilise un `Saver` :

```kotlin
data class UserSelection(
    val category: String,
    val sortOrder: SortOrder
)

val UserSelectionSaver = Saver<UserSelection, Bundle>(
    save = { selection ->
        Bundle().apply {
            putString("category", selection.category)
            putString("sortOrder", selection.sortOrder.name)
        }
    },
    restore = { bundle ->
        UserSelection(
            category = bundle.getString("category") ?: "",
            sortOrder = SortOrder.valueOf(bundle.getString("sortOrder") ?: "ASC")
        )
    }
)

@Composable
fun UserPreferences() {
    var selection by rememberSaveable(stateSaver = UserSelectionSaver) {
        mutableStateOf(UserSelection("All", SortOrder.ASC))
    }
}
```

### remember vs rememberSaveable

| Aspect | `remember` | `rememberSaveable` |
|--------|------------|-------------------|
| Survit aux recompositions | Oui | Oui |
| Survit aux changements de configuration | Non | Oui |
| Survit à la mort du processus | Non | Oui (si l'app est restaurée) |
| Performance | Plus rapide | Légèrement plus lent |
| Types supportés | Tous | Types sérialisables |

**Règle générale :**
- Utilisez `remember` pour l'état temporaire (animations, états d'UI locaux)
- Utilisez `rememberSaveable` pour l'état utilisateur important (texte saisi, sélections)

> **Voir dans le projet :**
> - [`TaskItem.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskItem.kt) - Utilisation de `remember` pour l'état d'expansion

---

## 5. Activity et Cycle de Vie

### Qu'est-ce qu'une Activity ?

Une **Activity** est un composant fondamental d'Android qui représente un écran avec lequel l'utilisateur peut interagir. Dans les applications Compose, l'Activity sert de **conteneur** pour l'UI Compose.

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // setContent définit le contenu Compose de l'Activity
        setContent {
            // Le thème Material englobe toute l'application
            MyCampusTasksTheme {
                // Point d'entrée de l'UI Compose
                MyCampusTasksApp()
            }
        }
    }
}
```

### ComponentActivity vs AppCompatActivity

- `ComponentActivity` : Classe de base minimale pour Compose, recommandée pour les nouvelles apps
- `AppCompatActivity` : Hérite de `ComponentActivity`, ajoute la compatibilité avec les anciennes versions d'Android et les composants XML

### Le Cycle de Vie en Détail

```
                    ┌─────────────────┐
                    │   onCreate()    │ ← Activity créée, UI initialisée
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │    onStart()    │ ← Activity visible mais pas interactive
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
         ┌─────────►│   onResume()    │ ← Activity au premier plan, interactive
         │          └────────┬────────┘
         │                   │
         │          ┌────────▼────────┐
         │          │    onPause()    │ ← Activity partiellement masquée
         │          └────────┬────────┘
         │                   │
         │          ┌────────▼────────┐
         │          │    onStop()     │ ← Activity complètement cachée
         │          └────────┬────────┘
         │                   │
    onRestart()     ┌────────▼────────┐
         │          │   onDestroy()   │ ← Activity détruite
         │          └─────────────────┘
         │                   │
         └───────────────────┘
```

### Détail de Chaque Callback

**`onCreate(savedInstanceState: Bundle?)`**
- Appelée une seule fois lors de la création de l'Activity
- C'est ici qu'on initialise l'UI avec `setContent {}`
- `savedInstanceState` contient l'état sauvegardé si l'Activity est recréée

**`onStart()`**
- L'Activity devient visible à l'utilisateur
- L'UI est dessinée mais l'utilisateur ne peut pas encore interagir

**`onResume()`**
- L'Activity est au premier plan et prête à recevoir les interactions
- C'est l'état "normal" d'une app en cours d'utilisation

**`onPause()`**
- Une autre Activity passe au premier plan (dialogue, autre app en multi-window)
- L'Activity reste partiellement visible
- Sauvegarder les données importantes ici

**`onStop()`**
- L'Activity n'est plus visible (retour home, autre app lancée)
- Libérer les ressources lourdes ici

**`onDestroy()`**
- L'Activity va être détruite (finish() appelé ou système a besoin de mémoire)
- Nettoyer toutes les ressources

**`onRestart()`**
- Appelée quand l'Activity revient de l'état stoppé
- Précède toujours `onStart()`

### Scénarios Courants

```kotlin
// Démarrage de l'app
onCreate() → onStart() → onResume()

// Appui sur Home
onPause() → onStop()

// Retour à l'app
onRestart() → onStart() → onResume()

// Rotation de l'écran (changement de configuration)
onPause() → onStop() → onDestroy() → onCreate() → onStart() → onResume()

// Fermeture de l'app (bouton retour depuis l'écran principal)
onPause() → onStop() → onDestroy()
```

### Observer le Cycle de Vie dans Compose

```kotlin
@Composable
fun LifecycleAwareComponent() {
    val lifecycleOwner = LocalLifecycleOwner.current

    DisposableEffect(lifecycleOwner) {
        val observer = LifecycleEventObserver { _, event ->
            when (event) {
                Lifecycle.Event.ON_RESUME -> {
                    // L'écran est visible et actif
                }
                Lifecycle.Event.ON_PAUSE -> {
                    // L'écran va être masqué
                }
                else -> {}
            }
        }

        lifecycleOwner.lifecycle.addObserver(observer)

        onDispose {
            lifecycleOwner.lifecycle.removeObserver(observer)
        }
    }
}
```

> **Voir dans le projet :**
> - [`MainActivity.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MainActivity.kt) - Activity principale avec `setContent`

---

## 6. Scaffold - Structure d'Écran

### Qu'est-ce que Scaffold ?

`Scaffold` est un composable qui implémente la structure visuelle de base de Material Design. Il fournit des emplacements ("slots") pour les éléments d'UI courants.

```kotlin
@Composable
fun MyScreen() {
    Scaffold(
        topBar = { /* Barre d'app en haut */ },
        bottomBar = { /* Barre de navigation en bas */ },
        floatingActionButton = { /* Bouton flottant */ },
        snackbarHost = { /* Conteneur pour les Snackbars */ },
        containerColor = MaterialTheme.colorScheme.background
    ) { innerPadding ->
        // Contenu principal
        // innerPadding évite que le contenu soit caché sous les barres
        Content(modifier = Modifier.padding(innerPadding))
    }
}
```

### Les Slots de Scaffold

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun CompleteScaffoldExample() {
    val snackbarHostState = remember { SnackbarHostState() }

    Scaffold(
        // 1. Barre d'application en haut
        topBar = {
            TopAppBar(
                title = { Text("Mon Application") },
                navigationIcon = {
                    IconButton(onClick = { /* Retour */ }) {
                        Icon(Icons.Default.ArrowBack, "Retour")
                    }
                },
                actions = {
                    IconButton(onClick = { /* Recherche */ }) {
                        Icon(Icons.Default.Search, "Rechercher")
                    }
                }
            )
        },

        // 2. Barre de navigation en bas
        bottomBar = {
            NavigationBar {
                NavigationBarItem(
                    selected = true,
                    onClick = { },
                    icon = { Icon(Icons.Default.Home, "Accueil") },
                    label = { Text("Accueil") }
                )
                NavigationBarItem(
                    selected = false,
                    onClick = { },
                    icon = { Icon(Icons.Default.Settings, "Paramètres") },
                    label = { Text("Paramètres") }
                )
            }
        },

        // 3. Bouton d'action flottant
        floatingActionButton = {
            FloatingActionButton(
                onClick = { /* Ajouter */ },
                containerColor = MaterialTheme.colorScheme.primary
            ) {
                Icon(Icons.Default.Add, "Ajouter")
            }
        },

        // 4. Position du FAB
        floatingActionButtonPosition = FabPosition.End,

        // 5. Conteneur pour les Snackbars
        snackbarHost = { SnackbarHost(snackbarHostState) },

        // 6. Couleur de fond
        containerColor = MaterialTheme.colorScheme.background,

        // 7. Couleur du contenu (texte, icônes par défaut)
        contentColor = MaterialTheme.colorScheme.onBackground

    ) { paddingValues ->
        // 8. Contenu principal avec le padding nécessaire
        LazyColumn(
            modifier = Modifier
                .fillMaxSize()
                .padding(paddingValues)  // IMPORTANT : évite le chevauchement
        ) {
            items(100) { index ->
                Text("Item $index", modifier = Modifier.padding(16.dp))
            }
        }
    }
}
```

### L'Importance de innerPadding

Le `innerPadding` (ou `paddingValues`) fourni par Scaffold est crucial :

```kotlin
Scaffold(
    topBar = { TopAppBar(title = { Text("Titre") }) }  // Hauteur ~64dp
) { innerPadding ->
    // Sans padding : le contenu serait caché sous la TopAppBar
    // innerPadding.calculateTopPadding() ≈ 64.dp

    Column(modifier = Modifier.padding(innerPadding)) {
        Text("Ce texte n'est pas caché sous la barre")
    }
}
```

### Scaffold avec Scroll Behavior

Pour que la TopAppBar réagisse au défilement :

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun ScrollableScaffold() {
    val scrollBehavior = TopAppBarDefaults.enterAlwaysScrollBehavior()

    Scaffold(
        modifier = Modifier.nestedScroll(scrollBehavior.nestedScrollConnection),
        topBar = {
            TopAppBar(
                title = { Text("Titre") },
                scrollBehavior = scrollBehavior  // La barre réagit au scroll
            )
        }
    ) { innerPadding ->
        LazyColumn(modifier = Modifier.padding(innerPadding)) {
            items(100) { Text("Item $it") }
        }
    }
}
```

> **Voir dans le projet :**
> - [`HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - Scaffold avec topBar et floatingActionButton

---

## 7. TopAppBar - Barre d'Application

### Types de TopAppBar

Material3 propose plusieurs variantes :

```kotlin
// 1. TopAppBar simple - Titre à gauche
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun SimpleTopAppBar() {
    TopAppBar(
        title = { Text("Titre") }
    )
}

// 2. CenterAlignedTopAppBar - Titre centré
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun CenteredTopAppBar() {
    CenterAlignedTopAppBar(
        title = { Text("Titre Centré") }
    )
}

// 3. MediumTopAppBar - Plus grande, titre en bas
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MediumTopAppBar() {
    MediumTopAppBar(
        title = { Text("Titre Medium") }
    )
}

// 4. LargeTopAppBar - Encore plus grande
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun LargeTopAppBar() {
    LargeTopAppBar(
        title = { Text("Titre Large") }
    )
}
```

### Anatomie d'une TopAppBar

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun CompleteTopAppBar() {
    TopAppBar(
        // 1. Titre principal
        title = {
            Text(
                text = "Mon Application",
                maxLines = 1,
                overflow = TextOverflow.Ellipsis
            )
        },

        // 2. Icône de navigation (gauche) - retour, menu hamburger
        navigationIcon = {
            IconButton(onClick = { /* Navigation */ }) {
                Icon(
                    imageVector = Icons.Default.Menu,
                    contentDescription = "Menu"
                )
            }
        },

        // 3. Actions (droite) - recherche, paramètres, etc.
        actions = {
            IconButton(onClick = { /* Recherche */ }) {
                Icon(Icons.Default.Search, "Rechercher")
            }
            IconButton(onClick = { /* Plus */ }) {
                Icon(Icons.Default.MoreVert, "Plus d'options")
            }
        },

        // 4. Couleurs personnalisées
        colors = TopAppBarDefaults.topAppBarColors(
            containerColor = MaterialTheme.colorScheme.primaryContainer,
            titleContentColor = MaterialTheme.colorScheme.onPrimaryContainer,
            navigationIconContentColor = MaterialTheme.colorScheme.onPrimaryContainer,
            actionIconContentColor = MaterialTheme.colorScheme.onPrimaryContainer
        ),

        // 5. Comportement au scroll
        scrollBehavior = TopAppBarDefaults.pinnedScrollBehavior()
    )
}
```

### Comportements au Scroll (ScrollBehavior)

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun ScrollBehaviorExamples() {
    // 1. pinnedScrollBehavior - La barre reste toujours visible
    val pinned = TopAppBarDefaults.pinnedScrollBehavior()

    // 2. enterAlwaysScrollBehavior - Se cache au scroll down, réapparaît immédiatement au scroll up
    val enterAlways = TopAppBarDefaults.enterAlwaysScrollBehavior()

    // 3. exitUntilCollapsedScrollBehavior - Se réduit mais ne disparaît pas complètement
    val exitUntilCollapsed = TopAppBarDefaults.exitUntilCollapsedScrollBehavior()
}
```

### Implémentation dans MyCampusTasks

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MyCampusTasksTopAppBar(
    title: String,
    modifier: Modifier = Modifier,
    scrollBehavior: TopAppBarScrollBehavior? = null,
    canNavigateBack: Boolean = false,
    navigateUp: () -> Unit = {}
) {
    CenterAlignedTopAppBar(
        title = { Text(title) },
        modifier = modifier,
        scrollBehavior = scrollBehavior,
        navigationIcon = {
            if (canNavigateBack) {
                IconButton(onClick = navigateUp) {
                    Icon(
                        imageVector = Icons.Filled.ArrowBack,
                        contentDescription = stringResource(R.string.back)
                    )
                }
            }
        }
    )
}
```

### Annotation @OptIn

`@OptIn(ExperimentalMaterial3Api::class)` est nécessaire car certaines API de Material3 sont encore expérimentales. Cela signifie :
- L'API peut changer dans les versions futures
- On accepte consciemment ce risque en utilisant `@OptIn`

> **Voir dans le projet :**
> - [`MyCampusTasksApp.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MyCampusTasksApp.kt) - `MyCampusTasksTopAppBar` avec CenterAlignedTopAppBar
> - [`HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - TopAppBar avec scrollBehavior

---

## 8. Modifier - Configuration des Composables

### Qu'est-ce qu'un Modifier ?

Un `Modifier` est un objet immuable qui permet de :
- Définir la taille et la position d'un composable
- Ajouter du padding, des marges
- Gérer les interactions (clics, focus)
- Appliquer des effets visuels (couleurs, formes, ombres)
- Et bien plus...

```kotlin
Text(
    text = "Hello",
    modifier = Modifier
        .fillMaxWidth()           // Prend toute la largeur
        .padding(16.dp)           // Padding de 16dp
        .background(Color.Blue)   // Fond bleu
        .clickable { }            // Réagit aux clics
)
```

### L'Ordre des Modifiers Est Important !

Les modifiers s'appliquent de l'extérieur vers l'intérieur (comme des couches d'oignon) :

```kotlin
// Exemple 1 : padding PUIS background
Text(
    text = "A",
    modifier = Modifier
        .padding(16.dp)        // 1. Ajoute 16dp d'espace autour
        .background(Color.Red) // 2. Le fond rouge est DANS le padding
)
// Résultat : texte sur fond rouge, avec espace transparent autour

// Exemple 2 : background PUIS padding
Text(
    text = "B",
    modifier = Modifier
        .background(Color.Red) // 1. Fond rouge sur tout l'espace
        .padding(16.dp)        // 2. Le padding est DANS le fond rouge
)
// Résultat : texte avec fond rouge qui inclut le padding
```

### Modifiers de Taille

```kotlin
Modifier
    // Taille fixe
    .size(100.dp)                    // Largeur ET hauteur = 100dp
    .width(200.dp)                   // Largeur = 200dp
    .height(50.dp)                   // Hauteur = 50dp

    // Taille relative au parent
    .fillMaxSize()                   // 100% largeur ET hauteur
    .fillMaxWidth()                  // 100% largeur
    .fillMaxHeight()                 // 100% hauteur
    .fillMaxWidth(0.5f)              // 50% de la largeur

    // Contraintes
    .wrapContentSize()               // Taille minimale pour le contenu
    .sizeIn(minWidth = 50.dp, maxWidth = 200.dp)

    // Ratio d'aspect
    .aspectRatio(16f / 9f)           // Ratio 16:9
```

### Modifiers d'Espacement

```kotlin
Modifier
    // Padding (espace intérieur)
    .padding(16.dp)                          // Tous les côtés
    .padding(horizontal = 16.dp, vertical = 8.dp)
    .padding(start = 8.dp, end = 16.dp, top = 4.dp, bottom = 4.dp)

    // Offset (décalage de position)
    .offset(x = 10.dp, y = 5.dp)
```

### Modifiers Visuels

```kotlin
Modifier
    // Couleur de fond
    .background(Color.Blue)
    .background(Color.Blue, shape = RoundedCornerShape(8.dp))

    // Bordure
    .border(2.dp, Color.Black)
    .border(2.dp, Color.Black, RoundedCornerShape(8.dp))

    // Forme (clip)
    .clip(RoundedCornerShape(16.dp))
    .clip(CircleShape)

    // Ombre
    .shadow(elevation = 4.dp, shape = RoundedCornerShape(8.dp))

    // Transparence
    .alpha(0.5f)
```

### Modifiers d'Interaction

```kotlin
Modifier
    // Clic
    .clickable { /* Action au clic */ }
    .clickable(
        enabled = isEnabled,
        onClick = { }
    )

    // Clic avec effet ripple personnalisé
    .clickable(
        interactionSource = remember { MutableInteractionSource() },
        indication = rememberRipple(bounded = true, color = Color.Blue),
        onClick = { }
    )

    // Scroll
    .verticalScroll(rememberScrollState())
    .horizontalScroll(rememberScrollState())

    // Focus
    .focusable()
```

### Modifiers de Layout

```kotlin
Modifier
    // Alignement dans le parent (pour Box, Row, Column)
    .align(Alignment.Center)           // Dans Box
    .align(Alignment.CenterVertically) // Dans Row
    .align(Alignment.CenterHorizontally) // Dans Column

    // Poids (pour Row, Column)
    .weight(1f)    // Prend l'espace restant proportionnellement
    .weight(2f)    // Prend 2x plus d'espace que weight(1f)
```

### LazyColumn et LazyRow - Listes Performantes

Pour les longues listes, utilisez `LazyColumn` ou `LazyRow` qui ne composent que les éléments visibles :

```kotlin
LazyColumn(
    modifier = Modifier.fillMaxSize(),
    contentPadding = PaddingValues(16.dp),  // Padding du contenu
    verticalArrangement = Arrangement.spacedBy(8.dp)  // Espace entre items
) {
    // Un seul élément
    item {
        Text("En-tête")
    }

    // Liste d'éléments
    items(tasks) { task ->
        TaskItem(task = task)
    }

    // Liste avec index
    itemsIndexed(tasks) { index, task ->
        TaskItem(task = task, position = index)
    }
}
```

> **Voir dans le projet :**
> - [`TaskInput.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskInput.kt) - Utilisation de Modifier.fillMaxWidth(), padding()
> - [`TaskItem.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskItem.kt) - Modifier en paramètre avec valeur par défaut
> - [`TaskList.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskList.kt) - Column avec forEach

---

## 10. Composants Material3

### TextField et OutlinedTextField

Champs de saisie de texte avec différents styles.

```kotlin
// OutlinedTextField - Bordure autour du champ
@Composable
fun TaskSubjectField(
    value: String,
    onValueChange: (String) -> Unit,
    isError: Boolean
) {
    OutlinedTextField(
        // Valeur actuelle du champ
        value = value,

        // Callback appelé à chaque modification
        onValueChange = onValueChange,

        // Label qui s'anime au focus
        label = { Text("Sujet de la tâche") },

        // Placeholder visible quand le champ est vide
        placeholder = { Text("Entrez le sujet...") },

        // Icône au début du champ
        leadingIcon = {
            Icon(Icons.Default.Subject, contentDescription = null)
        },

        // Icône à la fin (ex: bouton effacer)
        trailingIcon = {
            if (value.isNotEmpty()) {
                IconButton(onClick = { onValueChange("") }) {
                    Icon(Icons.Default.Clear, "Effacer")
                }
            }
        },

        // État d'erreur
        isError = isError,

        // Texte d'aide ou d'erreur sous le champ
        supportingText = {
            if (isError) {
                Text("Le sujet est requis", color = MaterialTheme.colorScheme.error)
            }
        },

        // Une seule ligne
        singleLine = true,

        // Type de clavier
        keyboardOptions = KeyboardOptions(
            keyboardType = KeyboardType.Text,
            imeAction = ImeAction.Next  // Bouton "Suivant" sur le clavier
        ),

        // Action du bouton clavier
        keyboardActions = KeyboardActions(
            onNext = { /* Focus le champ suivant */ }
        ),

        modifier = Modifier.fillMaxWidth()
    )
}
```

### Button - Les Boutons

```kotlin
// Button principal (rempli)
Button(
    onClick = { /* Action */ },
    enabled = isFormValid,
    colors = ButtonDefaults.buttonColors(
        containerColor = MaterialTheme.colorScheme.primary,
        contentColor = MaterialTheme.colorScheme.onPrimary,
        disabledContainerColor = MaterialTheme.colorScheme.surfaceVariant,
        disabledContentColor = MaterialTheme.colorScheme.onSurfaceVariant
    )
) {
    Icon(Icons.Default.Add, contentDescription = null)
    Spacer(Modifier.width(8.dp))
    Text("Ajouter")
}

// OutlinedButton - Bouton avec bordure
OutlinedButton(onClick = { }) {
    Text("Annuler")
}

// TextButton - Bouton texte simple
TextButton(onClick = { }) {
    Text("En savoir plus")
}

// FilledTonalButton - Bouton avec couleur atténuée
FilledTonalButton(onClick = { }) {
    Text("Action secondaire")
}

// FloatingActionButton - Bouton d'action flottant
FloatingActionButton(
    onClick = { },
    containerColor = MaterialTheme.colorScheme.primaryContainer
) {
    Icon(Icons.Default.Add, "Ajouter")
}
```

### Card - Les Cartes

```kotlin
// Card simple
Card(
    modifier = Modifier.fillMaxWidth(),
    colors = CardDefaults.cardColors(
        containerColor = MaterialTheme.colorScheme.surfaceVariant
    )
) {
    Column(modifier = Modifier.padding(16.dp)) {
        Text("Titre", style = MaterialTheme.typography.titleMedium)
        Text("Contenu de la carte")
    }
}

// ElevatedCard - Avec élévation
ElevatedCard(
    elevation = CardDefaults.elevatedCardElevation(defaultElevation = 4.dp)
) {
    // Contenu
}

// OutlinedCard - Avec bordure
OutlinedCard(
    border = BorderStroke(1.dp, MaterialTheme.colorScheme.outline)
) {
    // Contenu
}

// Card cliquable
Card(
    onClick = { /* Navigation */ },
    modifier = Modifier.fillMaxWidth()
) {
    // Contenu
}
```

### Checkbox, Switch, RadioButton

```kotlin
// Checkbox
var checked by remember { mutableStateOf(false) }

Row(verticalAlignment = Alignment.CenterVertically) {
    Checkbox(
        checked = checked,
        onCheckedChange = { checked = it }
    )
    Text("J'accepte les conditions")
}

// Switch
var switched by remember { mutableStateOf(false) }

Row(verticalAlignment = Alignment.CenterVertically) {
    Text("Mode sombre")
    Spacer(Modifier.weight(1f))
    Switch(
        checked = switched,
        onCheckedChange = { switched = it }
    )
}

// RadioButton (groupe)
var selectedOption by remember { mutableStateOf("option1") }

Column {
    listOf("option1" to "Option 1", "option2" to "Option 2").forEach { (value, label) ->
        Row(verticalAlignment = Alignment.CenterVertically) {
            RadioButton(
                selected = selectedOption == value,
                onClick = { selectedOption = value }
            )
            Text(label)
        }
    }
}
```

### Icon et IconButton

```kotlin
// Icon simple
Icon(
    imageVector = Icons.Default.Favorite,
    contentDescription = "Favori",  // Important pour l'accessibilité
    tint = Color.Red
)

// Icon depuis ressource
Icon(
    painter = painterResource(R.drawable.custom_icon),
    contentDescription = "Icône personnalisée"
)

// IconButton - Bouton icône cliquable
IconButton(
    onClick = { /* Action */ },
    enabled = true
) {
    Icon(Icons.Default.Delete, contentDescription = "Supprimer")
}
```

### Divider - Séparateur

```kotlin
// HorizontalDivider (anciennement Divider)
HorizontalDivider(
    modifier = Modifier.padding(vertical = 8.dp),
    thickness = 1.dp,
    color = MaterialTheme.colorScheme.outlineVariant
)

// VerticalDivider
Row(modifier = Modifier.height(40.dp)) {
    Text("Gauche")
    VerticalDivider(modifier = Modifier.padding(horizontal = 8.dp))
    Text("Droite")
}
```

> **Voir dans le projet :**
> - [`TaskInput.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskInput.kt) - OutlinedTextField, Button
> - [`TaskItem.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskItem.kt) - Checkbox, IconButton, Icon
> - [`TaskList.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskList.kt) - HorizontalDivider
> - [`TaskSwitch.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskSwitch.kt) - Switch
> - [`HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - FloatingActionButton

---

## 11. Flux de Données Unidirectionnel

### Le Principe

Le **flux de données unidirectionnel** (Unidirectional Data Flow - UDF) est un pattern architectural où :
- **L'état descend** : les composants parents passent l'état aux enfants via les paramètres
- **Les événements remontent** : les composants enfants notifient les parents via des callbacks

```
┌─────────────────────────────────────────────────────────┐
│                     PARENT                              │
│  ┌─────────────┐                   ┌─────────────────┐  │
│  │    État     │ ──── descend ──► │    Composable   │  │
│  │  (state)    │                   │     Enfant      │  │
│  └─────────────┘                   └────────┬────────┘  │
│         ▲                                   │           │
│         │                                   │           │
│         └──── remonte ──── Événement ◄──────┘           │
│                           (callback)                    │
└─────────────────────────────────────────────────────────┘
```

### Exemple Concret : TaskInputForm

```kotlin
// Composable STATELESS (sans état) - Réutilisable et testable
@Composable
fun TaskInputForm(
    // ÉTAT (descend du parent)
    subject: String,
    place: String,
    isSubjectError: Boolean,
    isPlaceError: Boolean,

    // ÉVÉNEMENTS (remontent vers le parent)
    onSubjectChange: (String) -> Unit,
    onPlaceChange: (String) -> Unit,
    onAddClick: () -> Unit,

    modifier: Modifier = Modifier
) {
    Column(modifier = modifier.padding(16.dp)) {
        OutlinedTextField(
            value = subject,                    // État reçu
            onValueChange = onSubjectChange,    // Événement émis
            label = { Text("Sujet") },
            isError = isSubjectError
        )

        OutlinedTextField(
            value = place,
            onValueChange = onPlaceChange,
            label = { Text("Lieu") },
            isError = isPlaceError
        )

        Button(
            onClick = onAddClick,               // Événement émis
            enabled = subject.isNotEmpty() && place.isNotEmpty()
        ) {
            Text("Ajouter")
        }
    }
}
```

### Composable Stateful vs Stateless

**Stateless (sans état)** - Préféré pour la réutilisation :
```kotlin
@Composable
fun TaskItem(
    task: Task,                      // Données reçues
    onDelete: (Task) -> Unit,        // Callback pour les actions
    modifier: Modifier = Modifier
) {
    // Pas de remember, pas d'état local
    Row(modifier = modifier) {
        Text(task.subject)
        IconButton(onClick = { onDelete(task) }) {
            Icon(Icons.Default.Delete, "Supprimer")
        }
    }
}
```

**Stateful (avec état)** - Quand l'état est purement local :
```kotlin
@Composable
fun ExpandableTaskItem(
    task: Task,
    onDelete: (Task) -> Unit
) {
    // État local : l'expansion est un détail d'UI, pas une donnée métier
    var isExpanded by remember { mutableStateOf(false) }

    Column {
        Row(
            modifier = Modifier.clickable { isExpanded = !isExpanded }
        ) {
            Text(task.subject)
            Icon(
                if (isExpanded) Icons.Default.ExpandLess else Icons.Default.ExpandMore,
                "Expand"
            )
        }

        if (isExpanded) {
            Text(task.description ?: "Pas de description")
        }
    }
}
```

### State Hoisting (Remontée de l'État)

Le **state hoisting** consiste à "remonter" l'état vers un composable parent pour :
1. Permettre au parent de contrôler l'état
2. Rendre le composable enfant réutilisable
3. Faciliter les tests

```kotlin
// AVANT : État interne (difficile à tester, non réutilisable)
@Composable
fun SearchBar() {
    var query by remember { mutableStateOf("") }
    TextField(value = query, onValueChange = { query = it })
}

// APRÈS : État remonté (testable, réutilisable)
@Composable
fun SearchBar(
    query: String,
    onQueryChange: (String) -> Unit
) {
    TextField(value = query, onValueChange = onQueryChange)
}

// Le parent gère l'état
@Composable
fun SearchScreen() {
    var searchQuery by remember { mutableStateOf("") }

    Column {
        SearchBar(
            query = searchQuery,
            onQueryChange = { searchQuery = it }
        )
        // Le parent peut utiliser searchQuery pour filtrer
        FilteredResults(query = searchQuery)
    }
}
```

### Avantages du Flux Unidirectionnel

1. **Prévisibilité** : L'état vient d'une seule source (single source of truth)
2. **Débogage facilité** : On peut tracer d'où vient chaque modification
3. **Testabilité** : Les composables stateless sont faciles à tester
4. **Réutilisabilité** : Les composables sont découplés de la logique métier

> **Voir dans le projet :**
> - [`TaskInput.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskInput.kt) - `TaskInputForm` reçoit l'état et les callbacks
> - [`TaskItem.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskItem.kt) - Composable stateless avec callbacks `onTaskDeleted`
> - [`HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - State hoisting avec `TaskViewModel`

---

## 12. ViewModel - Gestion de la Logique Métier

### Qu'est-ce qu'un ViewModel ?

Le `ViewModel` est un composant d'architecture Android qui :
1. **Survit aux changements de configuration** (rotation, changement de langue)
2. **Sépare la logique métier de l'UI**
3. **Gère l'état de l'écran**
4. **Coordonne les opérations asynchrones**

```kotlin
class TaskViewModel(
    private val tasksRepository: TasksRepository
) : ViewModel() {

    // État du formulaire
    private val _subject = MutableStateFlow("")
    val subject: StateFlow<String> = _subject.asStateFlow()

    private val _place = MutableStateFlow("")
    val place: StateFlow<String> = _place.asStateFlow()

    // Liste des tâches (depuis le repository)
    val tasks: Flow<List<Task>> = tasksRepository.getTasks()

    // Méthodes pour modifier l'état
    fun onSubjectChange(newSubject: String) {
        _subject.value = newSubject
    }

    fun onPlaceChange(newPlace: String) {
        _place.value = newPlace
    }

    // Opérations métier
    fun addTask() {
        if (_subject.value.isNotEmpty() && _place.value.isNotEmpty()) {
            viewModelScope.launch {
                val newTask = Task(
                    subject = _subject.value,
                    place = _place.value
                )
                tasksRepository.insertTask(newTask)
                clearInputFields()
            }
        }
    }

    fun removeTask(task: Task) {
        viewModelScope.launch {
            tasksRepository.deleteTask(task)
        }
    }

    private fun clearInputFields() {
        _subject.value = ""
        _place.value = ""
    }
}
```

### Cycle de Vie du ViewModel

```
Activity/Fragment créé
         │
         ▼
    ViewModel créé (ou récupéré si déjà existant)
         │
         ▼
    ┌────────────────────────────────────────┐
    │  Configuration change (rotation)       │
    │  Activity détruite et recréée          │
    │  → ViewModel SURVIT                    │
    └────────────────────────────────────────┘
         │
         ▼
    Activity/Fragment définitivement détruit
    (finish() ou navigation arrière)
         │
         ▼
    ViewModel.onCleared() appelé
    ViewModel détruit
```

### Utilisation dans Compose

```kotlin
@Composable
fun HomeScreen(
    taskViewModel: TaskViewModel = viewModel()  // Récupère ou crée le ViewModel
) {
    val tasks by taskViewModel.tasks.collectAsState(initial = emptyList())
    val subject by taskViewModel.subject.collectAsState()

    Column {
        TextField(
            value = subject,
            onValueChange = { taskViewModel.onSubjectChange(it) }
        )

        LazyColumn {
            items(tasks) { task ->
                TaskItem(
                    task = task,
                    onDelete = { taskViewModel.removeTask(it) }
                )
            }
        }
    }
}
```

### Bonnes Pratiques

1. **Ne pas passer de Context au ViewModel** - Utilisez `AndroidViewModel` si nécessaire
2. **Exposer des StateFlow immuables** - Pattern backing property
3. **Utiliser viewModelScope pour les coroutines**
4. **Un ViewModel par écran** - Pas de ViewModel partagé entre écrans non liés

> **Voir dans le projet :**
> - [`TaskViewModel.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModel.kt) - ViewModel complet avec StateFlow et méthodes métier

---

## 13. StateFlow et MutableStateFlow

### Différence entre StateFlow et Flow

| Aspect | Flow | StateFlow |
|--------|------|-----------|
| Valeur actuelle | Non (flux de données) | Oui (toujours une valeur) |
| Hot/Cold | Cold (démarre à la collecte) | Hot (actif immédiatement) |
| Replay | Non | Oui (dernière valeur) |
| Cas d'usage | Flux de données (DB, réseau) | État observable |

### MutableStateFlow - État Mutable

```kotlin
class TaskViewModel : ViewModel() {
    // MutableStateFlow : on peut modifier la valeur
    private val _isLoading = MutableStateFlow(false)

    // StateFlow : version en lecture seule exposée publiquement
    val isLoading: StateFlow<Boolean> = _isLoading.asStateFlow()

    fun loadData() {
        viewModelScope.launch {
            _isLoading.value = true          // Modification directe

            // Charger les données...
            delay(1000)

            _isLoading.value = false
        }
    }
}
```

### Backing Property Pattern

Ce pattern expose une version immuable de l'état pour empêcher les modifications externes :

```kotlin
class TaskViewModel : ViewModel() {
    // Privé et mutable - seul le ViewModel peut modifier
    private val _subject = MutableStateFlow("")

    // Public et immuable - l'UI peut seulement lire
    val subject: StateFlow<String> = _subject.asStateFlow()

    // L'UI doit passer par cette fonction pour modifier
    fun onSubjectChange(newSubject: String) {
        _subject.value = newSubject
    }
}
```

**Pourquoi ce pattern ?**
- Encapsulation : l'état ne peut être modifié que via des méthodes contrôlées
- Validation : on peut valider les nouvelles valeurs avant de les accepter
- Débogage : toutes les modifications passent par un seul point

### StateFlow vs LiveData

| Aspect | StateFlow | LiveData |
|--------|-----------|----------|
| Null safety | Non-null par défaut | Nullable |
| Lifecycle-aware | Non (manuel) | Oui (automatique) |
| Transformations | Opérateurs Flow | Transformations limitées |
| Coroutines | Intégré | Via extension |
| Initial value | Requis | Optionnel |

Dans Compose, `StateFlow` est préféré car :
- Meilleure intégration avec les coroutines
- Plus de flexibilité avec les opérateurs Flow
- `collectAsState()` gère automatiquement le lifecycle

### Opérations sur StateFlow

```kotlin
class TaskViewModel : ViewModel() {
    private val _searchQuery = MutableStateFlow("")
    val searchQuery: StateFlow<String> = _searchQuery.asStateFlow()

    private val _allTasks = MutableStateFlow<List<Task>>(emptyList())

    // Transformation : filtrer les tâches selon la recherche
    val filteredTasks: StateFlow<List<Task>> = combine(
        _allTasks,
        _searchQuery
    ) { tasks, query ->
        if (query.isEmpty()) tasks
        else tasks.filter { it.subject.contains(query, ignoreCase = true) }
    }.stateIn(
        scope = viewModelScope,
        started = SharingStarted.WhileSubscribed(5000),
        initialValue = emptyList()
    )
}
```

> **Voir dans le projet :**
> - [`TaskViewModel.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModel.kt) - Backing property pattern avec `_subject` / `subject`

---

## 14. collectAsState - Pont entre Flow et Compose

### Fonctionnement

`collectAsState()` convertit un `Flow` ou `StateFlow` en `State<T>` observable par Compose.

```kotlin
@Composable
fun TaskList(viewModel: TaskViewModel) {
    // Convertit le StateFlow en State<List<Task>>
    val tasks by viewModel.tasks.collectAsState(initial = emptyList())

    // 'tasks' est maintenant une List<Task> que Compose observe
    // Toute modification du StateFlow déclenche une recomposition

    LazyColumn {
        items(tasks) { task ->
            TaskItem(task = task)
        }
    }
}
```

### Avec et Sans Valeur Initiale

```kotlin
// StateFlow - pas besoin de valeur initiale (en a déjà une)
val stateFlow: StateFlow<String> = viewModel.subject
val state1 by stateFlow.collectAsState()  // OK

// Flow - nécessite une valeur initiale
val flow: Flow<List<Task>> = viewModel.tasks
val state2 by flow.collectAsState(initial = emptyList())  // Requis
```

### Lifecycle et collectAsState

`collectAsState()` respecte automatiquement le lifecycle du composable :
- Commence à collecter quand le composable entre dans la composition
- Arrête de collecter quand le composable sort de la composition

```kotlin
@Composable
fun MyScreen() {
    // La collecte s'arrête automatiquement si MyScreen est retiré de l'écran
    val data by viewModel.data.collectAsState()
}
```

### collectAsStateWithLifecycle

Pour un contrôle plus fin du lifecycle (recommandé pour les données qui changent fréquemment) :

```kotlin
// Nécessite : implementation "androidx.lifecycle:lifecycle-runtime-compose:2.6.0"

@Composable
fun MyScreen() {
    val data by viewModel.data.collectAsStateWithLifecycle()
    // Arrête la collecte quand l'app passe en arrière-plan (onStop)
}
```

> **Voir dans le projet :**
> - [`TaskInput.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/task/TaskInput.kt) - `collectAsState()` pour observer le ViewModel
> - [`HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - Collecte des tasks avec valeur initiale

---

## 15. ViewModelFactory - Injection de Dépendances

### Le Problème

Par défaut, `viewModel()` ne peut créer que des ViewModels avec un constructeur sans paramètre :

```kotlin
// Fonctionne
class SimpleViewModel : ViewModel()

// NE FONCTIONNE PAS avec viewModel() par défaut
class TaskViewModel(private val repository: TasksRepository) : ViewModel()
```

### La Solution : ViewModelProvider.Factory

```kotlin
class TaskViewModelFactory(
    private val tasksRepository: TasksRepository
) : ViewModelProvider.Factory {

    @Suppress("UNCHECKED_CAST")
    override fun <T : ViewModel> create(modelClass: Class<T>): T {
        // Vérifie que la classe demandée est bien TaskViewModel
        if (modelClass.isAssignableFrom(TaskViewModel::class.java)) {
            // Crée l'instance avec les dépendances
            return TaskViewModel(tasksRepository) as T
        }
        throw IllegalArgumentException("Unknown ViewModel class: ${modelClass.name}")
    }
}
```

### Utilisation dans Compose

```kotlin
@Composable
fun TaskNavHost(navController: NavHostController) {
    // Récupère le repository depuis l'Application
    val application = LocalContext.current.applicationContext as MyCampusTasksApplication
    val tasksRepository = application.tasksRepository

    // Crée le ViewModel avec la factory
    val taskViewModel: TaskViewModel = viewModel(
        factory = TaskViewModelFactory(tasksRepository)
    )

    NavHost(navController = navController, startDestination = "home") {
        composable("home") {
            HomeScreen(taskViewModel = taskViewModel)
        }
    }
}
```

### Factory avec Plusieurs ViewModels

```kotlin
class AppViewModelFactory(
    private val tasksRepository: TasksRepository,
    private val userRepository: UserRepository
) : ViewModelProvider.Factory {

    @Suppress("UNCHECKED_CAST")
    override fun <T : ViewModel> create(modelClass: Class<T>): T {
        return when {
            modelClass.isAssignableFrom(TaskViewModel::class.java) -> {
                TaskViewModel(tasksRepository) as T
            }
            modelClass.isAssignableFrom(UserViewModel::class.java) -> {
                UserViewModel(userRepository) as T
            }
            else -> throw IllegalArgumentException("Unknown ViewModel: ${modelClass.name}")
        }
    }
}
```

### Alternative Moderne : Hilt

Avec Hilt (injection de dépendances), la factory est générée automatiquement :

```kotlin
@HiltViewModel
class TaskViewModel @Inject constructor(
    private val tasksRepository: TasksRepository
) : ViewModel() {
    // ...
}

// Utilisation simplifiée
@Composable
fun TaskScreen() {
    val viewModel: TaskViewModel = hiltViewModel()
}
```

> **Voir dans le projet :**
> - [`TaskViewModelFactory.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModelFactory.kt) - Factory complète
> - [`TaskNavigationGraph.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/TaskNavigationGraph.kt) - Utilisation de la factory avec `viewModel()`

---

## 16. Coroutines et viewModelScope

### Qu'est-ce qu'une Coroutine ?

Une **coroutine** est une unité de code qui peut être suspendue et reprise, permettant d'écrire du code asynchrone de manière séquentielle.

```kotlin
// SANS coroutines (callbacks)
fun loadData(callback: (Result) -> Unit) {
    api.fetch { result1 ->
        api.process(result1) { result2 ->
            api.save(result2) { finalResult ->
                callback(finalResult)  // Callback hell
            }
        }
    }
}

// AVEC coroutines (séquentiel)
suspend fun loadData(): Result {
    val result1 = api.fetch()      // Suspend, attend le résultat
    val result2 = api.process(result1)
    return api.save(result2)
}
```

### Fonctions suspend

Une fonction `suspend` peut être mise en pause sans bloquer le thread :

```kotlin
// Cette fonction peut être suspendue
suspend fun insertTask(task: Task) {
    // Le thread n'est pas bloqué pendant l'attente
    database.taskDao().insert(task)
}

// Doit être appelée depuis une coroutine ou une autre fonction suspend
viewModelScope.launch {
    insertTask(myTask)  // OK
}

// insertTask(myTask)  // ERREUR : pas dans une coroutine
```

### viewModelScope

`viewModelScope` est un `CoroutineScope` lié au cycle de vie du ViewModel :

```kotlin
class TaskViewModel : ViewModel() {

    fun addTask(task: Task) {
        // Lance une coroutine dans le scope du ViewModel
        viewModelScope.launch {
            try {
                repository.insertTask(task)
                // Succès
            } catch (e: Exception) {
                // Erreur
            }
        }
        // Le code ici s'exécute IMMÉDIATEMENT, sans attendre
    }
}
```

**Avantages de viewModelScope :**
- **Annulation automatique** : Quand le ViewModel est détruit, toutes les coroutines sont annulées
- **Dispatcher par défaut** : `Dispatchers.Main.immediate` (thread principal)
- **Pas de fuite mémoire** : Les coroutines ne survivent pas au ViewModel

### Dispatchers

Les **dispatchers** définissent sur quel thread la coroutine s'exécute :

```kotlin
viewModelScope.launch {
    // Dispatchers.Main (défaut) - Thread principal (UI)
    updateUiState(loading = true)

    // Dispatchers.IO - Thread d'I/O (réseau, base de données)
    val data = withContext(Dispatchers.IO) {
        repository.fetchData()
    }

    // Retour automatique sur Main
    updateUiState(data = data, loading = false)
}
```

### Opérations Parallèles

```kotlin
viewModelScope.launch {
    // Séquentiel
    val user = repository.getUser()      // Attend
    val posts = repository.getPosts()    // Puis attend
    // Total : temps(user) + temps(posts)

    // Parallèle avec async
    val userDeferred = async { repository.getUser() }
    val postsDeferred = async { repository.getPosts() }

    val user = userDeferred.await()
    val posts = postsDeferred.await()
    // Total : max(temps(user), temps(posts))
}
```

### Gestion des Erreurs

```kotlin
viewModelScope.launch {
    try {
        val result = repository.fetchData()
        _state.value = State.Success(result)
    } catch (e: IOException) {
        _state.value = State.Error("Erreur réseau")
    } catch (e: Exception) {
        _state.value = State.Error("Erreur inconnue")
    }
}
```

> **Voir dans le projet :**
> - [`TaskViewModel.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModel.kt) - Utilisation de `viewModelScope.launch` pour les opérations asynchrones

---

## 17. Navigation Compose

### Architecture de Navigation

La navigation dans Compose repose sur trois concepts :
1. **NavController** : Gère la pile de navigation (backstack)
2. **NavHost** : Conteneur qui affiche la destination courante
3. **NavGraph** : Définit les destinations et leurs routes

### Définir les Destinations

```kotlin
// Interface pour typer les destinations
interface NavigationDestination {
    val route: String      // Identifiant unique de la route
    val titleRes: Int      // Ressource string pour le titre
}

// Destinations concrètes
object HomeDestination : NavigationDestination {
    override val route = "home"
    override val titleRes = R.string.app_name
}

object TaskInputDestination : NavigationDestination {
    override val route = "task_input"
    override val titleRes = R.string.task_add
}

object TaskDetailDestination : NavigationDestination {
    override val route = "task_detail"
    override val titleRes = R.string.task_detail

    // Route avec argument
    const val taskIdArg = "taskId"
    val routeWithArgs = "$route/{$taskIdArg}"
}
```

### Configurer le NavHost

```kotlin
@Composable
fun TaskNavHost(
    navController: NavHostController = rememberNavController(),
    startDestination: String = HomeDestination.route
) {
    NavHost(
        navController = navController,
        startDestination = startDestination
    ) {
        // Destination simple
        composable(route = HomeDestination.route) {
            HomeScreen(
                navigateToTaskInput = {
                    navController.navigate(TaskInputDestination.route)
                },
                navigateToTaskDetail = { taskId ->
                    navController.navigate("${TaskDetailDestination.route}/$taskId")
                }
            )
        }

        // Destination simple
        composable(route = TaskInputDestination.route) {
            TaskInputScreen(
                navigateBack = { navController.popBackStack() }
            )
        }

        // Destination avec argument
        composable(
            route = TaskDetailDestination.routeWithArgs,
            arguments = listOf(
                navArgument(TaskDetailDestination.taskIdArg) {
                    type = NavType.IntType
                }
            )
        ) { backStackEntry ->
            val taskId = backStackEntry.arguments?.getInt(TaskDetailDestination.taskIdArg)
            TaskDetailScreen(
                taskId = taskId ?: 0,
                navigateBack = { navController.popBackStack() }
            )
        }
    }
}
```

### NavController et Navigation

```kotlin
// Créer/récupérer le NavController
val navController = rememberNavController()

// Naviguer vers une destination
navController.navigate("task_input")

// Naviguer avec argument
navController.navigate("task_detail/42")

// Retour arrière
navController.popBackStack()

// Naviguer en remplaçant la destination courante
navController.navigate("home") {
    popUpTo("home") { inclusive = true }
}

// Naviguer en vidant la pile
navController.navigate("login") {
    popUpTo(0) { inclusive = true }
}
```

### Passer le NavController vs Passer des Lambdas

**Approche recommandée : Lambdas**
```kotlin
@Composable
fun HomeScreen(
    navigateToTaskInput: () -> Unit,    // Lambda de navigation
    navigateToTaskDetail: (Int) -> Unit
) {
    // Le composable ne connaît pas NavController
    Button(onClick = navigateToTaskInput) {
        Text("Ajouter")
    }
}
```

**Pourquoi ?**
- Meilleure testabilité (pas besoin de NavController dans les tests)
- Découplage (l'écran ne sait pas comment la navigation est implémentée)
- Réutilisabilité (peut fonctionner avec différents systèmes de navigation)

### Navigation avec Résultat

```kotlin
// Écran A : attend un résultat
@Composable
fun ScreenA(navController: NavController) {
    val result = navController.currentBackStackEntry
        ?.savedStateHandle
        ?.get<String>("result_key")

    LaunchedEffect(result) {
        result?.let {
            // Traiter le résultat
        }
    }
}

// Écran B : renvoie un résultat
@Composable
fun ScreenB(navController: NavController) {
    Button(onClick = {
        navController.previousBackStackEntry
            ?.savedStateHandle
            ?.set("result_key", "valeur_retournée")
        navController.popBackStack()
    }) {
        Text("Retourner avec résultat")
    }
}
```

> **Voir dans le projet :**
> - [`TaskNavigationGraph.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/TaskNavigationGraph.kt) - Configuration NavHost
> - [`NavigationDestination.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/NavigationDestination.kt) - Interface de destination
> - [`TaskNavigationDestination.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/TaskNavigationDestination.kt) - Destinations concrètes (HomeDestination, TaskInputDestination)

---

## 18. LocalContext et CompositionLocal

### Qu'est-ce que CompositionLocal ?

`CompositionLocal` permet de passer des données implicitement à travers l'arbre de composition, sans les passer explicitement en paramètre à chaque niveau.

```kotlin
// Sans CompositionLocal : passage explicite
@Composable
fun GrandParent(context: Context) {
    Parent(context = context)
}

@Composable
fun Parent(context: Context) {
    Child(context = context)
}

@Composable
fun Child(context: Context) {
    // Utilise context
}

// Avec CompositionLocal : passage implicite
@Composable
fun Child() {
    val context = LocalContext.current  // Accès direct
}
```

### CompositionLocals Fournis par Android/Compose

```kotlin
@Composable
fun MyComposable() {
    // Context Android
    val context = LocalContext.current

    // Configuration (langue, orientation, etc.)
    val configuration = LocalConfiguration.current
    val isLandscape = configuration.orientation == Configuration.ORIENTATION_LANDSCAPE

    // Density (pour convertir dp <-> px)
    val density = LocalDensity.current
    val pxValue = with(density) { 16.dp.toPx() }

    // Lifecycle owner
    val lifecycleOwner = LocalLifecycleOwner.current

    // View (pour l'interop avec le système de View)
    val view = LocalView.current

    // Focus manager
    val focusManager = LocalFocusManager.current
    focusManager.clearFocus()
}
```

### Utilisation de LocalContext

```kotlin
@Composable
fun TaskNavHost() {
    // Récupère le contexte
    val context = LocalContext.current

    // Accède à l'Application personnalisée
    val application = context.applicationContext as MyCampusTasksApplication

    // Récupère le repository
    val tasksRepository = application.tasksRepository

    // Crée le ViewModel avec la factory
    val taskViewModel: TaskViewModel = viewModel(
        factory = TaskViewModelFactory(tasksRepository)
    )

    NavHost(navController = navController, startDestination = "home") {
        composable("home") {
            HomeScreen(taskViewModel = taskViewModel)
        }
    }
}
```

### Créer son Propre CompositionLocal

```kotlin
// 1. Définir le CompositionLocal
data class AppTheme(
    val primaryColor: Color,
    val secondaryColor: Color
)

val LocalAppTheme = compositionLocalOf<AppTheme> {
    error("No AppTheme provided")  // Erreur si non fourni
}

// Alternative avec valeur par défaut
val LocalAppTheme = staticCompositionLocalOf {
    AppTheme(Color.Blue, Color.Green)
}

// 2. Fournir la valeur
@Composable
fun App() {
    val theme = AppTheme(Color.Red, Color.Yellow)

    CompositionLocalProvider(LocalAppTheme provides theme) {
        // Tous les composables enfants peuvent accéder à LocalAppTheme
        MainScreen()
    }
}

// 3. Consommer la valeur
@Composable
fun SomeDeepComponent() {
    val theme = LocalAppTheme.current
    Box(modifier = Modifier.background(theme.primaryColor))
}
```

### compositionLocalOf vs staticCompositionLocalOf

| Aspect | `compositionLocalOf` | `staticCompositionLocalOf` |
|--------|---------------------|---------------------------|
| Changement de valeur | Recompose seulement les consommateurs | Recompose TOUT le sous-arbre |
| Performance | Meilleure pour valeurs changeantes | Meilleure pour valeurs stables |
| Cas d'usage | Thème dynamique, préférences | Context, configuration système |

> **Voir dans le projet :**
> - [`TaskNavigationGraph.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/navigation/TaskNavigationGraph.kt) - Utilisation de `LocalContext.current` pour accéder à l'Application

---

## 19. Room Database - Persistance Locale

### Architecture Room

Room est une bibliothèque de persistance qui fournit une couche d'abstraction sur SQLite.

```
┌─────────────────────────────────────────────────────────┐
│                    APPLICATION                          │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐  │
│  │  ViewModel  │───►│  Repository │───►│     DAO     │  │
│  └─────────────┘    └─────────────┘    └──────┬──────┘  │
│                                               │         │
│                                        ┌──────▼──────┐  │
│                                        │   Database  │  │
│                                        │    (Room)   │  │
│                                        └──────┬──────┘  │
│                                               │         │
└─────────────────────────────────────────────────────────┘
```

### Entity - Définir les Tables

Une `@Entity` représente une table dans la base de données :

```kotlin
@Entity(tableName = "task")  // Nom de la table
data class Task(
    // Clé primaire auto-incrémentée
    @PrimaryKey(autoGenerate = true)
    val id: Int = 0,

    // Colonne simple (nom = nom de la propriété)
    val subject: String,

    // Colonne avec nom personnalisé
    @ColumnInfo(name = "task_place")
    var place: String,

    // Colonne nullable
    @ColumnInfo(name = "description")
    var description: String? = null,

    // Colonne avec type personnalisé (nécessite TypeConverter)
    @ColumnInfo(name = "created_at")
    val createdAt: Date? = Date(),

    // Colonne ignorée (pas stockée en base)
    @Ignore
    val isSelected: Boolean = false
)
```

### Annotations Entity Avancées

```kotlin
@Entity(
    tableName = "task",

    // Index pour accélérer les recherches
    indices = [
        Index(value = ["subject"]),
        Index(value = ["created_at"], unique = false)
    ],

    // Clé étrangère
    foreignKeys = [
        ForeignKey(
            entity = Category::class,
            parentColumns = ["id"],
            childColumns = ["category_id"],
            onDelete = ForeignKey.CASCADE
        )
    ]
)
data class Task(
    @PrimaryKey(autoGenerate = true) val id: Int = 0,
    val subject: String,

    @ColumnInfo(name = "category_id", index = true)
    val categoryId: Int
)
```

### DAO - Data Access Object

Le `@Dao` définit les méthodes d'accès à la base de données :

```kotlin
@Dao
interface TaskDao {

    // INSERT
    @Insert
    suspend fun insert(task: Task)

    @Insert(onConflict = OnConflictStrategy.REPLACE)
    suspend fun insertOrUpdate(task: Task)

    @Insert
    suspend fun insertAll(tasks: List<Task>)

    // UPDATE
    @Update
    suspend fun update(task: Task)

    // DELETE
    @Delete
    suspend fun delete(task: Task)

    @Query("DELETE FROM task WHERE id = :taskId")
    suspend fun deleteById(taskId: Int)

    @Query("DELETE FROM task")
    suspend fun deleteAll()

    // SELECT - Retourne un Flow pour l'observation réactive
    @Query("SELECT * FROM task ORDER BY subject ASC")
    fun getAllTasks(): Flow<List<Task>>

    @Query("SELECT * FROM task WHERE id = :taskId")
    fun getTaskById(taskId: Int): Flow<Task?>

    @Query("SELECT * FROM task WHERE subject LIKE '%' || :query || '%'")
    fun searchTasks(query: String): Flow<List<Task>>

    // SELECT - Retourne une valeur directe (pour les opérations ponctuelles)
    @Query("SELECT COUNT(*) FROM task")
    suspend fun getTaskCount(): Int

    @Query("SELECT * FROM task WHERE id = :taskId")
    suspend fun getTaskByIdOnce(taskId: Int): Task?
}
```

### Database - Configuration

```kotlin
@Database(
    entities = [Task::class, Category::class],  // Liste des entités
    version = 3,                                  // Version du schéma
    exportSchema = true                           // Exporter le schéma pour les tests
)
@TypeConverters(DateTypeConverter::class)        // Convertisseurs de types
abstract class TaskDatabase : RoomDatabase() {

    // Accès aux DAOs
    abstract fun taskDao(): TaskDao
    abstract fun categoryDao(): CategoryDao

    companion object {
        // Singleton thread-safe
        @Volatile
        private var INSTANCE: TaskDatabase? = null

        fun getDatabase(context: Context): TaskDatabase {
            // Double-checked locking
            return INSTANCE ?: synchronized(this) {
                INSTANCE ?: buildDatabase(context).also { INSTANCE = it }
            }
        }

        private fun buildDatabase(context: Context): TaskDatabase {
            return Room.databaseBuilder(
                context.applicationContext,
                TaskDatabase::class.java,
                "task_database"
            )
            .addMigrations(MIGRATION_1_2, MIGRATION_2_3)
            .fallbackToDestructiveMigration()  // En dernier recours
            .build()
        }
    }
}
```

### Flow vs suspend dans le DAO

```kotlin
@Dao
interface TaskDao {
    // Flow : pour observer les changements en continu
    // Utilisé pour les listes qui doivent se mettre à jour automatiquement
    @Query("SELECT * FROM task")
    fun getAllTasks(): Flow<List<Task>>

    // suspend : pour les opérations ponctuelles
    // Utilisé pour insert, update, delete, ou lectures uniques
    @Insert
    suspend fun insert(task: Task)

    @Query("SELECT * FROM task WHERE id = :id")
    suspend fun getTaskById(id: Int): Task?
}
```

> **Voir dans le projet :**
> - [`Task.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/Task.kt) - Entity Room avec annotations
> - [`TaskDao.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TaskDao.kt) - Data Access Object (DAO)
> - [`TaskDatabase.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TaskDatabase.kt) - Configuration de la base de données Room

---

## 20. TypeConverter - Conversion de Types

### Pourquoi les TypeConverters ?

SQLite ne supporte que quelques types primitifs :
- `NULL`
- `INTEGER` (Long, Int, Short, Byte, Boolean)
- `REAL` (Double, Float)
- `TEXT` (String)
- `BLOB` (ByteArray)

Pour stocker des types complexes comme `Date`, `List`, ou des enums, on utilise des **TypeConverters**.

### Convertir Date ↔ Long

```kotlin
class DateTypeConverter {

    // Long (stocké en base) → Date (utilisé dans le code)
    @TypeConverter
    fun toDate(timestamp: Long?): Date? {
        return timestamp?.let { Date(it) }
    }

    // Date (utilisé dans le code) → Long (stocké en base)
    @TypeConverter
    fun toLong(date: Date?): Long? {
        return date?.time
    }
}
```

### Convertir Date ↔ String (ISO 8601)

Pour la compatibilité avec les APIs REST :

```kotlin
class DateTypeConverter {
    private val dateFormat = SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", Locale.US).apply {
        timeZone = TimeZone.getTimeZone("UTC")
    }

    @TypeConverter
    fun toDate(dateString: String?): Date? {
        return dateString?.let {
            try {
                dateFormat.parse(it)
            } catch (e: Exception) {
                null
            }
        }
    }

    @TypeConverter
    fun toString(date: Date?): String? {
        return date?.let { dateFormat.format(it) }
    }
}
```

### Convertir List ↔ String (JSON)

```kotlin
class ListTypeConverter {
    private val gson = Gson()

    @TypeConverter
    fun fromStringList(list: List<String>?): String? {
        return list?.let { gson.toJson(it) }
    }

    @TypeConverter
    fun toStringList(json: String?): List<String>? {
        return json?.let {
            val type = object : TypeToken<List<String>>() {}.type
            gson.fromJson(it, type)
        }
    }
}
```

### Convertir Enum ↔ String

```kotlin
enum class TaskPriority { LOW, MEDIUM, HIGH }

class EnumTypeConverter {
    @TypeConverter
    fun toPriority(value: String?): TaskPriority? {
        return value?.let { TaskPriority.valueOf(it) }
    }

    @TypeConverter
    fun fromPriority(priority: TaskPriority?): String? {
        return priority?.name
    }
}
```

### Enregistrer les TypeConverters

```kotlin
@Database(entities = [Task::class], version = 1)
@TypeConverters(
    DateTypeConverter::class,
    ListTypeConverter::class,
    EnumTypeConverter::class
)
abstract class TaskDatabase : RoomDatabase() {
    // ...
}
```

> **Voir dans le projet :**
> - [`DateTypeConverter.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/DateTypeConverter.kt) - Convertisseur Date ↔ Long
> - [`TaskDatabase.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TaskDatabase.kt) - Enregistrement du TypeConverter avec `@TypeConverters`

---

## 21. Migrations Room

### Pourquoi les Migrations ?

Quand le schéma de la base de données change (nouvelle colonne, nouveau type), Room doit savoir comment transformer les données existantes.

**Sans migration :**
- L'app crash au démarrage
- Ou les données sont perdues (avec `fallbackToDestructiveMigration()`)

**Avec migration :**
- Les données existantes sont préservées
- Le schéma est mis à jour proprement

### Créer une Migration

```kotlin
// Migration de la version 1 à 2 : ajouter une colonne 'description'
val MIGRATION_1_2 = object : Migration(1, 2) {
    override fun migrate(db: SupportSQLiteDatabase) {
        // SQL pour modifier le schéma
        db.execSQL("ALTER TABLE task ADD COLUMN description TEXT NULL")
    }
}

// Migration de la version 2 à 3 : ajouter une colonne 'created_at'
val MIGRATION_2_3 = object : Migration(2, 3) {
    override fun migrate(db: SupportSQLiteDatabase) {
        // INTEGER car Date est converti en Long par le TypeConverter
        db.execSQL("ALTER TABLE task ADD COLUMN created_at INTEGER NULL")
    }
}
```

### Enregistrer les Migrations

```kotlin
@Database(entities = [Task::class], version = 3)
abstract class TaskDatabase : RoomDatabase() {

    companion object {
        fun getDatabase(context: Context): TaskDatabase {
            return Room.databaseBuilder(
                context,
                TaskDatabase::class.java,
                "task_database"
            )
            .addMigrations(MIGRATION_1_2, MIGRATION_2_3)  // Ajouter les migrations
            .build()
        }

        val MIGRATION_1_2 = object : Migration(1, 2) {
            override fun migrate(db: SupportSQLiteDatabase) {
                db.execSQL("ALTER TABLE task ADD COLUMN description TEXT NULL")
            }
        }

        val MIGRATION_2_3 = object : Migration(2, 3) {
            override fun migrate(db: SupportSQLiteDatabase) {
                db.execSQL("ALTER TABLE task ADD COLUMN created_at INTEGER NULL")
            }
        }
    }
}
```

### Migrations Complexes

Certaines modifications ne peuvent pas être faites avec `ALTER TABLE` (renommer une colonne, changer un type). Il faut alors :

```kotlin
val MIGRATION_3_4 = object : Migration(3, 4) {
    override fun migrate(db: SupportSQLiteDatabase) {
        // 1. Créer une nouvelle table avec le bon schéma
        db.execSQL("""
            CREATE TABLE task_new (
                id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
                subject TEXT NOT NULL,
                place TEXT NOT NULL,
                description TEXT,
                created_at INTEGER,
                priority TEXT NOT NULL DEFAULT 'MEDIUM'
            )
        """)

        // 2. Copier les données
        db.execSQL("""
            INSERT INTO task_new (id, subject, place, description, created_at)
            SELECT id, subject, place, description, created_at FROM task
        """)

        // 3. Supprimer l'ancienne table
        db.execSQL("DROP TABLE task")

        // 4. Renommer la nouvelle table
        db.execSQL("ALTER TABLE task_new RENAME TO task")
    }
}
```

### Tester les Migrations

```kotlin
@RunWith(AndroidJUnit4::class)
class MigrationTest {

    @get:Rule
    val helper = MigrationTestHelper(
        InstrumentationRegistry.getInstrumentation(),
        TaskDatabase::class.java
    )

    @Test
    fun migrate1To2() {
        // Créer la base en version 1
        helper.createDatabase("test_db", 1).apply {
            execSQL("INSERT INTO task (id, subject, place) VALUES (1, 'Test', 'Home')")
            close()
        }

        // Migrer vers la version 2
        helper.runMigrationsAndValidate("test_db", 2, true, MIGRATION_1_2)

        // Vérifier que les données sont préservées
        val db = helper.openDatabase("test_db", 2)
        val cursor = db.query("SELECT * FROM task WHERE id = 1")
        assertTrue(cursor.moveToFirst())
        assertEquals("Test", cursor.getString(cursor.getColumnIndex("subject")))
    }
}
```

### Stratégie de Fallback

En développement, on peut accepter de perdre les données :

```kotlin
Room.databaseBuilder(context, TaskDatabase::class.java, "task_database")
    .fallbackToDestructiveMigration()  // Efface tout si migration impossible
    .build()
```

**ATTENTION** : Ne jamais utiliser en production !

> **Voir dans le projet :**
> - [`TaskDatabase.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TaskDatabase.kt) - Migrations `MIGRATION_1_2` et `MIGRATION_2_3` pour ajouter les colonnes `description` et `created_at`

---

## 22. Repository Pattern

### Pourquoi le Repository Pattern ?

Le **Repository** est une couche d'abstraction entre les sources de données et le reste de l'application.

```
┌───────────────────────────────────────────────────────────┐
│                      ViewModel                            │
│                          │                                │
│                          ▼                                │
│              ┌───────────────────────┐                    │
│              │     Repository        │ ◄── Interface      │
│              │     (Interface)       │                    │
│              └───────────┬───────────┘                    │
│                          │                                │
│          ┌───────────────┼───────────────┐                │
│          ▼               ▼               ▼                │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐       │
│  │   Offline    │ │    Online    │ │    Mock      │       │
│  │  Repository  │ │  Repository  │ │  Repository  │       │
│  │   (Room)     │ │  (Retrofit)  │ │   (Tests)    │       │
│  └──────────────┘ └──────────────┘ └──────────────┘       │
└───────────────────────────────────────────────────────────┘
```

### Avantages

1. **Abstraction** : Le ViewModel ne sait pas d'où viennent les données
2. **Flexibilité** : Facile de changer de source (locale → API)
3. **Testabilité** : Facile de mocker pour les tests
4. **Séparation des responsabilités** : Logique d'accès aux données isolée
5. **Single Source of Truth** : Une seule source de vérité pour les données

### Définir l'Interface

```kotlin
interface TasksRepository {

    // Lecture - Flow pour observation réactive
    fun getTasks(): Flow<List<Task>>
    fun getTaskById(id: Int): Flow<Task?>
    fun searchTasks(query: String): Flow<List<Task>>

    // Écriture - suspend pour opérations asynchrones
    suspend fun insertTask(task: Task)
    suspend fun updateTask(task: Task)
    suspend fun deleteTask(task: Task)

    // Opérations spéciales
    suspend fun refreshTasks()  // Pour les repos en ligne
}
```

### Implémentation Offline (Room)

```kotlin
class OfflineTasksRepository(
    private val taskDao: TaskDao
) : TasksRepository {

    override fun getTasks(): Flow<List<Task>> {
        return taskDao.getAllTasks()
    }

    override fun getTaskById(id: Int): Flow<Task?> {
        return taskDao.getTaskById(id)
    }

    override fun searchTasks(query: String): Flow<List<Task>> {
        return taskDao.searchTasks(query)
    }

    override suspend fun insertTask(task: Task) {
        taskDao.insert(task)
    }

    override suspend fun updateTask(task: Task) {
        taskDao.update(task)
    }

    override suspend fun deleteTask(task: Task) {
        taskDao.delete(task)
    }

    override suspend fun refreshTasks() {
        // Pas nécessaire pour le mode offline
    }
}
```

### Implémentation Online (Retrofit)

```kotlin
class OnlineTaskRepository(
    private val ownerName: String
) : TasksRepository {

    private val apiService = RetrofitClient.instance
    private val _tasks = MutableStateFlow<List<Task>>(emptyList())

    override fun getTasks(): Flow<List<Task>> = _tasks.asStateFlow()

    override fun getTaskById(id: Int): Flow<Task?> {
        return _tasks.map { tasks -> tasks.find { it.id == id } }
    }

    override fun searchTasks(query: String): Flow<List<Task>> {
        return _tasks.map { tasks ->
            tasks.filter { it.subject.contains(query, ignoreCase = true) }
        }
    }

    override suspend fun insertTask(task: Task) {
        val dto = CreateTaskDto(
            subject = task.subject,
            place = task.place,
            description = task.description,
            owner = ownerName
        )

        val createdDto = apiService.createTask(dto)
        val createdTask = createdDto.toTask()

        // Mise à jour du cache local
        _tasks.value = _tasks.value + createdTask
    }

    override suspend fun deleteTask(task: Task) {
        apiService.deleteTask(task.id)
        _tasks.value = _tasks.value.filter { it.id != task.id }
    }

    override suspend fun refreshTasks() {
        try {
            val taskDtos = apiService.getTasks()
            _tasks.value = taskDtos
                .filter { it.owner == ownerName }
                .map { it.toTask() }
        } catch (e: Exception) {
            Log.e("OnlineTaskRepository", "Error refreshing tasks", e)
            throw e
        }
    }

    override suspend fun updateTask(task: Task) {
        // Implémentation...
    }
}
```

### Choisir l'Implémentation

```kotlin
class MyCampusTasksApplication : Application() {

    private val USE_ONLINE = true
    private val OWNER_NAME = "victor"

    val tasksRepository: TasksRepository by lazy {
        if (USE_ONLINE) {
            OnlineTaskRepository(OWNER_NAME)
        } else {
            OfflineTasksRepository(TaskDatabase.getDatabase(this).taskDao())
        }
    }
}
```

### Permissions Réseau

Dans `AndroidManifest.xml` :

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- Permission Internet -->
    <uses-permission android:name="android.permission.INTERNET"/>

    <!-- Permission pour vérifier l'état du réseau -->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

    <application ...>
        ...
    </application>
</manifest>
```

> **Voir dans le projet :**
> - [`TasksRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TasksRepository.kt) - Interface Repository
> - [`OfflineTasksRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/OfflineTasksRepository.kt) - Implémentation avec Room (mode offline)
> - [`OnlineTaskRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/OnlineTaskRepository.kt) - Implémentation avec Retrofit (mode online)
> - [`MyCampusTasksApplication.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MyCampusTasksApplication.kt) - Choix dynamique de l'implémentation

---

## 23. Application Singleton

### Qu'est-ce que la Classe Application ?

La classe `Application` est un singleton qui représente l'application Android elle-même. Elle est créée avant toute Activity et reste vivante tant que l'app tourne.

```kotlin
class MyCampusTasksApplication : Application() {

    // Appelée une seule fois au démarrage de l'app
    override fun onCreate() {
        super.onCreate()
        // Initialisation globale
    }
}
```

### Déclarer dans le Manifest

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <application
        android:name=".MyCampusTasksApplication"  <!-- IMPORTANT -->
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.MyCampusTasks">

        <activity android:name=".MainActivity" ... />
    </application>
</manifest>
```

### Utilisation pour les Dépendances Globales

```kotlin
class MyCampusTasksApplication : Application() {

    // Préférences de l'utilisateur
    private val sharedPreferences by lazy {
        getSharedPreferences("app_prefs", Context.MODE_PRIVATE)
    }

    // Mode online/offline
    private val USE_ONLINE_KEY = "use_online"
    private val OWNER_NAME = "victor"

    // Repository exposé comme StateFlow pour réagir aux changements
    private val _currentRepository = MutableStateFlow<TasksRepository?>(null)
    val currentRepository: StateFlow<TasksRepository?> = _currentRepository.asStateFlow()

    // Accès direct au repository (pour la compatibilité)
    val tasksRepository: TasksRepository
        get() = _currentRepository.value ?: createRepository(isUseOnline())

    override fun onCreate() {
        super.onCreate()
        // Initialise le repository au démarrage
        _currentRepository.value = createRepository(isUseOnline())
    }

    // Crée le bon repository selon le mode
    private fun createRepository(useOnline: Boolean): TasksRepository {
        return if (useOnline) {
            OnlineTaskRepository(OWNER_NAME)
        } else {
            OfflineTasksRepository(TaskDatabase.getDatabase(this).taskDao())
        }
    }

    // Lecture du mode actuel
    fun isUseOnline(): Boolean {
        return sharedPreferences.getBoolean(USE_ONLINE_KEY, true)
    }

    // Changement de mode avec recréation du repository
    fun setUseOnline(useOnline: Boolean) {
        sharedPreferences.edit().putBoolean(USE_ONLINE_KEY, useOnline).apply()
        _currentRepository.value = createRepository(useOnline)
    }
}
```

### Accès depuis un Composable

```kotlin
@Composable
fun MyScreen() {
    val context = LocalContext.current
    val application = context.applicationContext as MyCampusTasksApplication

    // Accès au repository
    val repository = application.tasksRepository

    // Observer le changement de repository
    val currentRepo by application.currentRepository.collectAsState()
}
```

### Lazy Initialization

Le pattern `by lazy` est utilisé pour initialiser les objets seulement quand ils sont accédés pour la première fois :

```kotlin
class MyCampusTasksApplication : Application() {

    // Initialisé seulement au premier accès
    val database: TaskDatabase by lazy {
        TaskDatabase.getDatabase(this)
    }

    val tasksRepository: TasksRepository by lazy {
        OfflineTasksRepository(database.taskDao())
    }
}
```

**Avantages :**
- Démarrage plus rapide de l'app
- Ressources créées seulement si nécessaires
- Thread-safe par défaut

> **Voir dans le projet :**
> - [`MyCampusTasksApplication.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MyCampusTasksApplication.kt) - Singleton Application avec gestion des préférences et repository
> - [`AndroidManifest.xml`](app/src/main/AndroidManifest.xml) - Déclaration de la classe Application dans le manifest

---

## 24. Retrofit - Appels Réseau

### Qu'est-ce que Retrofit ?

Retrofit est une bibliothèque qui transforme une API HTTP en interface Kotlin/Java.

### Configuration du Client

```kotlin
object RetrofitClient {

    private const val BASE_URL = "https://mycampustasks.k8s.iut-larochelle.fr/api/"

    // Configuration OkHttp
    private val okHttpClient: OkHttpClient by lazy {
        OkHttpClient.Builder()
            // Intercepteur pour les logs (debug)
            .addInterceptor(HttpLoggingInterceptor().apply {
                level = HttpLoggingInterceptor.Level.BODY
            })
            // Intercepteur pour ajouter des headers
            .addInterceptor { chain ->
                val request = chain.request().newBuilder()
                    .addHeader("Accept", "application/json")
                    .addHeader("Content-Type", "application/json")
                    .build()
                chain.proceed(request)
            }
            // Timeouts
            .connectTimeout(30, TimeUnit.SECONDS)
            .readTimeout(30, TimeUnit.SECONDS)
            .writeTimeout(30, TimeUnit.SECONDS)
            .build()
    }

    // Instance Retrofit (singleton)
    val instance: TaskApiService by lazy {
        Retrofit.Builder()
            .baseUrl(BASE_URL)
            .client(okHttpClient)
            .addConverterFactory(GsonConverterFactory.create())
            .build()
            .create(TaskApiService::class.java)
    }
}
```

### Définir l'Interface API

```kotlin
interface TaskApiService {

    // GET - Récupérer toutes les tâches
    @GET("tasks")
    suspend fun getTasks(): List<TaskDto>

    // GET - Récupérer une tâche par ID
    @GET("tasks/{id}")
    suspend fun getTaskById(@Path("id") id: Int): TaskDto

    // GET - Rechercher avec query parameter
    @GET("tasks")
    suspend fun searchTasks(@Query("search") query: String): List<TaskDto>

    // POST - Créer une tâche
    @POST("tasks")
    suspend fun createTask(@Body task: CreateTaskDto): TaskDto

    // PUT - Mettre à jour une tâche
    @PUT("tasks/{id}")
    suspend fun updateTask(
        @Path("id") id: Int,
        @Body task: UpdateTaskDto
    ): TaskDto

    // DELETE - Supprimer une tâche
    @DELETE("tasks/{id}")
    suspend fun deleteTask(@Path("id") id: Int)

    // POST avec FormUrlEncoded
    @FormUrlEncoded
    @POST("login")
    suspend fun login(
        @Field("username") username: String,
        @Field("password") password: String
    ): AuthResponse
}
```

### Data Transfer Objects (DTOs)

Les DTOs représentent les données échangées avec l'API :

```kotlin
// DTO pour la lecture (depuis l'API)
data class TaskDto(
    @SerializedName("id")
    val id: Int,

    @SerializedName("subject")
    val subject: String,

    @SerializedName("place")
    val place: String,

    @SerializedName("description")
    val description: String?,

    @SerializedName("owner")
    val owner: String,

    @SerializedName("created_at")
    val createdAt: String?  // Format ISO 8601
) {
    // Conversion vers le modèle local
    fun toTask(): Task {
        return Task(
            id = id,
            subject = subject,
            place = place,
            description = description,
            createdAt = createdAt?.let { parseDate(it) }
        )
    }

    private fun parseDate(dateString: String): Date? {
        return try {
            SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", Locale.US).parse(dateString)
        } catch (e: Exception) {
            null
        }
    }
}

// DTO pour la création (vers l'API)
data class CreateTaskDto(
    @SerializedName("subject")
    val subject: String,

    @SerializedName("place")
    val place: String,

    @SerializedName("description")
    val description: String?,

    @SerializedName("owner")
    val owner: String
)
```

### Utilisation dans le Repository

```kotlin
class OnlineTaskRepository(private val ownerName: String) : TasksRepository {

    private val apiService = RetrofitClient.instance
    private val _tasks = MutableStateFlow<List<Task>>(emptyList())

    override fun getTasks(): Flow<List<Task>> = _tasks.asStateFlow()

    override fun getTaskById(id: Int): Flow<Task?> {
        return _tasks.map { tasks -> tasks.find { it.id == id } }
    }

    override fun searchTasks(query: String): Flow<List<Task>> {
        return _tasks.map { tasks ->
            tasks.filter { it.subject.contains(query, ignoreCase = true) }
        }
    }

    override suspend fun insertTask(task: Task) {
        val dto = CreateTaskDto(
            subject = task.subject,
            place = task.place,
            description = task.description,
            owner = ownerName
        )

        val createdDto = apiService.createTask(dto)
        val createdTask = createdDto.toTask()

        // Mise à jour du cache local
        _tasks.value = _tasks.value + createdTask
    }

    override suspend fun deleteTask(task: Task) {
        apiService.deleteTask(task.id)
        _tasks.value = _tasks.value.filter { it.id != task.id }
    }

    override suspend fun refreshTasks() {
        try {
            val taskDtos = apiService.getTasks()
            _tasks.value = taskDtos
                .filter { it.owner == ownerName }
                .map { it.toTask() }
        } catch (e: Exception) {
            Log.e("OnlineTaskRepository", "Error refreshing tasks", e)
            throw e
        }
    }

    override suspend fun updateTask(task: Task) {
        // Implémentation...
    }
}
```

### Permissions Réseau

Dans `AndroidManifest.xml` :

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- Permission Internet -->
    <uses-permission android:name="android.permission.INTERNET"/>

    <!-- Permission pour vérifier l'état du réseau -->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

    <application ...>
        ...
    </application>
</manifest>
```

> **Voir dans le projet :**
> - [`RetrofitClient.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/api/RetrofitClient.kt) - Configuration du client Retrofit avec OkHttp
> - [`TaskApiService.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/api/TaskApiService.kt) - Interface définissant les endpoints de l'API
> - [`TaskDto.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/api/TaskDto.kt) - Data Transfer Objects (DTOs) pour l'API
> - [`OnlineTaskRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/OnlineTaskRepository.kt) - Utilisation de Retrofit dans le repository
> - [`AndroidManifest.xml`](app/src/main/AndroidManifest.xml) - Permission INTERNET

---

## 25. Patterns Architecturaux

### Récapitulatif des Patterns Utilisés

| Pattern | Description | Implémentation |
|---------|-------------|----------------|
| **MVVM** | Model-View-ViewModel | `TaskViewModel` + Composables + `Task` |
| **Repository** | Abstraction des sources de données | `TasksRepository` interface |
| **Singleton** | Instance unique | `TaskDatabase`, `RetrofitClient`, `Application` |
| **Factory** | Création d'objets avec dépendances | `TaskViewModelFactory` |
| **Observer** | Notification des changements | `StateFlow`, `Flow`, `collectAsState` |
| **UDF** | Unidirectional Data Flow | État descend, événements remontent |
| **Backing Property** | Encapsulation de l'état mutable | `_mutableState` / `state` |
| **Dependency Injection** | Injection des dépendances | Factory, Application |

### Architecture Complète

```
┌─────────────────────────────────────────────────────────────────────┐
│                              UI LAYER                               │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                      Composables                            │    │
│  │  HomeScreen, TaskInput, TaskList, TaskItem                  │    │
│  │  (État reçu via paramètres, événements émis via callbacks)  │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                              │                                      │
│                    collectAsState()                                 │
│                              │                                      │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                      ViewModel                              │    │
│  │  - Expose StateFlow (subject, place, tasks)                 │    │
│  │  - Méthodes métier (addTask, removeTask)                    │    │
│  │  - viewModelScope pour les coroutines                       │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                              │                                      │
│                    Interface Repository                           │
│                              │                                      │
┌─────────────────────────────────────────────────────────────────────┐
│                           DATA LAYER                                │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    TasksRepository                          │    │
│  │  (Interface : getTasks, insertTask, deleteTask)             │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                    │                        │                       │
│        ┌──────────┴──────────┐   ┌─────────┴──────────┐             │
│        │OfflineTasksRepository│   │OnlineTaskRepository│             │
│        │      (Room)         │   │    (Retrofit)      │             │
│        └──────────┬──────────┘   └─────────┬──────────┘             │
│                   │                        │                        │
│           ┌───────┴───────┐        ┌───────┴───────┐                │
│           │   TaskDao     │        │TaskApiService │                │
│           └───────┬───────┘        └───────┬───────┘                │
│                   │                        │                        │
│           ┌───────┴───────┐        ┌───────┴───────┐                │
│           │ TaskDatabase  │        │RetrofitClient │                │
│           │   (SQLite)    │        │   (HTTP)      │                │
│           └───────────────┘        └───────────────┘                │
└─────────────────────────────────────────────────────────────────────┘
```

### Bonnes Pratiques Retenues

1. **Séparation des responsabilités**
   - UI : Affichage uniquement
   - ViewModel : Logique métier et état
   - Repository : Accès aux données
   - Database/API : Stockage

2. **Immutabilité**
   - Exposer des `StateFlow` (pas `MutableStateFlow`)
   - Utiliser des `data class` immuables
   - Créer de nouvelles listes au lieu de modifier

3. **Composables réutilisables**
   - Préférer les composables stateless
   - Remonter l'état (state hoisting)
   - Paramètre `Modifier` avec valeur par défaut

4. **Gestion des erreurs**
   - Try/catch dans les coroutines
   - États d'erreur dans le ViewModel
   - Messages utilisateur appropriés

5. **Performance**
   - `LazyColumn` pour les longues listes
   - `remember` pour les calculs coûteux
   - Éviter les recompositions inutiles

6. **Testabilité**
   - Interfaces pour les dépendances
   - Injection via Factory
   - Composables découplés de la logique

> **Voir dans le projet :**
> - [`TaskViewModel.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModel.kt) - ViewModel avec StateFlow et coroutines
> - [`TaskViewModelFactory.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/viewmodel/TaskViewModelFactory.kt) - Factory pour l'injection de dépendances
> - [`TasksRepository.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/model/TasksRepository.kt) - Interface Repository Pattern
> - [`HomeScreen.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/ui/home/HomeScreen.kt) - Composable écran avec UDF
> - [`MyCampusTasksApplication.kt`](app/src/main/java/iutlr/butinfo3/devbdmob/mycampustasks/MyCampusTasksApplication.kt) - Application Singleton

