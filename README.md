# Menu Maker by Qwenta : planification d'un projet web en Agile

> **Projet de planification, sans code.** Projet de formation OpenClassrooms (parcours Développeur Web), réalisé pour un client fictif.

J'ai planifié de A à Z le développement de **Menu Maker**, un outil en ligne qui permet aux restaurateurs de créer, personnaliser et diffuser leur menu. Dans le rôle d'un développeur front-end d'agence, j'ai transformé les besoins du client en tâches techniques, estimé et planifié le travail en méthode Agile, rédigé les spécifications techniques et mis en place une veille technologique.

**16** User Stories · **29** tâches techniques · **93** story points · **5** sprints de 2 semaines

---

## Sommaire

- [Contexte](#contexte)
- [Compétences mises en œuvre](#compétences-mises-en-œuvre)
- [Livrables](#livrables)
- [Méthodologie](#méthodologie)
- [Choix techniques](#choix-techniques)
- [Veille technologique](#veille-technologique)
- [Ce que j'ai appris](#ce-que-jai-appris)

---

## Contexte

**Qwenta** (client fictif) est un imprimeur historique de supports pour les professionnels, qui veut se diversifier vers le numérique. Menu Maker permet aux restaurateurs de :

1. **Créer** leur menu : catégories, plats, prix, descriptions, photos.
2. **Personnaliser** leur menu : police, couleur et logo, avec un aperçu en temps réel.
3. **Diffuser** leur menu : export PDF, Deliveroo, Instagram, ou commande d'impression chez Qwenta.

**Contraintes du projet :** version desktop uniquement, compatibilité avec Chrome, Safari et Firefox, navigation au clavier, compatibilité avec les lecteurs d'écran, respect de la charte graphique de Qwenta.

---

## Compétences mises en œuvre

| Compétence | Concrètement |
|---|---|
| Découper un projet | Transformer 16 User Stories en 29 tâches techniques (17 front-end, 12 back-end) |
| Estimer et planifier | Estimation en story points (suite de Fibonacci), vélocité, découpage en sprints |
| Organiser le travail en Agile | Méthode Scrum, tableau Kanban sur Notion |
| Faire des choix techniques | Choisir une stack et justifier chaque décision |
| Assurer une veille technologique | Veille organisée sur Feedly, avec un impact direct sur les choix techniques |
| Présenter son travail à un client | Soutenance face au Product Owner (rôle joué par l'évaluateur) |

---

## Livrables

| N° | Livrable | Lien |
|---|---|---|
| 1 | Spécifications techniques | [PDF](./livrables/Holtzinger_Julien_1_specifications_techniques_092026.pdf) |
| 2 | Tableau Kanban | [PDF](./livrables/Holtzinger_Julien_2_kanban_092026.pdf) · [Tableau Notion public](https://fishy-composer-3b5.notion.site/3edfb3ecb55580aa8431c175b530a241?v=194b6204f22c466ba871edccda1ffb1b) |
| 3 | Système de veille | [PDF](./livrables/Holtzinger_Julien_3_veille_092026.pdf) |
| 4 | Présentation au client | [PDF](./livrables/Holtzinger_Julien_4_presentation_092026.pdf) |

---

## Méthodologie

### Scrum

Le développement est découpé en **sprints de 2 semaines**. Chaque sprint suit le même cycle : planification, point quotidien (daily), revue avec le client, puis rétrospective.

**Pourquoi Scrum pour ce projet ?**

- Les fonctionnalités prioritaires sont livrées en premier.
- Le client valide chaque version et peut réorienter les priorités.
- Les points encore incertains (accès à l'API Deliveroo, flux RSS du blog) sont traités au fil des sprints, sans bloquer tout le projet.

### Estimation et planning

- **93 story points** au total, estimés selon la suite de Fibonacci (1, 2, 3, 5, 8…).
- **Vélocité estimée : 20 points par sprint.** C'est une estimation de départ, à réajuster après les premiers sprints.
- 93 ÷ 20 ≈ 4,65, soit **5 sprints, environ 10 semaines**, avec une petite marge pour les imprévus.

| Étape | Contenu |
|---|---|
| Sprint 1 | Les fondations : serveur, base de données, sécurité, connexion |
| Fin du sprint 3 | Toutes les fonctionnalités **P1** sont livrées (59 points, environ 6 semaines) : le restaurateur peut créer, personnaliser, exporter et faire imprimer son menu |
| Sprints 4 et 5 | Les fonctionnalités **P2 et P3**, comme la diffusion sur Deliveroo et Instagram |

### Kanban

Le tableau compte 4 colonnes : **À faire → En cours → À tester → Terminé**.

Chaque carte contient : la User Story liée, l'Epic, le sprint, la personne attribuée, les story points, les sous-tâches, les spécifications et les **critères de succès**.

### Validation d'une tâche

1. Le développeur crée une branche Git, puis ouvre une **pull request**.
2. Le code est relu en **code review** avant chaque fusion.
3. On vérifie que les **critères de succès** de la carte sont remplis.
4. À la revue de sprint, le **client** valide la fonctionnalité.

---

## Choix techniques

| Couche | Technologies | Pourquoi |
|---|---|---|
| Front-end | React + Vite, React Router, React Hook Form, variables CSS | Des composants réutilisables, une interface dynamique sans rechargement (indispensable pour l'aperçu en temps réel), un écosystème riche |
| Back-end | Node.js + Express (API REST), JWT, Nodemailer, Multer | La gestion de la connexion, des e-mails et des images, avec les clés des API externes gardées côté serveur |
| Base de données | MongoDB + Mongoose | Un menu (menu → catégories → plats) est stocké dans un seul document, sans assembler plusieurs tableaux |
| Hébergement | Render ou Railway, MongoDB Atlas | Une mise en ligne automatique depuis GitHub |

**Un seul langage, JavaScript, du front à la base de données :** le développement et la maintenance sont plus simples.

### Focus : la connexion sans mot de passe (lien magique)

À la demande du client, la connexion se fait **uniquement avec l'adresse e-mail**. Le restaurateur reçoit un lien unique et temporaire, et il est connecté en un clic.

- **Plus sûr :** aucun mot de passe n'est stocké, donc rien à voler en cas de fuite.
- **Plus simple :** un seul parcours pour s'inscrire et se connecter.

### Sécurité

- Routes protégées par un middleware JWT : chaque restaurateur n'accède qu'à ses propres données.
- Double confirmation pour changer d'adresse e-mail.
- Clés des API Deliveroo et Instagram stockées côté serveur, dans un fichier `.env`.
- Fichiers envoyés limités aux images de 2 Mo maximum.
- HTTPS sur tout le site, et audit régulier des dépendances.

---

## Veille technologique

La veille est organisée sur **Feedly**, un outil qui rassemble au même endroit les nouveautés de toutes mes sources. Elle suit 2 axes :

- **Axe 1, technologies du projet (8 sources)** : React Blog, notes de version de Node.js, MongoDB, Grafikart…
- **Axe 2, développement web, accessibilité et sécurité (7 sources)** : OWASP, Snyk, Access42, Smashing Magazine, JavaScript Weekly…

J'ai choisi des supports variés : blogs, vidéos, podcast, newsletter, notes de version.

**Ce que la veille a changé dans le projet :** j'ai appris que **styled-components** était passé en mode maintenance. Pour un nouveau projet, j'ai donc choisi les **variables CSS**, qui sont natives au navigateur et ne dépendent d'aucune bibliothèque.

---

## Ce que j'ai appris

- **Une User Story n'est pas une tâche.** La User Story décrit le besoin (le « quoi »), la tâche décrit la solution technique (le « comment »).
- **Les story points mesurent la complexité, pas le temps.** C'est la vélocité qui fait le lien avec le calendrier.
- **Une tâche est terminée quand ses critères de succès sont vérifiés**, pas seulement quand le code est écrit.
- **Le rôle du développeur senior** (retour de soutenance) : dans une petite équipe, c'est lui qui garantit la qualité, car il sait relire le code front comme le code back.
- **La cohérence des chiffres** (retour de soutenance) : la taille de l'équipe, la vélocité et la durée du projet doivent rester cohérentes entre elles.

---

**Julien Holtzinger** · Développeur web en formation · [GitHub](https://github.com/Alzorath57)

*Projet réalisé dans le cadre du parcours Développeur Web d'OpenClassrooms : client, agence et Product Owner sont fictifs.*
