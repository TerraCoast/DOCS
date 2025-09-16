# Cahier des charges – Terracoast

## Contexte et objectif

Terracoast est une application web de quiz géographiques compétitifs destinée aux amateurs de géographie, professeurs, élèves ou simples curieux. L'objectif est de proposer des quiz variés autour des drapeaux, capitales et cartes du monde, avec des modes compétitifs innovants, un système social et des fonctionnalités avancées de classement et de personnalisation des profils.

## Fonctionnalités clés

### Profil utilisateur
- Création de compte (pseudo, email pour newsletter, mot de passe hashé).
- Accès à son profil, affichage du niveau, des titres, badges, historique de parties et leaderboard.
- Droit de publier jusqu’à **10 quiz publics** maximum.
- Réinitialisation de mot de passe par email avec token sécurisé.

### Rôles et administration
- Rôles : Utilisateur, Admin.
- Les admins peuvent créer des comptes admin depuis l’interface.
- Gestion centralisée des droits ; possibilité pour les admins de créer et de publier des quiz globaux.

### Quiz
- Deux modes de création :
  - **Admin** : Quiz globaux visibles par tous.
  - **Personnel** : Quiz privés, partageables à des amis.
- Type de quiz : Drapeaux, capitales, cartes, frontières, parties de pays, etc.
- Type de question : QCM, réponse unique, clic sur carte, texte libre.
- Validation immédiate à chaque réponse (juste/faux instantané).
- Score basé sur exactitude et rapidité.[15]
- Un utilisateur ne peut publier que 10 quiz. Gestion de la limite contrôlée côté backend avant chaque publication.

### Compétition
- Mode Duel : deux joueurs s’affrontent en temps réel sur un même quiz, score par rapidité et justesse.
- Classement mondial et leaderboard entre amis.
- Affichage du rang et statistiques sur le profil.
- Système de badges et titres selon progression et réussite (cancre, pèlerin, rogue, noosphère, arcane, etc.).
- Titres spéciaux "Diligent" (premier d’un quiz) et "Ouroboros" (ancien compte).

### Partie sociale
- Ajout et gestion d’amis.
- Invitations à duels, partage de quiz privé.
- Chat simplifié sur le site (pas de notifications push ou email, notifications uniquement sur la webapp).

### Sécurité & confidentialité
- Mots de passe hashés (bcrypt conseillé), pas de stockage en clair.
- Réinitialisation via email sécurisé, token unique par demande, expiration rapide.
- Pas d’envoi de notifications par mail ni SMS, tout reste sur le site.
- Données personnelles stockées selon RGPD (si cible EU).

### UX / UI
- Interface moderne, épurée, affichage direct des résultats et indicateurs de progression.
- Aucun tutoriel ou démo imposé à l’utilisateur.
- Site en une seule langue (français ou anglais), sans gestion multilingue pour la première version.
- Possibilité d’intégrer une charte graphique personnalisée (titres, badges, couleurs…).

### Architecture technique
- Backend Node.js avec API RESTful (Express.js ou équivalent).
- Base de données PostgreSQL, tables pour utilisateurs, quiz, questions, réponses, badges, amis, duels, leaderboard.
- Frontend React (Web), tailwind pour le design responsive et rapide.
- Authentification JWT ou session, middleware pour gestion de rôles et droits (admin, user).

### Admin & Modération
- Dashboard admin pour gestion des utilisateurs, quiz, reports/abus, badges, statistiques.
- Suivi et modération des quiz publiés, signalement abus ou contenus inappropriés.

### Contraintes et exclusions
- Pas de mode démo, ni onboarding/tutoriel.
- Pas de notifications externes, ni support multilingue.
- Système de limitation de publication solide côté backend.
- Inscription et utilisation uniquement via web (pas d’appli mobile dans le MVP).

