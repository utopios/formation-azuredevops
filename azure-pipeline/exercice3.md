## Exercice : Pipeline Azure DevOps pour le dépôt ASP.NET Core Tests Sample

**Objectif**

Créer un pipeline Azure DevOps pour automatiser les étapes suivantes en utilisant le dépôt [giggio-samples/aspnetcore-tests-sample](https://github.com/giggio-samples/aspnetcore-tests-sample) :
1.	Restaurer les dépendances du projet.
2.	Compiler l’application ASP.NET Core.
3.	Exécuter les tests unitaires inclus dans le projet.
4.	Inclure des conditions pour :
•	Exécuter les tests uniquement si la compilation réussit.
•	Ne lancer la compilation et les tests que si la branche est main ou develop.