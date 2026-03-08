# TP – Déployer Keycloak, activer MFA et configurer OAuth2/OIDC

## Objectif du projet
Ce TP consiste à déployer une instance locale de Keycloak, créer un realm et un utilisateur, activer l’authentification multifacteur (MFA via TOTP) et configurer un client OAuth2/OIDC utilisant le flux Authorization Code + PKCE.

---

## Architecture du système
Le TP repose sur un environnement simple composé de :

### Keycloak (Docker)
- Exposé sur le port 8080  
- Admin bootstrap via variables d’environnement  
- Mode start-dev pour un déploiement rapide

### Realm : lab-iam
- Espace d’authentification isolé  
- Gestion des utilisateurs, clients et politiques MFA

### Utilisateur : alice
- Email vérifié  
- Mot de passe défini  
- Action obligatoire : Configure OTP

### Client OIDC : demo-spa
- Type : Public  
- Flux : Authorization Code + PKCE  
- Redirect URI : https://www.keycloak.org/app/*  

---

## Fonctionnalités principales

###  Déploiement Keycloak (Docker)
- Lancement rapide via docker run  
- Création automatique de l’admin  
- Accès à la console d’administration

###  Création du realm et d’un utilisateur
- Realm lab-iam
- Utilisateur alice avec email vérifié  
- Définition du mot de passe  
- Activation de l’action obligatoire *Configure OTP*

###  Activation du MFA (TOTP)
- Activation de Configure OTP dans Required Actions  
- Scan du QR code via une application TOTP  
- Validation du code à 6 chiffres  
- Authentification en deux étapes (mot de passe + OTP)

###  Configuration d’un client OIDC
- Client public demo-spa  
- Standard Flow activé  
- Redirect URI vers l’app de test Keycloak  
- Web origins ouverts pour le test

###  Test du flux Authorization Code + PKCE
- Connexion via https://www.keycloak.org/app  
- Redirection vers Keycloak  
- Authentification avec MFA  
- Retour automatique vers l’application  
- Analyse des tokens via DevTools

