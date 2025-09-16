# Documentation de la base de données Terracoast

## 1. Introduction

La base de données Terracoast est conçue pour gérer efficacement toutes les données relatives à une plateforme de quiz géographiques avec profils utilisateurs, quiz multitypes, système de badges, notifications internes, modes compétitifs et sociaux, ainsi que gestion d’administrateurs. Elle utilise un modèle relationnel avec PostgreSQL.

***

## 2. Description des entités principales

### Utilisateur (User)

Représente un joueur ou un administrateur.  
Champs clés :  
- `id` : identifiant unique (UUID)  
- `username` : pseudo  
- `email` : adresse email (pour newsletter, réinitialisation)  
- `password_hash` : mot de passe stocké en hash sécurisé (ex. bcrypt)  
- `role` : rôle utilisateur (admin ou user) contrôlant les accès  
- `published_quiz_count` : nombre de quiz publics publiés (limité à 10)  
- `joined_at` : date d’inscription  

***

### Quiz

Contient un ensemble de questions.  
Champs clés :  
- `id` : identifiant unique  
- `author_id` : référence à l’utilisateur créateur  
- `title` et `description` : description textuelle  
- `published` : booléen indiquant si quiz visible publiquement  
- `created_at`, `updated_at` : timestamps  

***

### Question

Stocke une question individuelle liée à un quiz, adaptable à plusieurs types.  
Champs clés :  
- `id`  
- `quiz_id` : référence au quiz parent  
- `type` : type de question (texte libre, QCM, image, carte...)  
- `text` : texte de la question ou consigne  
- `media_url` : lien vers média (image par exemple), facultatif  

***

### Answer (Réponse)

Liste des réponses possibles ou attendues selon le type de question.  
Champs clés :  
- `id`  
- `question_id` : référence à la question  
- `text` : texte de la réponse (ou saisie attendue)  
- `is_correct` : booléen pour valider la/les bonnes réponse(s) (utile pour QCM)  

***

### Badge & Title (Récompenses)

Représentent distinctions graphiques attribuées aux utilisateurs selon leur progression ou rôles.  
Tables d’association `UserBadge` et `UserTitle` lient utilisateur à badges/titres avec date d’attribution.

***

### Friendship (Amis)

Gère les relations sociales entre utilisateurs avec statuts (« pending », « accepted »...). Permet duels et partages privés.

***

### Duel

Représente un duel entre deux joueurs sur un quiz donné, avec indication du gagnant, début et fin du duel.

***

### Leaderboard

Stocke les scores des joueurs par quiz, avec précision, temps et date de mise à jour pour classement et historique.

***

### PasswordResetToken

Gère les tokens sécurisés pour la réinitialisation du mot de passe, avec expiration et usage unique garanti.

***

## 3. Contraintes et règles métier

- Un utilisateur peut publier jusqu’à 10 quiz publics maximum, contrôlé par `published_quiz_count` et validation backend.  
- Les rôles administrateurs peuvent créer d’autres admins, gérer les quiz globaux et les utilisateurs.  
- Les mots de passe sont stockés hashés pour la sécurité, réinitialisables via email avec tokens temporaires.  
- La validation des réponses est immédiate dans l’interface utilisateur.  
- Notifications internes uniquement, sans envoi externe (email/push) pour simplicité MVP.  
- Interface mono-langue, pas de gestion multilingue dans le MVP.

***

## 4. Relations principales

- Un Utilisateur crée plusieurs Quiz.  
- Un Quiz contient plusieurs Questions.  
- Une Question peut avoir plusieurs Réponses (answers), dépendant du type.  
- Un Utilisateur peut recevoir plusieurs Badges et Titres.  
- Les relations d’amitié sont stockées avec statut et timestamps pour un historique complet.  
- Les Duels font référence aux deux participants, au quiz, et retiennent le vainqueur.  
- Le Leaderboard permet de suivre performances par utilisateur et quiz.  

***
