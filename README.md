# 🛠️ Déploiement Sécurisé de GLPI sur Windows Server

![Windows Server](https://img.shields.io/badge/Windows_Server-0078D6?style=for-the-badge&logo=windows&logoColor=white) ![IIS](https://img.shields.io/badge/IIS-0078D6?style=for-the-badge&logo=iis&logoColor=white) ![PHP](https://img.shields.io/badge/PHP_8.1-777BB4?style=for-the-badge&logo=php&logoColor=white) ![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white) ![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=for-the-badge&logo=powershell&logoColor=white) ![Active Directory](https://img.shields.io/badge/Active_Directory-0078D6?style=for-the-badge&logo=microsoft&logoColor=white)

## 📝 Présentation du projet
[cite_start]Ce projet est un *Proof of Concept* (PoC) complet visant à déployer **GLPI**, une solution de gestion de services informatiques (ITSM) et de helpdesk, dans un environnement d'entreprise 100% Microsoft[cite: 467, 468, 469]. 

[cite_start]L'objectif était de bâtir une infrastructure robuste, sécurisée et automatisée, allant de la résolution DNS à la création automatique de tickets d'incidents via API[cite: 472, 688, 703].

## 🏗️ Architecture Technique
[cite_start]L'infrastructure centralisée repose sur un serveur Windows Server hébergeant de multiples rôles[cite: 472]:
* [cite_start]**Serveur Web** : IIS (Internet Information Services) avec configuration FastCGI et PHP 8.1.33[cite: 487, 488, 497].
* [cite_start]**Base de données** : MariaDB/MySQL avec une gestion stricte des privilèges utilisateurs[cite: 566].
* [cite_start]**Services d'Infrastructure** : Rôles AD DS (Active Directory), DNS, et AD CS (Autorité de Certification)[cite: 472, 481, 482].
* [cite_start]**Clients** : Postes Windows intégrés au domaine pour remonter l'inventaire matériel[cite: 485, 668].

## 🛠️ Réalisations et Implémentations

### 1. Administration Web & Base de données
* [cite_start]Installation et configuration d'IIS avec les modules nécessaires (CGI, WebDAV, Compression)[cite: 488].
* [cite_start]Intégration de PHP et activation des extensions requises (`pdo_mysql`, `curl`, `gd`, `mbstring`)[cite: 489].
* [cite_start]Optimisation du pool d'applications IIS pour garantir la stabilité de GLPI[cite: 490].

### 2. Sécurité et Résolution Réseau (HTTPS / DNS)
* [cite_start]**AD CS** : Création d'une autorité de certification interne et génération d'un certificat SSL[cite: 628, 629].
* [cite_start]**DNS** : Mise en place d'une zone DNS pour une URL conviviale (`https://glpi.company.local`)[cite: 664, 665].
* **Hardening** : 
  * [cite_start]Redirection permanente HTTP vers HTTPS via IIS[cite: 631].
  * [cite_start]Configuration stricte du pare-feu Windows et application de permissions NTFS minimales sur les répertoires sensibles[cite: 691, 692].

### 3. Inventaire Automatisé (ITAM)
* [cite_start]Déploiement de **GLPI Agent** sur les postes clients du domaine[cite: 667, 668].
* [cite_start]Remontée automatique et régulière des informations matérielles, réseau et logicielles dans la base GLPI[cite: 669, 670].

### 4. Authentification Centralisée (LDAP)
* [cite_start]Intégration de GLPI avec **Active Directory (LDAP)**[cite: 696, 697].
* [cite_start]Les utilisateurs peuvent se connecter au portail de support directement avec leur compte de domaine Windows (SSO-like), simplifiant grandement la gestion des accès[cite: 697, 698].

## 🚀 Automatisation (Highlight) : Script d'Alerte Disque
[cite_start]Afin de démontrer une démarche de Maintien en Condition Opérationnelle (MCO) proactive, un script **PowerShell** a été développé et couplé au planificateur de tâches Windows.
* [cite_start]**Fonctionnement** : Le script monitore l'espace de stockage des postes clients[cite: 687].
* [cite_start]**Action** : Si l'espace disque disponible passe en dessous de **5%**, le script effectue une requête `CURL` authentifiée vers l'**API REST de GLPI** pour générer automatiquement un ticket d'incident assigné à l'équipe technique[cite: 687, 688].

---
*Projet réalisé par Ahmadou DIALLO dans le cadre de mon Master à SUPINFO.*
