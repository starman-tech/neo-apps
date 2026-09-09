# FOCUS.OS

**Coach de concentration par vision par ordinateur.** La webcam surveille le poste de travail : téléphone sorti ou chaise vide, le chrono s'arrête.

![Type](https://img.shields.io/badge/type-single--file-000?style=flat-square)
![Stack](https://img.shields.io/badge/stack-TensorFlow.js%20%2B%20COCO--SSD-ff6f00?style=flat-square)
![Privacy](https://img.shields.io/badge/privacy-100%25%20local-4ade80?style=flat-square)

---

## Principe

Le modèle **COCO-SSD** tourne dans le navigateur sur le flux webcam et ne suit que deux classes :

| Détection | Effet |
| --- | --- |
| `person` absente | Session en pause, compteur **ABS** (absence) qui monte |
| `cell phone` présent | Session en pause, compteur **TEL** + écran de pénalité |
| Poste occupé, pas de téléphone | Chrono de travail qui tourne |

Le flux vidéo n'est jamais transmis : tout est traité dans l'onglet, image par image.

## Fonctionnalités

- **Deux modes** — chronomètre libre ou Pomodoro
- **Objectif de session** nommé, sauvegardé avec l'historique
- **Mode Calculatrice** — assouplit le seuil de détection pour ne pas confondre une calculatrice graphique avec un téléphone
- **Écran de pénalité** avec décompte lors d'une distraction
- **Historique local** des sessions (durée travaillée, temps téléphone, temps d'absence)
- **Deux thèmes** — `Brutal` / `Glass`, mémorisés dans le navigateur

## Versions

| Version | Apports |
| --- | --- |
| **V1** | Base : détection personne + téléphone, chrono, Pomodoro, historique |
| **V2** | Ajout du **mode Calculatrice** (seuil de détection tolérant) |
| **V3** | *Version de référence.* Boucle d'inférence régulée, **alerte sonore**, **Wake Lock** (l'écran ne s'éteint plus), compteur repris dans le titre de l'onglet, logo |

`V3/V3HID/` contient un build obfusqué de la V3, destiné à la distribution.

## Lancer

La webcam exige un contexte sécurisé — servir en HTTP local :

```bash
python3 -m http.server 8000
# → http://localhost:8000/Focus.os/V3/
```

Autoriser l'accès caméra, saisir un objectif, puis **GO**.

## Contraintes

- Le premier chargement télécharge les poids COCO-SSD (~30 Mo), ensuite mis en cache.
- La détection dépend de l'éclairage et du cadrage : la caméra doit voir le buste et le plan de travail.
- Le mode Calculatrice réduit volontairement la sensibilité — à n'activer que si nécessaire.

## Structure

```
Focus.os/
├── V1/index.html
├── V2/index.html
└── V3/
    ├── index.html      # version de référence
    ├── logo.png
    └── V3HID/          # build obfusqué
```
