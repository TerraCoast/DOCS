## Authentification & Utilisateurs

- **POST** /auth/register  
  Inscription utilisateur (pseudo, email, mdp)  
- **POST** /auth/login  
  Connexion (email + mdp, retourne token JWT)  
- **POST** /auth/logout  
  Déconnexion (invalidation token côté client ou blacklist côté serveur)  
- **POST** /auth/password-reset-request  
  Demande de réinitialisation par email  
- **POST** /auth/password-reset  
  Réinitialisation via token + nouveau mdp  
- **GET** /users/me  
  Récupérer profil utilisateur connecté  
- **PATCH** /users/me  
  Mise à jour profil (pseudo, email, mdp)  
- **GET** /users/:id  
  Récupérer profil public d’un utilisateur

***

## Gestion des quiz

- **GET** /quizzes  
  Liste quiz publics (filtrage par type, popularité, date, etc.)  
- **GET** /quizzes/:id  
  Détails complet d’un quiz (questions, médias, auteurs)  
- **POST** /quizzes  
  Création quiz (user/admin)  
- **PATCH** /quizzes/:id  
  Modification quiz (seulement auteur/admin)  
- **DELETE** /quizzes/:id  
  Suppression quiz (seulement auteur/admin)  
- **POST** /quizzes/:id/publish  
  Publication quiz (vérifie limite 10 quiz pour utilisateur)  
- **GET** /users/:id/quizzes  
  Liste quiz créés par un utilisateur (publics + privés, selon droits)  

***

## Gestion des questions & réponses

- **POST** /quizzes/:quizId/questions  
  Ajouter question à un quiz  
- **PATCH** /questions/:id  
  Modifier question  
- **DELETE** /questions/:id  
  Supprimer question  
- **GET** /questions/:id/answers  
  Récupérer réponses possibles  
- **POST** /questions/:questionId/answers  
  Ajouter réponse  
- **PATCH** /answers/:id  
  Modifier réponse  
- **DELETE** /answers/:id  
  Supprimer réponse

***

## Gestion des types de questions (admin)

- **GET** /question-types  
  Liste tous les types de questions  
- **POST** /question-types  
  Créer type question (admin seulement)  
- **PATCH** /question-types/:id  
  Modifier type question (admin)  
- **DELETE** /question-types/:id  
  Supprimer type question (admin)

***

## Gestion des badges et titres

- **GET** /badges  
  Liste des badges  
- **POST** /badges  
  Création badge (admin)  
- **PATCH** /badges/:id  
  Modification badge (admin)  
- **DELETE** /badges/:id  
  Suppression badge (admin)

- **GET** /titles  
  Liste des titres  
- **POST** /titles  
  Création titre (admin)  
- **PATCH** /titles/:id  
  Modification titre (admin)  
- **DELETE** /titles/:id  
  Suppression titre (admin)

***

## Relations sociales & duels

- **GET** /friends  
  Liste amis de l’utilisateur connecté  
- **POST** /friends/:friendId  
  Envoyer demande d’amitié  
- **PATCH** /friends/:friendId  
  Accepter/refuser demande  
- **DELETE** /friends/:friendId  
  Supprimer ami

- **POST** /duels  
  Créer duel (avec quiz, joueur2)  
- **GET** /duels/:id  
  Récupérer état duel  
- **PATCH** /duels/:id  
  Mettre à jour (réponses, fin duel)  
- **GET** /users/:id/duels  
  Liste duels d’un utilisateur

***

## Leaderboards & scores

- **GET** /leaderboard/global  
  Classement mondial (tri par score, temps, précision)  
- **GET** /leaderboard/friends  
  Classement entre amis  
- **POST** /leaderboard  
  Poster un score après quiz/duel  
- **GET** /leaderboard/:quizId  
  Classement spécifique à un quiz  

***

## Administration (dashboard)

- **GET** /admin/users  
  Liste utilisateurs (admin seulement)  
- **PATCH** /admin/users/:id/role  
  Changer rôle utilisateur  
- **GET** /admin/reports  
  Liste signalements / problèmes  
- **PATCH** /admin/reports/:id  
  Résoudre/report gérer  

***

Cette liste de routes couvre toutes les fonctionnalités nécessaires à l’application Terracoast, du frontend vers le backend, avec gestion sécurisée, rôles, contenu dynamique, compétitions, social et administration.Voici une liste complète des routes API REST à implémenter pour couvrir toutes les fonctionnalités de l’application Terracoast :

## Authentification & utilisateurs
- POST /auth/register — inscription
- POST /auth/login — connexion
- POST /auth/logout — déconnexion
- POST /auth/password-reset-request — demande reset mot de passe
- POST /auth/password-reset — réinitialisation avec token
- GET /users/me — profil utilisateur connecté
- PATCH /users/me — modifier profil
- GET /users/:id — profil public utilisateur

## Gestion des quiz
- GET /quizzes — liste quiz publics
- GET /quizzes/:id — détail quiz complet
- POST /quizzes — créer quiz
- PATCH /quizzes/:id — modifier quiz
- DELETE /quizzes/:id — supprimer quiz
- POST /quizzes/:id/publish — publier quiz (limite contrôlée backend)
- GET /users/:id/quizzes — quiz créés par un utilisateur

## Questions & réponses
- POST /quizzes/:quizId/questions — ajouter question
- PATCH /questions/:id — modifier question
- DELETE /questions/:id — supprimer question
- GET /questions/:id/answers — réponses d’une question
- POST /questions/:questionId/answers — ajouter réponse
- PATCH /answers/:id — modifier réponse
- DELETE /answers/:id — supprimer réponse

## Types de questions (admin)
- GET /question-types — liste types questions
- POST /question-types — créer type question
- PATCH /question-types/:id — modifier type
- DELETE /question-types/:id — supprimer type

## Badges & titres
- GET /badges — liste badges
- POST /badges — création badge (admin)
- PATCH /badges/:id — modifier badge (admin)
- DELETE /badges/:id — supprimer badge (admin)
- GET /titles — liste titres
- POST /titles — créer titre (admin)
- PATCH /titles/:id — modifier titre (admin)
- DELETE /titles/:id — supprimer titre (admin)

## Relations sociales & duels
- GET /friends — liste amis
- POST /friends/:friendId — demande amitié
- PATCH /friends/:friendId — accepter/refuser
- DELETE /friends/:friendId — supprimer ami
- POST /duels — créer duel avec joueur & quiz
- GET /duels/:id — état duel
- PATCH /duels/:id — mise à jour duel
- GET /users/:id/duels — duels d’un utilisateur

## Leaderboards & scores
- GET /leaderboard/global — classement mondial
- GET /leaderboard/friends — classement amis
- POST /leaderboard — poster score
- GET /leaderboard/:quizId — classement quiz spécifique

## Administration
- GET /admin/users — liste utilisateurs (admin)
- PATCH /admin/users/:id/role — changer rôle
- GET /admin/reports — liste signalements
- PATCH /admin/reports/:id — gérer signalement
