# Collaboration & Performance d'Équipe

## I. Fondations : Du Groupe à l'Équipe

### Distinction Groupe vs Équipe

* **Groupe** : Objectifs individuels, addition des forces, réussites personnelles.
* **Équipe** : **Objectif commun**, **responsabilité mutuelle**, réussite/échec **collectif**.

### Caractéristiques d'une Équipe Performante

* Cadre de collaboration structuré
* **Valeurs partagées** (motivation et engagement)
* **Confiance** et sécurité psychologique
* Gestion constructive des conflits

## II. Modèle de Tuckman : Évolution d'Équipe

1. **Forming** : Politesse, dépendance au leader
2. **Storming** : Conflits nécessaires, lutte pour le pouvoir
3. **Norming** : Règles établies (DOD, chartes), cohésion
4. **Performing** : Autonomie, focus sur l'objectif
5. **Adjourning** : Clôture, célébration

## III. L'Équipe Agile Idéale

### Structure et Compétences

* **Petite taille** : < 10 personnes
* **Pluridisciplinaire** : Toutes compétences pour livrer end-to-end
* **Profils en T** : Expertise forte + compétences larges
* **Stabilité** : Changements = rupture d'équilibre

### Fonctionnement

* **Auto-organisation** : L'équipe décide du qui/quoi/quand/comment
* **Empowerment** : Confiance et délégation d'autorité
* **Propriété collective** : Succès par l'entraide

## IV. Rôles Scrum

### 🎭 Product Owner (PO) - Le Visionnaire

**Mission :** Maximiser la **valeur du produit**.

**Responsabilités :**
- 📋 Gestion du Product Backlog (définir, ordonner, prioriser, affiner)
- 🎯 Vision produit et roadmap stratégique
- 💼 Interface avec les stakeholders
- ✅ Validation des incréments (Sprint Review)
- 💰 Arbitrage coût/valeur/délai

**Anti-Patterns :**
❌ Proxy PO, PO absent, Micro-management, Comité de PO

### 🤝 Scrum Master (SM) - Le Servant Leader

**Mission :** Garantir que Scrum est **compris et appliqué** correctement.

**Responsabilités :**
- 🎓 Coach agile : Former, faciliter l'auto-organisation, promouvoir l'amélioration continue
- 📅 Facilitateur : Animer les cérémonies, gérer les conflits, maintenir le focus
- 🛡️ Gardien du processus : Protéger l'équipe, respecter les time-boxes et la DOD
- 🔧 Obstacle Remover : Identifier et retirer les blocages
- 🏢 Support organisationnel : Former, accompagner la transformation agile

**Ce que le SM N'EST PAS :**
❌ Chef de projet, Secrétaire, Bouche-trou, Intermédiaire obligatoire

### 💻 Développeurs - Les Créateurs de Valeur

**Mission :** Créer un **incrément "Done"** livrable à chaque sprint.

**Responsabilités :**
- 📋 Engagement : Participer au planning, estimer, s'engager sur le Sprint Goal
- 💻 Développement : Code propre, testé, documenté, code reviews
- 🤝 Collaboration : Pair/mob programming, Daily Scrum, entraide
- 💡 Amélioration : Rétrospectives actives, formation continue, réduction dette technique

**Taille :** 3 à 9 développeurs (Front, Back, Full-Stack, QA, UX/UI, DevOps, Architectes)

### 🔄 Cérémonies Scrum

| Cérémonie | Durée Max | Participants | Objectif |
|-----------|-----------|--------------|----------|
| **Sprint Planning** | 8h (1 mois) | Scrum Team | Planifier le Sprint |
| **Daily Scrum** | 15 min | Développeurs | Synchronisation |
| **Sprint Review** | 4h (1 mois) | Team + Stakeholders | Inspecter l'incrément |
| **Retrospective** | 3h (1 mois) | Scrum Team | Améliorer le processus |
| **Backlog Refinement** | ~10% sprint | PO + Développeurs | Affiner les PBI |

**Note :** Sprint de 2 semaines = diviser les durées par 2.

### 📦 Artefacts Scrum

**Product Backlog** : Liste ordonnée des besoins | **Engagement :** Product Goal  
**Sprint Backlog** : PBI sélectionnés + plan | **Engagement :** Sprint Goal  
**Incrément** : Somme des PBI "Done" | **Engagement :** Definition of Done

### 📊 Flux Kanban : Visualiser et Optimiser

#### Principes Kanban

1. **Commencer par ce que vous faites** : Évolution incrémentale, pas de révolution
2. **Changement incrémental** : Amélioration continue (Kaizen)
3. **Respecter les processus actuels** : Pas de remise en question brutale
4. **Leadership à tous niveaux** : Tout le monde peut proposer des améliorations

#### Les 6 Pratiques Kanban

**1. Visualiser le Flux**

```
┌──────────┬──────────┬──────────┬──────────┬──────────┐
│ To Do    │ In       │ Code     │ Testing  │ Done     │
│          │ Progress │ Review   │          │          │
│          │ (WIP:3)  │ (WIP:2)  │ (WIP:2)  │          │
└──────────┴──────────┴──────────┴──────────┴──────────┘
```

**2. Limiter le WIP (Work In Progress)**

> "Stop Starting, Start Finishing"

**Pourquoi ?**
- 🐌 Loi de Little : Lead Time = WIP / Throughput
- 🧠 Multitâche réduit la productivité de 40%
- 🎯 Focus : Finir avant de commencer
- 🚨 Détection rapide des problèmes

**Quand WIP atteint :**
✅ Aider un collègue | ✅ Code reviews | ✅ Tests | ✅ Réduire dette technique | ❌ NE PAS commencer nouvelle tâche

**3. Gérer le Flux**
- Mesurer : Lead Time, Cycle Time, Throughput
- Identifier les goulets d'étranglement
- Optimiser

**4. Règles Explicites**
- Definition of Done par colonne
- Critères de passage clairs

**5. Boucles de Feedback**
- Daily, Review, Rétrospective, Metrics Review

**6. Améliorer Collaborativement**
- Hypothèses → Expérimentation → Mesure → Adoption/Abandon

### 📐 Scrum + Kanban = Scrumban

| Aspect | Scrum | Kanban | Scrumban |
|--------|-------|--------|----------|
| **Rôles** | PO, SM, Dev Team | Pas de rôles imposés | Rôles Scrum maintenus |
| **Itérations** | Sprints time-boxed | Flow continu | Sprints + flux visualisé |
| **Planification** | Sprint Planning | À la demande (pull) | Sprint Planning + limite WIP |
| **Engagement** | Sur le sprint | Sur la prochaine tâche | Mix des deux |
| **Métriques** | Vélocité, Burndown | Lead Time, Cycle Time | Les deux |
| **Changement** | Pas en cours de sprint | Possible à tout moment | Négocié |

---

## V. Les 5 Dysfonctionnements de Lencioni

### 🎯 Concept Clé

Patrick Lencioni identifie cinq obstacles majeurs qui empêchent une équipe d'être efficace, présentés sous forme de **pyramide inversée**. Chaque dysfonctionnement est la base du suivant.

```
        🏆 Résultats Collectifs
              ↑ Bloqué par
        ⚠️ Inattention aux Résultats
              ↑ Bloqué par
      🙈 Évitement des Responsabilités
              ↑ Bloqué par
        💭 Manque d'Engagement
              ↑ Bloqué par
          😱 Peur du Conflit
              ↑ Bloqué par
        🚫 Absence de Confiance
```

### 1️⃣ Absence de Confiance

**Définition :** Incapacité à se montrer **vulnérable**. Peur d'admettre erreurs, faiblesses ou besoins d'aide.

**🚨 Signes :** Erreurs cachées, pas de demande d'aide, réunions superficielles, rumeurs, jugements rapides

**💡 Exemples :**
- ❌ Daily : "Tout va bien" (bloqué depuis 2 jours)
- ✅ Daily : "Je suis bloqué, j'ai besoin d'aide"

**🔧 Solutions :**
1. **Exercices de Vulnérabilité** : Partage d'histoires personnelles, erreurs passées
2. **Profiling d'Équipe** : Tests MBTI, DISC, cartographie forces/faiblesses
3. **Pratiques Quotidiennes** : Leader montre l'exemple, normaliser "Je ne sais pas", célébrer échecs
4. **Temps Informel** : Pauses café, déjeuners, team building

### 2️⃣ Peur du Conflit

**Définition :** Recherche d'**harmonie artificielle** empêchant les débats d'idées productifs.

**🚨 Signes :** Réunions ennuyeuses, accord de façade, back-channel, sujets évités, fausse gentillesse

**💡 Distinction Cruciale :**
- ✅ **Conflit d'Idées** : Débat sur approches/solutions → Meilleures décisions
- ❌ **Conflit Personnel** : Attaques personnelles → Toxicité

**Exemples :**
- ✅ "Ton approche REST est moins performante que GraphQL. Voici mes arguments..."
- ❌ "Tu proposes toujours des solutions sur-complexes pour briller !"

**🔧 Solutions :**
1. **Reconnaissance** : "Le désaccord est attendu et bienvenu"
2. **Techniques** : Avocat du diable, Six Thinking Hats, Round Robin
3. **Permission Explicite** : "Je vais challenger cette idée..."
4. **Temps Dédié** : 30 min de débat critique pour décisions importantes
5. **Mining for Conflict** : SM verbalise les désaccords non-exprimés

**🎭 Rôle du Leader :**
- ✅ Accepter les challenges sur ses idées
- ✅ Intervenir si conflit devient personnel
- ❌ Ne pas résoudre les conflits trop vite

### 3️⃣ Manque d'Engagement

**Définition :** Ambiguïté sur les décisions car tout le monde n'a pas pu s'exprimer.

**⚠️ Important :** Engagement ≠ consensus. Nécessite : expression, écoute, clarté, soutien de la décision.

**🚨 Signes :** Ambiguïté, réouverture constante de sujets, désalignement, "J'ai jamais dit que j'étais d'accord"

**💡 Exemple :**
- ❌ Sans : "On fera un mix..." → 2 semaines après : "Mais j'avais compris microservices !"
- ✅ Avec : Débat 2h → Décision claire "monolithe modulaire" → Jean : "Pas convaincu mais je m'engage"

**🔧 Solutions :**
1. **Disagree and Commit** : "Tu n'es pas d'accord, mais peux-tu t'engager ?"
2. **Clarté Absolue** : Décision documentée (Quoi, Pourquoi, Quand, Qui), ADR
3. **Deadline** : "On décide avant vendredi"
4. **Worst Case Analysis** : "Quel est le pire ? Peut-on revenir en arrière ?"
5. **Cascading Messages** : Chacun communique la décision
6. **Thematic Goals** : 1-3 priorités absolues, dire NON au reste

**📊 Test :** "Quelle décision ?" "Es-tu d'accord ?" "T'engages-tu quand même ?" "Que diras-tu à ton équipe ?"

### 4️⃣ Évitement des Responsabilités (Accountability)

**Définition :** Tolérance de standards médiocres. Les membres ne se tiennent pas mutuellement responsables.

**🚨 Signes :** Seul le leader rappelle les règles, baisse de performance tolérée, "Pas mon problème"

**💡 Distinction :**
- **Accountability** : Tenu responsable (par les autres) - Externe
- **Responsibility** : Se sentir responsable - Interne

**Exemples :**
- ❌ Marie livre sans tests (3e fois) → Équipe silencieuse → SM intervient
- ✅ Jean : "Marie, on s'était engagés sur 80% coverage. Tu as besoin d'aide ?"

**🔧 Solutions :**
1. **Standards Publics** : DOD visible, métriques partagées, Sprint Goals clairs
2. **Feedback de Pair à Pair** : 1-on-1, code reviews rigoureuses, feedback immédiat
3. **Publication Progrès** : Burndown visible, état stories affiché
4. **Peer Pressure Positif** : Reconnaissance, mob/pair programming, kudos
5. **Rétrospectives Honnêtes** : Comportements problématiques, action items
6. **Contrats d'Équipe** : Charte signée, conséquences claires

**🎭 Leader :** Encourager accountability entre pairs, modeler le comportement, intervenir uniquement si chronique

### 5️⃣ Inattention aux Résultats

**Définition :** Focalisation sur **ego/carrière individuelle** au lieu du succès collectif.

**🚨 Signes :** "J'ai fini mes tâches" (Sprint Goal raté), recherche mérite individuel, "Pas mon problème"

**💡 Faux Objectifs :**
- Statut individuel vs Succès produit
- Ego technique vs Valeur utilisateur
- Harmonie à tout prix vs Objectifs atteints
- Processus parfait vs Impact business

**Exemples :**
- ❌ Jean finit son API : "Si le front est pas prêt, pas mon problème" → Sprint Goal raté
- ✅ Jean : "Mon API est prête, j'aide Sophie sur le front pour finir le Sprint Goal"

**🔧 Solutions :**
1. **Objectifs Collectifs** : Sprint Goal binaire, OKRs d'équipe
2. **Métriques Résultats** : Impact business, NPS, adoption (PAS lignes de code)
3. **Récompenses Collectives** : Bonus d'équipe, "L'équipe X a livré..."
4. **Déclaration Publique** : Sprint Goal affiché, red flag si menacé
5. **Rétrospectives Résultats** : "Avons-nous atteint le Sprint Goal ?"
6. **Conséquences Partagées** : Succès/échec de toute l'équipe, post-mortem blameless

**🎯 Questions :** "Quel objectif ?" "Sommes-nous en train de l'atteindre ?" "Comment mesure-t-on notre succès ?"

### 📊 Tableau Récapitulatif : Les 5 Dysfonctionnements

| Dysfonctionnement | Origine / Symptôme | Solution de Lencioni | Pratiques Concrètes |
| --- | --- | --- | --- |
| **1. Absence de Confiance** | Peur d'être vulnérable, de demander de l'aide ou d'admettre ses erreurs | Encourager la vulnérabilité, partager des expériences personnelles | Personal histories, profiling, leader montre l'exemple |
| **2. Peur du Conflit** | Recherche d'harmonie artificielle ; évitement des débats d'idées productifs | Reconnaître que le conflit d'idées est nécessaire et sain | Avocat du diable, mining for conflict, permission explicite |
| **3. Manque d'Engagement** | Ambiguïté sur les décisions car tout le monde n'a pas pu s'exprimer | Viser la clarté et l'adhésion (même sans consensus total) | Disagree & commit, ADR, cascading messages |
| **4. Évitement des Responsabilités** | Tolérance de standards médiocres ; on ne se tient pas mutuellement pour responsables | Établir des normes claires et se rappeler les objectifs communs | DOD visible, feedback pairs, publication progrès |
| **5. Inattention aux Résultats** | Focalisation sur l'ego, la carrière ou les objectifs personnels au lieu du collectif | Se concentrer uniquement sur les succès de l'équipe | Sprint Goals clairs, métriques business, récompenses collectives |


### 🔄 Interdépendance des Dysfonctionnements

**Important** : Les dysfonctionnements sont interdépendants et cumulatifs :

```
Sans CONFIANCE → Impossible d'avoir des CONFLITS sains
Sans CONFLITS → Impossible d'avoir un vrai ENGAGEMENT
Sans ENGAGEMENT → Impossible d'avoir de l'ACCOUNTABILITY
Sans ACCOUNTABILITY → Impossible de se focaliser sur les RÉSULTATS
```

**Implication pratique :** Il faut traiter les dysfonctionnements **dans l'ordre**, en commençant par la base (confiance).


## VI. La Psychologie de la Responsabilité

### 1. Accountability vs Responsibility

* **Accountability** : Capacité à rendre des comptes. C'est souvent une **obligation** liée à un rôle (devoir).
* **Responsibility** : Sentiment d'appropriation d'une situation. C'est un **choix** et une liberté d'agir.

### 2. Le Processus de Responsabilité (Christopher Avery)

Face à un problème, notre cerveau suit un processus mental automatique. L'objectif est de franchir les étapes pour atteindre la "Responsabilité".

* **Déni** : Ignorer le problème.
* **Accusation** : Blâmer les autres.
* **Justification** : Blâmer les circonstances ("On a toujours fait comme ça").
* **Culpabilité / Honte** : S'auto-flageller (état passif, pas de solution).
* **Obligation** : Faire la tâche parce qu'on n'a "pas le choix" (désengagement).
* **Fuite** : Abandonner, se désengager totalement.
* **Responsabilité** : État où l'on se sent capable de traiter le problème et de choisir une solution.


## VII. Le Socle des Valeurs

Les valeurs individuelles et professionnelles sont le moteur de l'action.

* **Exercice de la Pyramide** : Identifier 6 valeurs clés (ex: Agilité, Bienveillance, Rigueur, Transparence), les comparer entre elles et les illustrer par des comportements concrets.
* **Impact** : Une équipe alignée sur des valeurs communes travaille avec plus de fluidité et de confiance.