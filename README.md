
# Centre Des Loisirs De Fatima

![Licence MIT](https://img.shields.io/badge/License-MIT-green.svg)
![Statut du build](https://img.shields.io/github/actions/workflow/status/miamoto15/centreloisirsdefatima/deploy.yml?branch=main)
![Dernier commit](https://img.shields.io/github/last-commit/miamoto15/centreloisirsdefatima)
![Issues ouvertes](https://img.shields.io/github/issues/miamoto15/centreloisirsdefatima)
![Contributeurs](https://img.shields.io/github/contributors/miamoto15/centreloisirsdefatima)

*Ajoutez ici une capture d’écran du site une fois en ligne.*

## Table des matières

- [Centre Des Loisirs De Fatima](#centre-des-loisirs-de-fatima)
  - [Table des matières](#table-des-matières)
  - [À propos](#à-propos)
  - [Fonctionnalités](#fonctionnalités)
  - [Prérequis](#prérequis)
  - [Installation](#installation)
  - [Structure du projet](#structure-du-projet)
  - [Déploiement](#déploiement)
    - [GitHub Pages](#github-pages)
    - [GitHub Actions](#github-actions)
  - [Contribuer](#contribuer)
  - [Licence](#licence)
  - [Support](#support)
  - [Ressources](#ressources)

## À propos

Le Centre des Loisirs de Fatima est un OBNL qui dynamise la vie communautaire du village de Fatima aux Îles-de-la-Madeleine. Ce site web statique, développé avec Hugo et le thème Dot Org, présente les événements, projets et informations du centre.

## Fonctionnalités

- Présentation des événements à venir
- Pages projets et actualités
- Multilingue (français/anglais)
- Responsive design
- Facile à déployer

Le Centre des Loisirs de Fatima est un organisme à but non lucratif (OBNL) qui œuvre pour dynamiser la vie communautaire du village de Fatima aux Îles-de-la-Madeleine. L’association organise divers événements, entretient des bâtiments importants, propose des initiatives comme des petits-déjeuners dans les écoles et finance ses activités grâce à des loteries, bingos, soirées dansantes, etc.

Pour accroître sa visibilité et promouvoir ses actions, le comité des loisirs a mis en place une vitrine web. Ce site statique, développé avec le générateur (SSG) Hugo et le thème Dot Org Hugo Theme, présente les événements, les projets et les informations essentielles du centre à l’aide de technologies HTML, CSS et JavaScript.

## Prérequis

- [Hugo Extended](https://gohugo.io/getting-started/installing/) (v0.154+)
- [Node.js](https://nodejs.org/) (v25+)
- Windows

Pour installer Hugo Extended et Node.js sous Windows :

```shell
winget install Hugo.Hugo.Extended
winget install OpenJS.NodeJS
```

## Installation

1. Clonez le dépôt Git :

   ```shell
   git clone https://github.com/miamoto15/centreloisirsdefatima.git
   cd centreloisirsdefatima
   ```

2. Installez les dépendances Node.js :

   ```shell
   npm install
   ```

3. Lancez le serveur de développement Hugo :

   ```shell
   npm run start
   ```

## Structure du projet

Voici la structure complète du projet :

- `archetypes/` : Modèles de contenu Hugo
- `assets/` : Fichiers d’assets (CSS, JS, images, etc.)
- `config/` : Fichiers de configuration Hugo
  - `_default/` : Configurations par défaut
  - `development/` : Configurations pour le développement
  - `production/` : Configurations pour la production
- `content/` : Contenu du site (pages, articles, etc.)
- `data/` : Fichiers de données YAML/JSON utilisés par Hugo
- `i18n/` : Fichiers de traduction pour le multilingue
- `layouts/` : Templates et mises en page Hugo
- `public/` : Site généré prêt à être déployé
- `resources/` : Fichiers générés et optimisés par Hugo
- `static/` : Fichiers statiques accessibles tels quels (images, fonts, etc.)
- `themes/` : Thèmes Hugo (ex : Dot Org Hugo Theme)
  - `dot-org-hugo-theme/` : Thème principal utilisé
    - `archetypes/` : Modèles spécifiques au thème
    - `assets/` : Assets du thème (JS, SCSS)
    - `layouts/` : Templates du thème
    - `static/` : Fichiers statiques du thème
    - `exampleSite/` : Exemple de site pour le thème
- `package.json` : Dépendances Node.js
- `postcss.config.js` : Configuration PostCSS
- `README.md` : Documentation du projet

## Déploiement

### GitHub Pages

Ce projet est conçu pour être déployé sur GitHub Pages.

**Statut :** La configuration GitHub Pages sera documentée prochainement.

En attendant, vous pouvez générer le site statique avec `npm run build` et déployer le contenu du dossier `public/` manuellement ou via une action GitHub.

Pour générer le site statique en production :

```shell
npm run build
```

Les fichiers générés seront dans le dossier `public/`.

### GitHub Actions

Un pipeline d’intégration et de déploiement continus (CI/CD) est mis en place avec GitHub Actions afin d’automatiser la construction et la mise en ligne du site.

**Pour lancer le pipeline** :

- Ouvrez une pull request vers la branche principale (`main`).
- Après l’approbation du propriétaire du dépôt, le pipeline GitHub Actions se lancera automatiquement et exécutera le workflow défini dans `.github/workflows/deploy.yml`.
- Le statut du build est visible dans l’onglet “Actions” du dépôt ou via le badge en haut du README.

Vous pouvez aussi lancer manuellement le workflow depuis l’onglet “Actions” sur GitHub si besoin.

## Contribuer

1. Forkez le projet
2. Créez une branche (`git checkout -b feature/ma-fonctionnalite`)
3. Commitez vos changements (`git commit -am 'Ajout d'une fonctionnalité'`)
4. Poussez la branche (`git push origin feature/ma-fonctionnalite`)
5. Ouvrez une Pull Request

## Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE).

Vous pouvez :

- Utiliser, copier et modifier le code
- Redistribuer, même à des fins commerciales
- Intégrer le code dans d’autres projets

Sous réserve de :

- Conserver la mention du copyright et la licence dans toutes les copies

Le fichier LICENSE reste la référence légale.

## Support

Pour toute question ou problème :

1. Veuillez d’abord créer un billet (issue) sur GitHub dans l’onglet “Issues” du dépôt.
2. Si besoin, contactez-nous par courriel à : [info@centreloisirsfatima.com](mailto:support@centreloisirsfatima.org)

## Ressources

- [Documentation Hugo](https://gohugo.io/documentation/)
- [Thème Dot Org Hugo](https://github.com/cncf/dot-org-hugo-theme)
