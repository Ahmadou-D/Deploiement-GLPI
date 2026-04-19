# 🛠️ Déploiement Sécurisé de GLPI sur Windows Server

![Windows Server](https://img.shields.io/badge/Windows_Server-0078D6?style=for-the-badge&logo=windows&logoColor=white) ![IIS](https://img.shields.io/badge/IIS-0078D6?style=for-the-badge&logo=iis&logoColor=white) ![PHP](https://img.shields.io/badge/PHP_8.1-777BB4?style=for-the-badge&logo=php&logoColor=white) ![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white) ![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=for-the-badge&logo=powershell&logoColor=white) ![Active Directory](https://img.shields.io/badge/Active_Directory-0078D6?style=for-the-badge&logo=microsoft&logoColor=white)

## 📝 Présentation du projet
Ce projet est un Proof of Concept (PoC) complet visant à déployer GLPI, une solution de gestion de services informatiques (ITSM) et de helpdesk, dans un environnement d'entreprise 100% Microsoft. 

L'objectif était de bâtir une infrastructure robuste, sécurisée et automatisée, allant de la résolution DNS à la création automatique de tickets d'incidents via API.

## 🏗️ Architecture Technique
L'infrastructure centralisée repose sur un serveur Windows Server hébergeant de multiples rôles :
* **Serveur Web** : IIS (Internet Information Services) avec configuration FastCGI et PHP 8.1.33.
* **Base de données** : MariaDB/MySQL avec une gestion stricte des privilèges utilisateurs.
* **Services d'Infrastructure** : Rôles AD DS (Active Directory), DNS, et AD CS (Autorité de Certification).
* **Clients** : Postes Windows intégrés au domaine pour remonter l'inventaire matériel.

## 🛠️ Réalisations et Implémentations

### 1. Administration Web & Base de données
* Installation et configuration d'IIS avec les modules nécessaires (CGI, WebDAV, Compression).
* Intégration de PHP et activation des extensions requises (`pdo_mysql`, `curl`, `gd`, `mbstring`).
* Optimisation du pool d'applications IIS pour garantir la stabilité de GLPI.

### 2. Sécurité et Résolution Réseau (HTTPS / DNS)
* **AD CS** : Création d'une autorité de certification interne et génération d'un certificat SSL.
* **DNS** : Mise en place d'une zone DNS pour une URL conviviale (`https://glpi.company.local`).
* **Hardening** : 
  * Redirection permanente HTTP vers HTTPS via IIS.
  * Configuration stricte du pare-feu Windows et application de permissions NTFS minimales sur les répertoires sensibles.

### 3. Inventaire Automatisé (ITAM)
* Déploiement de GLPI Agent sur les postes clients du domaine.
* Remontée automatique et régulière des informations matérielles, réseau et logicielles dans la base GLPI.

### 4. Authentification Centralisée (LDAP)
* Intégration de GLPI avec Active Directory (LDAP).
* Les utilisateurs peuvent se connecter au portail de support directement avec leur compte de domaine Windows (SSO-like), simplifiant grandement la gestion des accès.

## 🚀 Automatisation (Highlight) : Script d'Alerte Disque
Afin de démontrer une démarche de Maintien en Condition Opérationnelle (MCO) proactive, un script PowerShell a été développé et couplé au planificateur de tâches Windows.
* **Fonctionnement** : Le script monitore l'espace de stockage des postes clients.
* **Action** : Si l'espace disque disponible passe en dessous de 5%, le script effectue une requête CURL authentifiée vers l'API REST de GLPI pour générer automatiquement un ticket d'incident assigné à l'équipe technique.

---
*Projet réalisé par Ahmadou DIALLO.*
