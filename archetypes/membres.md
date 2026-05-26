---
# Prénom et nom du membre
name: "{{ replace .File.ContentBaseName "-" " " | title }}"

# Titre/rôle au sein du CA
titre: ""

# Courte description (optionnelle pour l'instant)
description: ""

# Chemin vers la photo (relative à /static)
# ex: "img/equipe/prenom-nom.jpg"
photo: "img/equipe/Personne.png"

# Ordre d'affichage (1 = premier)
weight: 99

# Ne pas modifier
membre_ca: true
draft: false
---
