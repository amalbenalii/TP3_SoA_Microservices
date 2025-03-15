# Système de Gestion de Tâches avec GraphQL

##  Objectifs
-  Comprendre comment configurer et utiliser GraphQL avec Node.js et Express.
-  Apprendre à créer un schéma GraphQL et des résolveurs pour gérer les requêtes et mutations.
-  Créer une API simple pour la gestion des tâches.

##  Outils utilisés
-  **Node.js** : Environnement d'exécution JavaScript.
-  **Express** : Framework web léger pour Node.js.
-  **Apollo Server** : Serveur GraphQL performant pour Node.js.
-  **GraphQL** : Langage de requête pour les API.

### Qu'est-ce que **GraphQL** ? 
**GraphQL** est un langage de requête pour les API, permettant aux clients de récupérer uniquement les données dont ils ont besoin, ce qui le rend plus efficace que les API REST traditionnelles. Il permet également une meilleure gestion des mutations et des requêtes complexes.

---

## Étapes de Création 
###  Étape 1 : Installation et configuration
###  1. Installer Node.js
 - **Télécharger et installer Node.js depuis le site officiel.**
  
###  2. Cloner le dépôt
```bash
git clone <URL_DU_DEPOT>
cd TP3_SoA_Microservices

```

###  3. Installer les dépendances
```bash
npm install
npm init -y
npm install express @apollo/server body-parser @graphql-tools/schema graphql

```
---
##  Structure du projet
```
tp-graphql/
├── node_modules/          # Dépendances installées
├── taskSchema.gql         # Schéma GraphQL des tâches
├── taskSchema.js          # Implémentation du schéma GraphQL
├── taskResolver.js        # Résolveurs pour les requêtes et mutations
├── index.js               # Point d'entrée du serveur
├── package.json           # Fichier de configuration du projet
└── README.md              # Documentation du projet
```
---
##  Etape 2: Schéma GraphQL

Le schéma est défini dans `taskSchema.gql` :

```graphql
type Task {
  id: ID!
  title: String!
  description: String!
  completed: Boolean!
  duration: Int
}

type Query {
  task(id: ID!): Task
  tasks: [Task]
}

type Mutation {
  addTask(title: String!, description: String!, completed: Boolean!, duration: Int): Task
  completeTask(id: ID!): Task
  changeDescription(id: ID!, description: String!): Task
  deleteTask(id: ID!): Task
}
```
---
### Étape 3: Tester l'API avec GraphiQL 
1. Démarrer le serveur
- **Démarrer le serveur avec la commande :**
```bash
node index.js
```
2. Accéder à Apollo Sandbox via : `http://localhost:5000/graphql`


3. Tester les requêtes et mutations suivantes :

####  Récupérer toutes les tâches
```graphql
query {
  tasks {
    id
    title
    description
    completed
    duration
  }
}
```

####  Ajouter une nouvelle tâche
```graphql
mutation {
  addTask(title: "Nouvelle Tâche", description: "Description ici", completed: false, duration: 5) {
    id
    title
    description
    completed
    duration
  }
}
```

####  Marquer une tâche comme terminée
```graphql
mutation {
  completeTask(id: "1") {
    id
    title
    completed
  }
}
```

####  Modifier la description d'une tâche
```graphql
mutation {
  changeDescription(id: "1", description: "Nouvelle description") {
    id
    title
    description
  }
}
```

####  Supprimer une tâche
```graphql
mutation {
  deleteTask(id: "1") {
    id
    title
  }
}
```

---


