Projet de Deploiement GLPI 

1. Presentation du projet
Ce projet consiste en la mise en place d'un Proof of Concept pour l'outil de helpdesk GLPI. L'objectif est de fournir a une entreprise une solution complete de gestion de tickets et d'inventaire automatise dans un environnement Windows Server avec des postes clients Windows.

Le deploiement integre des mecanismes de securisation (HTTPS), de resolution de noms (DNS), de gestion d'actifs et d'automatisation des alertes critiques.

2. Architecture Generale
L'infrastructure repose sur un serveur central unique regroupant les éléments suivants :
Serveur Web : Internet Information Services (IIS) avec support PHP 8.1.33.
Base de donnees : MySQL/MariaDB dediee avec utilisateur restreint.
Securite et Reseau : Active Directory Certificate Services (AD CS) et serveur DNS.
Clients : Postes Windows integres au domaine pour l'inventaire et l'authentification.

3. Implementation Technique
Serveur Web et GLPI
IIS : Activation des modules CGI, FastCGI et compression.
PHP : Configuration des extensions requises (pdo_mysql, mbstring, curl, gd) pour garantir la stabilite de l'application.
GLPI : Deploiement de la derniere version stable, configuration de la langue, des fuseaux horaires et des regles de tickets.

Reseau et HTTPS
AD CS : Creation d'une autorite de certification interne pour l'emission d'un certificat SSL lie a l'URL glpi.company.local.
DNS : Mise en place d'une URL conviviale et d'une redirection permanente HTTP vers HTTPS pour securiser les flux.

Inventaire et Automatisation
GLPI Agent : Installation et deploiement sur l'ensemble du parc pour une remontee automatique des informations materielles et logicielles.
Script de maintenance : Un script PowerShell a ete developpe pour analyser l'espace disque local. Il utilise une requete CURL via l'API GLPI pour creer un ticket automatique des que la capacite libre est inferieure a 5%.

4. Securisation 
Mesures de Securite
Activation du Firewall Windows avec des regles restrictives pour IIS et MySQL.
Application de permissions NTFS minimales sur les dossiers sensibles de GLPI.
Desactivation du compte administrateur par defaut et imposition de mots de passe forts.

Integration Active Directory 
Mise en place de l'authentification LDAP permettant aux utilisateurs du domaine de se connecter avec leurs identifiants Active Directory habituels.
Cette integration simplifie la gestion des comptes et ameliore l'experience utilisateur.

Ahmadou DIALLO
Etudiant à SUPINFO.
