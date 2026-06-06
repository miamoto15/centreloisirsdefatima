# 🔄 Documentation des Workflows GitHub Actions

Ce document décrit les pipelines CI/CD du projet et leurs limites.

## 📋 Pipelines disponibles

### 1. 🏷️ Release (`release.yml`)
**Déclencheurs :** Push sur `main` ou manuel via `workflow_dispatch`

**Fonctionnalités :**
- ✅ Versioning automatique basé sur Conventional Commits
- ✅ Création de tags Git (v1.2.3)
- ✅ GitHub Release avec notes auto-générées
- ✅ Artefacts du site (.tar.gz, .zip)
- ✅ Mise à jour du fichier VERSION

**Conventional Commits :**
```bash
fix: correction bug           → PATCH (1.0.0 → 1.0.1)
feat: nouvelle fonctionnalité → MINOR (1.0.0 → 1.1.0)
feat!: breaking change        → MAJOR (1.0.0 → 2.0.0)
```

### 2. 🧩 Preview (`preview.yml`)
**Déclencheur :** Pull Request (ouverture, synchronisation, fermeture)

**Fonctionnalités :**
- ✅ Build Hugo automatique
- ✅ Déploiement sur GitHub Pages (`/pr-{numéro}/`)
- ✅ URL unique par PR
- ✅ Bandeau visuel indiquant l'environnement de preview
- ✅ Commentaire automatique sur la PR
- ✅ Nettoyage automatique à la fermeture
- ✅ Blocage SEO (noindex, robots.txt)

### 3. 🚀 Deploy (`deploy.yml`)
**Déclencheur :** Push sur `main`

**Fonctionnalités :**
- ✅ Build Hugo en production
- ✅ Déploiement sur gh-pages
- ✅ Servir le site sur le domaine custom

### 4. 🔄 Auto-merge (`auto-merge.yml`)
**Déclencheur :** Pull Request

**Fonctionnalités :**
- ✅ Active l'auto-merge (squash) après :
  - CI vert
  - Approbation manuelle d'un reviewer

## ⚙️ Configuration requise

### GitHub Settings
1. **Settings → General → Pull Requests**
   - ✅ Allow auto-merge

2. **Settings → Branches → Protection rule for `main`**
   - ✅ Require a pull request before merging
   - ✅ Require approvals (minimum: 1)
   - ✅ Require status checks to pass before merging
   - Status checks requis : `Build Hugo (production)`

3. **Settings → Pages**
   - Source: `gh-pages` branch
   - Dossier: `/` (root)

### Secrets requis
- `GITHUB_TOKEN` (automatique)
- `WORKFLOW_TOKEN` (PAT pour déclencher workflows depuis auto-merge)

## ⚠️ Limites et considérations

### 1. Preview Environments - Routing Hugo

Le `baseURL` devient : `https://username.github.io/repo/pr-123/`

**⚠️ Limitations :**
- ❌ Liens absolus cassent
- ❌ Canonical URLs pointent vers production
- ❌ Sitemap automatique peut casser
- ✅ Solution : Utilisez toujours des URLs relatives dans Hugo

### 2. SEO et indexation

**Protections en place :**
- ✅ Meta robots `noindex, nofollow` sur toutes les pages
- ✅ `robots.txt` bloquant tous les crawlers
- ✅ Bannière visuelle indiquant l'environnement de preview

### 3. Taille du repo gh-pages

**Problème :** Chaque preview ajoute des centaines de fichiers

**Solutions :**
- ✅ Nettoyage automatique à la fermeture de PR
- ✅ Suppression physique des dossiers `/pr-*/`
- ⚠️ Recommandation : Limiter le nombre de PRs ouvertes simultanément

### 4. Collisions et conflits

**Risque :** Deux PRs avec le même numéro (rare)

**Mitigation :**
- Les PRs d'un même repo ont des numéros uniques
- Les forks utilisent leurs propres Actions

## 🔧 Maintenance

### Nettoyer manuellement les previews
Si le cleanup automatique échoue :

```bash
git checkout gh-pages
git rm -rf pr-*
git commit -m "chore: cleanup old previews"
git push origin gh-pages
```

### Vérifier la taille du repo gh-pages
```bash
git clone --branch gh-pages --single-branch https://github.com/username/repo.git gh-pages-check
cd gh-pages-check
du -sh pr-*
```

### Forcer une release
```bash
# Via l'interface GitHub
Actions → 🏷️ Release → Run workflow → Choisir le type (major/minor/patch)
```

## 📊 Monitoring

### Vérifier les déploiements
- **Production :** https://centreloisirsfatima.com
- **Previews :** https://username.github.io/repo/pr-{numéro}/
- **Statut :** Settings → Environments

### Logs et debugging
- Actions → Workflow runs
- Chaque étape a des logs détaillés
- Les erreurs PostCSS/Dart Sass sont les plus fréquentes

## 🎯 Best Practices

1. **Commits :** Utilisez Conventional Commits pour le versioning automatique
2. **PRs :** Attendez l'approbation avant de merger (auto-merge configuré)
3. **Previews :** Testez sur l'URL de preview avant d'approuver
4. **Cleanup :** Fermez les PRs obsolètes pour libérer gh-pages
5. **Monitoring :** Vérifiez régulièrement la taille de gh-pages

## 🚨 Troubleshooting

### PostCSS errors
**Solution :** Vérifier que Node.js LTS et npm ci ont bien été exécutés

### Dart Sass not found
**Solution :** `sudo snap install dart-sass` est dans le workflow

### Preview ne charge pas les styles
**Solution :** Vérifier le baseURL dans le build Hugo

### Auto-merge ne fonctionne pas
**Solution :** Vérifier que "Allow auto-merge" est activé dans Settings

---

**Version :** 1.0.0  
**Dernière mise à jour :** 2026-06-06
