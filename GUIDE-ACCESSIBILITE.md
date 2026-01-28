# Guide des bonnes pratiques d'accessibilité

## Centre des Loisirs de Fatima

Ce document explique les améliorations d'accessibilité mises en place et comment maintenir l'accessibilité lors de l'ajout de nouveau contenu.

## ✅ Améliorations implémentées

### 1. **Styles CSS d'accessibilité personnalisés**

Fichier : `assets/scss/accessibility-improvements.scss`

**Fonctionnalités ajoutées :**

- Indicateurs de focus améliorés (contour de 3px)
- Contraste de couleurs amélioré (texte #1a1a1a sur fond blanc)
- Zones cliquables minimales de 44x44 pixels
- Support des préférences utilisateur (mouvement réduit, contraste élevé)
- Styles de formulaires accessibles
- Amélioration de la lisibilité (hauteur de ligne, espacement)

### 2. **Structure HTML sémantique**

- Changement de `<section id="content">` en `<main id="content">`
- Utilisation appropriée de `<header>`, `<nav>`, `<article>`, `<footer>`
- Liens "Aller au contenu" déjà présents

### 3. **Navigation au clavier**

- Tous les éléments interactifs sont accessibles au clavier
- Indicateurs de focus visibles
- Ordre de tabulation logique

### 4. **Contrastes de couleurs**

- Ratios de contraste respectant WCAG 2.1 AA (minimum 4.5:1)
- Liens soulignés pour une meilleure visibilité
- Couleurs primaires ajustées pour un meilleur contraste

## 📝 Bonnes pratiques pour le contenu

### Images

Toujours ajouter un texte alternatif descriptif :

```markdown
![Description de l'image](chemin/vers/image.jpg)
```

**Bon exemple :**

```markdown
![Groupe d'enfants jouant au soccer au Centre des Loisirs de Fatima](images/soccer-2024.jpg)
```

**Mauvais exemple :**

```markdown
![image](image.jpg)
```

Pour les images décoratives, utilisez un alt vide :

```markdown
![ ](decoration.png)
```

### Liens

Utilisez des textes de liens explicites :

**Bon :**

```markdown
[Consultez notre calendrier d'activités 2026](/activites/)
```

**Mauvais :**

```markdown
[Cliquez ici](/activites/)
```

### Titres

Respectez la hiérarchie des titres (ne sautez pas de niveaux) :

```markdown
# Titre principal (H1) - Un seul par page

## Section (H2)

### Sous-section (H3)

#### Sous-sous-section (H4)
```

### Tableaux

Utilisez toujours des en-têtes de colonnes :

```markdown
| Nom | Date | Lieu |
|-----|------|------|
| Bingo | 15 mars | Salle principale |
```

### Listes

Utilisez les listes appropriées :

```markdown
<!-- Liste non ordonnée -->
- Élément 1
- Élément 2

<!-- Liste ordonnée (avec ordre d'importance) -->
1. Première étape
2. Deuxième étape
```

### Contenu vidéo

Si vous ajoutez des vidéos :

- Incluez des sous-titres
- Fournissez une transcription textuelle
- Utilisez le shortcode YouTube du thème qui est accessible

### Couleurs

- N'utilisez jamais la couleur seule pour transmettre une information
- Exemple : "Cliquez sur le bouton vert" → "Cliquez sur le bouton Inscription"

### Formulaires

Structure recommandée :

```html
<label for="nom">Nom :</label>
<input type="text" id="nom" name="nom" required>

<label for="email">Courriel :</label>
<input type="email" id="email" name="email" required>
```

## 🔍 Tests d'accessibilité

### Tests manuels à effectuer régulièrement

1. **Navigation au clavier**
   - Utilisez uniquement la touche Tab
   - Vérifiez que tous les éléments sont accessibles
   - Vérifiez que les indicateurs de focus sont visibles

2. **Zoom**
   - Testez le site avec un zoom de 200%
   - Vérifiez qu'aucun contenu n'est coupé
   - Vérifiez que tout reste fonctionnel

3. **Lecteur d'écran**
   - Windows : NVDA (gratuit) ou JAWS
   - Mac : VoiceOver (intégré)
   - Vérifiez que le contenu est lu de façon logique

### Outils automatisés recommandés

1. **Extension navigateur : axe DevTools**
   - Analyse automatique des problèmes d'accessibilité
   - Gratuit et facile à utiliser

2. **WAVE Web Accessibility Evaluation Tool**
   - <https://wave.webaim.org/>
   - Visualisation des problèmes d'accessibilité

3. **Validateur HTML du W3C**
   - <https://validator.w3.org/>
   - Vérifie la validité du HTML

4. **Contrast Checker**
   - <https://webaim.org/resources/contrastchecker/>
   - Vérifie les ratios de contraste

## 🎯 Checklist avant publication

- [ ] Toutes les images ont un texte alternatif approprié
- [ ] Les liens ont un texte descriptif
- [ ] La hiérarchie des titres est respectée
- [ ] Les tableaux ont des en-têtes
- [ ] Les formulaires ont des labels
- [ ] Le contraste des couleurs est suffisant
- [ ] Le contenu est lisible avec un zoom de 200%
- [ ] La page est navigable au clavier
- [ ] Les vidéos ont des sous-titres (si applicable)

## 🔗 Ressources utiles

- [WCAG 2.1 en français](https://www.w3.org/Translations/WCAG21-fr/)
- [Introduction à l'accessibilité web](https://www.w3.org/WAI/fundamentals/accessibility-intro/fr)
- [Guide d'accessibilité du Gouvernement du Canada](https://www.canada.ca/fr/secretariat-conseil-tresor/services/communications-gouvernementales/specifications-contenu-architecture-information-canada/accessibilite-web.html)

## 💡 Rappel important

L'accessibilité n'est pas une tâche ponctuelle, c'est un processus continu. Chaque fois que vous ajoutez du contenu, pensez aux personnes qui utilisent :

- Des lecteurs d'écran
- La navigation au clavier uniquement
- Des outils de grossissement d'écran
- Des technologies d'assistance diverses

**Question à se poser :** "Si je ne pouvais pas utiliser ma souris ou voir l'écran, pourrais-je accéder à cette information ?"
