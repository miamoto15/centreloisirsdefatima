
# Centre Des Loisirs De Fatima

![Licence AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue.svg)
![Statut du build](https://img.shields.io/github/actions/workflow/status/miamoto15/centreloisirsdefatima/deploy.yml?branch=main)
![Dernier commit](https://img.shields.io/github/last-commit/miamoto15/centreloisirsdefatima)
![Issues ouvertes](https://img.shields.io/github/issues/miamoto15/centreloisirsdefatima)
![Contributeurs](https://img.shields.io/github/contributors/miamoto15/centreloisirsdefatima)

![Site web - Centre des Loisirs de Fatima](static/Site%20web%20-%20Centre%20des%20Loisirs%20de%20Fatima.jpg)

## Table des matières

- [À propos](#à-propos)
- [Fonctionnalités](#fonctionnalités)
- [Stack technique](#stack-technique)
- [Configuration Windows (débutant)](#configuration-windows-débutant)
- [Démarrage local du projet](#démarrage-local-du-projet)
- [Commandes utiles](#commandes-utiles)
- [Contribuer (workflow recommandé)](#contribuer-workflow-recommandé)
- [Structure du projet (dossiers clés)](#structure-du-projet-dossiers-clés)
- [Déploiement](#déploiement)
- [Forker ce dépôt](#forker-ce-dépôt)
- [Licence](#licence)
- [Support](#support)
- [Ressources](#ressources)

## À propos

Le Centre des Loisirs de Fatima est un OBNL qui dynamise la vie communautaire du village de Fatima aux Îles-de-la-Madeleine.

Ce dépôt contient le site web statique officiel de l'organisme, construit avec Hugo.

## Fonctionnalités

- Présentation des événements et activités
- Pages de projets et d'information
- Site bilingue (français/anglais)
- Design responsive (mobile et bureau)
- Génération statique rapide et déploiement automatisé

## Stack technique

- [Hugo Extended](https://gohugo.io/) (générateur statique)
- [Node.js](https://nodejs.org/) + npm (outillage front-end)
- [Dart Sass](https://sass-lang.com/dart-sass/) (compilation SCSS)
- Git + GitHub (versionnement et collaboration)

## Configuration Windows (débutant)

Cette section est faite pour une première installation complète sur Windows.

### 1. Installer les outils requis

Ouvrir **PowerShell en mode administrateur** et exécuter :

```powershell
winget install --id Git.Git -e
winget install --id Hugo.Hugo.Extended -e
winget install --id OpenJS.NodeJS.LTS -e
winget install --id Google.dart-sdk -e
```

Si `winget` n'est pas reconnu, installer d'abord **App Installer** depuis le Microsoft Store, puis relancer PowerShell.

### 2. Vérifier les versions installées

Dans un nouveau terminal PowerShell :

```powershell
git --version
hugo version
node -v
npm -v
sass --version
```

Versions minimales recommandées :

- Hugo Extended: v0.161.1+
- Node.js: v20 LTS+

### 3. Configurer Git (une seule fois)

```powershell
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
```

### 4. Installer VS Code (recommandé)

- Installer [Visual Studio Code](https://code.visualstudio.com/)
- Installer l'extension **EditorConfig for VS Code** (optionnel mais utile)

## Démarrage local du projet

### 1. Cloner le dépôt

```powershell
git clone https://github.com/miamoto15/centreloisirsdefatima.git
cd centreloisirsdefatima
```

### 2. Installer les dépendances

```powershell
npm install
```

### 3. Lancer le serveur de développement

```powershell
npm run start
```

Puis ouvrir l'adresse locale affichée dans le terminal (habituellement `http://localhost:1313`).

### Dépannage rapide (Windows)

- `hugo` non reconnu : fermer/réouvrir PowerShell après installation, puis refaire `hugo version`.
- `sass` non reconnu : vérifier l'installation de Dart Sass avec `sass --version`.
- `npm install` échoue : vérifier `node -v` et `npm -v`, puis relancer dans un nouveau terminal.
- Port 1313 occupé : arrêter l'autre instance Hugo ou redémarrer le terminal.

## Commandes utiles

```powershell
# Serveur local (drafts + contenus futurs activés)
npm run start

# Build production local (sans déploiement)
npm run build

# Build staging local
npm run build:staging
```

Important : ne pas utiliser `npm run deploy` en contribution normale. Le déploiement est géré par GitHub Actions.

## Contribuer (workflow recommandé)

### 1. Créer une branche

```powershell
git checkout -b feature/ma-fonctionnalite
```

### 2. Développer et vérifier localement

- Modifier le code
- Vérifier le rendu avec `npm run start`
- Vérifier le build avec `npm run build`

### 3. Committer et pousser

```powershell
git add .
git commit -m "feat: ajouter ma fonctionnalite"
git push origin feature/ma-fonctionnalite
```

### 4. Ouvrir une Pull Request

- Créer une PR vers `main`
- Attendre le pipeline CI
- Corriger si le build échoue

## Structure du projet (dossiers clés)

- `archetypes/` : modèles de contenu Hugo
- `assets/` : SCSS, images et autres assets transformés
- `config/` : configuration Hugo par environnement
- `content/` : contenus éditoriaux (fr/en)
- `data/` : données YAML/JSON utilisées dans les pages
- `layouts/` : gabarits et partiels Hugo
- `static/` : fichiers servis tels quels
- `themes/dot-org-hugo-theme/` : thème Hugo utilisé
- `public/` : site généré (build output)

## Déploiement

### Flux CI/CD automatique (recommandé)

Le déploiement est automatisé via GitHub Actions.

```text
git push origin feature/ma-branche
  ↓
Pull Request vers main
  ↓
CI (build) doit passer
  ↓
Merge dans main
  ↓
Déploiement gh-pages automatique
  ↓
centreloisirsfatima.com mis à jour (~1 min)
```

### Pipelines GitHub Actions

| Fichier | Déclencheur | Rôle |
|---|---|---|
| `.github/workflows/ci.yml` | Chaque PR vers `main` | Build Hugo + vérification, bloque le merge si échec |
| `.github/workflows/deploy.yml` | Push sur `main` | Build production + publication sur `gh-pages` |
| `.github/workflows/auto-merge.yml` | Ouverture/mise à jour d'une PR | Active l'auto-merge squash quand la CI est verte |

### Déploiement manuel (urgence seulement)

Le workflow est déclenchable manuellement parce que `.github/workflows/deploy.yml` contient `workflow_dispatch`.

Chemin GitHub : **Actions -> Déploiement — gh-pages -> Run workflow**

Attention : ne pas utiliser le workflow **pages-build-deployment** pour cette action.
Ce workflow est géré automatiquement par GitHub Pages et n'est pas celui du dépôt.

Important : ce bouton est visible/utilisable seulement pour les membres ayant les permissions adéquates sur le dépôt (généralement `Write`, `Maintain` ou `Admin`).

## Forker ce dépôt

Si vous réutilisez ce dépôt comme base, vous devez **retirer tout le contenu propre au Centre Des Loisirs de Fatima** avant publication, incluant notamment :

- Photos et images
- Logos et marques de commerce
- Informations d'événements
- Textes et descriptions propres à l'organisme

Ce contenu est la propriété exclusive du **Centre Des Loisirs de Fatima, Î.M., Inc.** et n'est **pas** couvert par l'AGPL-3.0 (qui s'applique au code source seulement).

## Licence

Ce projet est distribué sous licence **GNU Affero General Public License v3.0 (AGPL-3.0)**. Voir [LICENSE](LICENSE).

| Titulaire | Périmètre |
|---|---|
| Copyright © 2026 LE CENTRE DES LOISIRS DE FATIMA, Î.M., INC. | Contenu : textes, images, données, marque et logo |
| Copyright © 2026 Cédric Arseneault | Code source : gabarits Hugo, styles, scripts, structure du site |

Vous pouvez :

- Utiliser, copier et modifier le code
- Redistribuer et déployer le code, y compris sur un serveur web

Sous réserve de :

- Conserver les mentions de copyright et la licence
- Publier vos modifications sous AGPL-3.0 en cas de redistribution ou déploiement public

Le fichier LICENSE reste la référence légale.

## Support

Pour toute question ou problème :

1. Ouvrir d'abord un ticket dans l'onglet **Issues** du dépôt GitHub.
2. Si besoin, contacter : [info@centreloisirsfatima.com](mailto:info@centreloisirsfatima.com)

## Ressources

- [Documentation Hugo](https://gohugo.io/documentation/)
- [Thème Dot Org Hugo](https://github.com/cncf/dot-org-hugo-theme)
