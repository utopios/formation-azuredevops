# **Workshop Maîtriser Azure DevOps**

## **Objectifs**
- Gérer un backlog complexe avec des priorités et des dépendances.
- Organiser plusieurs projets à l’aide de collections de projet.
- Personnaliser les workflows pour répondre à des besoins spécifiques.
- Exploiter les work items liés pour assurer la traçabilité.
- Créer un Wiki collaboratif pour la documentation technique.

---

## **Scénario : Application de gestion de flotte de véhicules**
Vous travaillez sur une application de gestion de flotte de véhicules pour une entreprise de logistique. Le projet inclut plusieurs équipes :
- **Back-end** : API et base de données.
- **Front-end** : Interface utilisateur.
- **Testeurs** : Validation et débogage.

---

## **Workshop : Instructions étape par étape**

### **1. Gestion du backlog**
#### **Objectif** : Organiser un backlog avec des dépendances et priorités.

1. **Créer des éléments du backlog** :
   - Accédez à **Boards > Backlogs**.
   - Ajoutez les éléments suivants :
     - **Epic** : "Gestion des véhicules".
     - **Feature** : "Création de rapports de maintenance".
     - **User Story** : "Afficher les données de maintenance d’un véhicule."

2. **Prioriser et organiser** :
   - Attribuez une priorité (élevée, moyenne, faible) à chaque élément.
   - Reliez la User Story à la Feature via **Add Link > Parent**.

3. **Planifier dans un sprint** :
   - Allez dans **Sprints**.
   - Faites glisser les User Stories dans un sprint actif.

---

### **2. Gérer des collections de projet**
#### **Objectif** : Créer une collection pour regrouper plusieurs projets.

1. **Accéder aux collections** :
   - Dans **Organization Settings > Collections**, cliquez sur **New Collection**.

2. **Créer une collection** :
   - Nom : "Projets de gestion de flotte".
   - Définissez les paramètres SQL pour Azure DevOps Server si applicable.

3. **Ajouter des projets à la collection** :
   - Créez deux projets : "Back-end Fleet" et "Front-end Fleet".
   - Assurez-vous que les permissions permettent l’accès à tous les membres.

---

### **3. Modèles de processus et personnalisation**
#### **Objectif** : Adapter un modèle de processus existant à vos besoins.

1. **Personnaliser un modèle** :
   - Allez dans **Organization Settings > Process**.
   - Dupliquez le modèle **Agile** et renommez-le : "Gestion Flotte Custom".

2. **Ajouter un nouveau type de Work Item** :
   - Cliquez sur **New Work Item Type** et nommez-le "Analyse Technique".
   - Ajoutez des champs personnalisés comme "Responsable" et "Date d’échéance".

3. **Appliquer le modèle personnalisé** :
   - Retournez au projet et appliquez ce modèle via les paramètres.

---

### **4. Gestion avancée des work items**
#### **Objectif** : Créer et lier des work items complexes.

1. **Créer un Bug** :
   - Allez dans **Boards > Work Items**.
   - Cliquez sur **New Work Item > Bug**.
   - Ajoutez le titre : "Erreur de calcul des kilométrages".

2. **Relier les work items** :
   - Ouvrez la User Story "Afficher les données de maintenance d’un véhicule."
   - Cliquez sur **Add Link > Related Work** et reliez le Bug.

3. **Filtrer et rechercher** :
   - Appliquez des filtres pour afficher uniquement les Bugs ou User Stories.

---

### **5. Personnalisation des workflows**
#### **Objectif** : Modifier les états et transitions des workflows.

1. **Modifier un workflow** :
   - Accédez à **Organization Settings > Process > Gestion Flotte Custom**.
   - Cliquez sur le type **Bug**.
   - Ajoutez un nouvel état : "En analyse".

2. **Configurer une transition** :
   - Transition de **Nouveau** à **En analyse**.
   - Ajoutez une règle qui oblige à renseigner le champ "Responsable" avant de passer à l’état suivant.

3. **Tester le workflow** :
   - Retournez dans Boards, créez un Bug, et testez les transitions.

---

### **6. Utiliser les outils collaboratifs et Wiki**
#### **Objectif** : Documenter le projet et collaborer avec votre équipe.

1. **Créer un Wiki** :
   - Allez dans **Wiki** et cliquez sur **Create Wiki**.
   - Ajoutez une page intitulée "Architecture de l’application".

2. **Ajouter du contenu** :
   - Utilisez Markdown pour structurer :
     - Une section sur l’API (Endpoints, types de requêtes).
     - Une section sur les tests.

3. **Collaborer** :
   - Invitez des membres à commenter ou modifier le Wiki.
   - Suivez l’historique des modifications pour traçabilité.
