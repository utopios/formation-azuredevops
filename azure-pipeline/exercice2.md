### Exercice : Pipeline Azure DevOps avec conditions

**Objectif**

Créer une pipeline Azure DevOps avec les fonctionnalités conditionnelles suivantes :
1.	Un stage de préparation qui exécute différentes actions en fonction de la branche (main, develop ou autre).
2.	Un stage de validation qui :
•	Ne s’exécute que si un fichier .sln est trouvé dans le dépôt.
•	Définit dynamiquement une variable contenant le chemin du fichier .sln.
3.	Un stage de déploiement qui :
•	S’exécute uniquement si la branche est main et si le stage de validation est réussi.
•	Inclut une étape pour déployer une application fictive avec un message de succès ou d’échec conditionnel.