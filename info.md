# Project Structure

Ce projet consiste à développer un fournisseur d'identité (IdP) avec une API REST en utilisant Spring Boot (Java), Maven et une base de données PostgreSQL, le tout conteneurisé avec Docker et hébergé sur GitHub. Voici une feuille de route détaillée pour vous guider :

**1. Initialisation du Projet :**

* **Création du dépôt GitHub :** Créez un nouveau dépôt sur GitHub pour héberger votre code.
* **Configuration du projet Spring Boot :** Utilisez Spring Initializr (start.spring.io) pour générer un projet Spring Boot avec les dépendances suivantes :
  * Spring Web (pour l'API REST)
  * Spring Data JPA (pour l'accès à la base de données)
  * PostgreSQL Driver
  * Spring Security (pour la sécurité)
  * Spring Boot DevTools (pour le développement)
  * Swagger (Springdoc-openapi)
  * Lombok (facultatif, pour réduire le boilerplate code)
* **Configuration de Maven :** Assurez-vous que le fichier `pom.xml` contient les dépendances nécessaires et configurez les plugins Maven appropriés (par exemple, pour la gestion des versions, les tests, etc.).
* **Dockerisation :** Créez un fichier `Dockerfile` pour conteneuriser l'application Spring Boot et un fichier `docker-compose.yml` pour orchestrer l'application et la base de données PostgreSQL.

**2. Modélisation des Données (MCD) :**

* **Table Utilisateur :** `id`, `nom`, `prenom`, `email`, `mot_de_passe`, `email_verifie`, `date_verification_email`, `nb_tentatives_connexion`, `date_dernier_echec`, etc.
* **Table Session :** `id`, `utilisateur_id`, `token`, `date_expiration`, etc.

**3. Implémentation des Fonctionnalités :**

* **Inscription :**
  * Création d'un endpoint REST pour l'inscription.
  * Validation des données saisies (format de l'email, mot de passe fort, etc.).
  * Envoi d'un email de validation contenant un lien unique.
  * Mise à jour du champ `email_verifie` dans la base de données après la validation.
* **Authentification Multifacteur (MFA) :**
  * Génération d'un code PIN aléatoire.
  * Envoi du PIN par email.
  * Création d'un endpoint pour la validation du PIN.
  * Vérification de la validité du PIN (90 secondes).
* **Gestion du Compte :**
  * Endpoints pour la modification des informations utilisateur (sauf l'email).
* **Gestion des Sessions :**
  * Création de sessions après l'authentification réussie.
  * Utilisation de JWT (JSON Web Tokens) pour gérer les sessions (recommandé).
  * Configuration de la durée de vie des sessions (paramétrable).
* **Hashing des Mots de Passe :**
  * Utiliser `BCryptPasswordEncoder` de Spring Security pour hasher les mots de passe.
* **Gestion des Tentatives de Connexion :**
  * Compteur de tentatives de connexion par utilisateur.
  * Blocage du compte après un nombre configurable de tentatives (par défaut 3).
  * Endpoint pour la réinitialisation du compteur de tentatives via un lien envoyé par email.
  * Réinitialisation du compteur après une connexion réussie.
* **Documentation API (Swagger) :**
  * Utiliser Springdoc-openapi pour générer automatiquement la documentation Swagger.

**4. Tests :**

* Écrire des tests unitaires pour chaque fonctionnalité.
* Utiliser Postman pour tester les endpoints de l'API REST.

**5. Configuration et Paramétrage :**

* Utiliser des fichiers de configuration (par exemple, `application.properties` ou `application.yml`) pour configurer les paramètres suivants :
  * Durée de vie des sessions.
  * Nombre maximal de tentatives de connexion.
  * Configuration de l'envoi d'emails.

**6. Docker et Docker Compose :**

* **Dockerfile :** Définir les instructions pour construire l'image Docker de l'application Spring Boot.
* **docker-compose.yml :** Définir les services (application Spring Boot et PostgreSQL) et leurs dépendances.

**7. Documentation Technique :**

* **MCD :** Inclure le diagramme MCD.
* **Scénarios d'utilisation :** Décrire les différents cas d'utilisation (inscription, authentification, gestion du compte, etc.).
* **Instructions de lancement :** Fournir des instructions claires pour compiler, conteneuriser et exécuter l'application.
* **Liste des membres :** Nom, prénom et NumETU de chaque membre de l'équipe.

**8. Livrables :**

* **Archive ZIP :** Contenant le code source, les instructions de lancement et la collection Postman.
* **Liste TODO :** Avec les tâches à accomplir et leur affectation aux membres de l'équipe. link: https://docs.google.com/spreadsheets/d/14Y1N1uY1NLFILozMZSLSuBJScVtQY2m_s2X9kR4YFu4/edit?usp=sharing

**Exemple de structure de projet (Maven) :**

``` text
idp-project/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/idp/
│   │   │       ├── controller/
│   │   │       ├── service/
│   │   │       ├── repository/
│   │   │       ├── model/
│   │   │       ├── config/
│   │   │       ├── exception/
│   │   │       └── IdpApplication.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── templates/ (pour les emails)
│   └── test/
│       └── ...
├── pom.xml
├── Dockerfile
├── docker-compose.yml
├── README.md
└── postman_collection.json
```

En suivant ces étapes et en utilisant les technologies mentionnées, vous serez en mesure de réaliser un projet de fournisseur d'identité complet et fonctionnel. N'oubliez pas de versionner régulièrement votre code sur GitHub et de communiquer au sein de votre équipe.
