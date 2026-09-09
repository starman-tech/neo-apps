<div align="center">

# NEO APP

**Une collection d'outils web autonomes — un fichier, zéro backend, tout tourne dans le navigateur.**

![Apps](https://img.shields.io/badge/apps-5-000?style=flat-square)
![Build](https://img.shields.io/badge/build-none-4ade80?style=flat-square)
![Backend](https://img.shields.io/badge/backend-none-3b82f6?style=flat-square)
![Style](https://img.shields.io/badge/design-neo--brutalism-a855f7?style=flat-square)

</div>

---

## Le principe

Chaque projet de ce dépôt est **une seule page HTML**. Pas de `npm install`, pas de bundler, pas de serveur applicatif, pas de compte à créer. On ouvre le fichier, ça marche.

Les traitements lourds — inférence LLM, détection d'objets, géométrie 3D, compression — s'exécutent **côté client**, sur la machine de l'utilisateur. Les seules requêtes réseau servent à charger les librairies depuis un CDN ou à interroger une API publique ouverte, jamais à transmettre des données personnelles.

L'ensemble partage la même identité visuelle : un néo-brutalisme assumé (bordures épaisses, ombres portées nettes, `Space Mono`) doublé d'un thème alternatif `Glass` sombre.

## Les applications

| Projet | En une ligne | Cœur technique |
| --- | --- | --- |
| **[AILOL.OS](AiLol.os/)** | Chat avec un LLM tournant entièrement sur votre machine | WebLLM (WebGPU) · Transformers.js (WASM) |
| **[FOCUS.OS](Focus.os/)** | Coach de concentration : la webcam met le chrono en pause si vous prenez votre téléphone | TensorFlow.js · COCO-SSD |
| **[MOL.OS](Mol.os/)** | Visualiseur moléculaire 3D et animateur de réactions | 3Dmol.js · API PubChem |
| **[SPOTIFY.STL](Spotify.stl/)** | Transforme un lien Spotify en porte-clés imprimable en 3D | three.js · STLExporter |
| **[PHOTO.TGR](photo.tgr/)** | Renommage, notation et tri d'un dossier photo entier, puis export ZIP | JSZip · Canvas |

Chaque dossier contient son propre README détaillé : fonctionnalités, historique des versions, contraintes.

---

### AILOL.OS — *IA locale*

Détecte le GPU, charge un modèle (Llama 3.2, Gemma 2, TinyLlama, Qwen) et discute sans jamais envoyer un octet vers un serveur. Affiche la télémétrie en direct : tokens/seconde, latence du premier token, tokens consommés. System prompt et température réglables.

### FOCUS.OS — *Concentration surveillée*

COCO-SSD tourne sur le flux webcam et cherche deux choses : êtes-vous là, et avez-vous un téléphone en main ? Le chrono de travail ne tourne que si la réponse est *oui / non*. Modes chronomètre et Pomodoro, historique des sessions, mode Calculatrice pour éviter les faux positifs en prépa. La vidéo ne quitte jamais l'onglet.

### MOL.OS — *Chimie 3D*

Recherche par nom courant ou par SMILES sur PubChem, rendu WebGL manipulable, plusieurs styles de représentation et une vue 2D topologique. La V2 ajoute un module d'animation de réactions par interpolation de géométries.

### SPOTIFY.STL — *Du son à l'objet*

Récupère le Spotify Code d'un titre, d'un album ou d'une playlist, l'analyse pixel par pixel, reconstruit ses barres en volume et exporte un STL prêt pour l'imprimante : forme de plaque, texte gravé, logo, forme du trou et cotes en millimètres.

### PHOTO.TGR — *Post-production de masse*

Charge un dossier entier, attribue une localisation à chaque cliché (vue grille ou mode « Tinder » plein écran), note la définition de chaque image sur une échelle d'imprimabilité, et exporte un ZIP renommé selon une convention stricte, accompagné d'un récapitulatif.

---

## Démarrage

Certaines apps utilisent des modules ES ou la webcam, ce qui interdit l'ouverture en `file://`. Le plus simple est de servir la racine du dépôt :

```bash
git clone https://github.com/<user>/<repo>.git
cd <repo>
python3 -m http.server 8000
```

Puis, dans le navigateur :

| App | URL |
| --- | --- |
| AILOL.OS | `http://localhost:8000/AiLol.os/` |
| FOCUS.OS | `http://localhost:8000/Focus.os/V3/` |
| MOL.OS | `http://localhost:8000/Mol.os/V2/` |
| SPOTIFY.STL | `http://localhost:8000/Spotify.stl/V2/` |
| PHOTO.TGR | `http://localhost:8000/photo.tgr/phototagger_matteocean.html` |

Navigateur recommandé : **Chrome ou Edge récent** (WebGPU pour AILOL.OS, `webkitdirectory` pour PHOTO.TGR).

## Conventions du dépôt

- **Versions** — les projets qui ont évolué conservent leur historique dans des dossiers `V1/`, `V2/`, `V3/`. La version la plus élevée est la version de référence ; les précédentes sont gardées telles quelles.
- **Dossiers `*HID/`** — builds obfusqués d'une version, destinés à la distribution. Le code lisible est toujours le `index.html` du dossier parent.
- **Dépendances** — chargées par CDN, épinglées dans le `<head>` de chaque page. Rien à installer.

## Confidentialité

Aucun projet n'embarque de tracker, d'analytics ou de collecte. Les données qui restent en mémoire d'une session (historique de FOCUS.OS, préférence de thème) sont stockées dans le `localStorage` du navigateur et n'en sortent pas.

## Licence

[MIT](LICENSE) — © Matteo (`@matteocean`)
