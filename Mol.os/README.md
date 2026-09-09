# MOL.OS

**Visualiseur moléculaire 3D et animateur de réactions.** Tape un nom ou un SMILES, obtiens la structure en 3D manipulable.

![Type](https://img.shields.io/badge/type-single--file-000?style=flat-square)
![Stack](https://img.shields.io/badge/stack-3Dmol.js-3b82f6?style=flat-square)
![Data](https://img.shields.io/badge/data-PubChem%20(NIH)-a855f7?style=flat-square)

---

## Principe

Les structures sont récupérées en direct sur l'API **PubChem** (NIH) au format SDF 3D, puis rendues par **3Dmol.js** dans un canvas WebGL. Si la molécule n'existe pas en 3D dans la base, l'app retombe automatiquement sur la version 2D.

Deux modes de recherche :

- **NOM** — `Aspirin`, `Caffeine`, `Glucose`, `Water`…
- **SMILES** — notation chimique linéaire, ex. `CC(=O)OC1=CC=CC=C1C(=O)O`

## Fonctionnalités

- **Rendu 3D interactif** — rotation, zoom, rotation automatique
- **Styles de représentation** — bâtons, sphères, lignes, ou vue **2D topologique**
- **Panneau d'infos** — source des données et étiquettes de la molécule courante
- **Raccourcis** vers des molécules courantes
- **Deux thèmes** — `Brutal` / `Glass`

## Versions

| Version | Apports |
| --- | --- |
| **V1** | Visualiseur universel : recherche nom / SMILES, styles de rendu, vue 2D |
| **V2** | *Version de référence.* Ajout du **module Réactions** : animation interpolée entre l'état initial et l'état final (combustion du méthane, formation de l'eau…), via parsing de trajectoires XYZ |

`V1/V1HID/` et `V2/V1HID/` contiennent les builds obfusqués correspondants.

## Lancer

Aucune compilation. Il suffit d'ouvrir le fichier — ou, pour éviter tout blocage réseau du navigateur :

```bash
python3 -m http.server 8000
# → http://localhost:8000/Mol.os/V2/
```

## Contraintes

- Une **connexion internet** est nécessaire : les structures viennent de PubChem, pas d'une base locale.
- Les réactions animées sont des **interpolations pédagogiques** entre deux géométries, pas des simulations de dynamique moléculaire.

## Structure

```
Mol.os/
├── V1/
│   ├── index.html
│   └── V1HID/          # build obfusqué
└── V2/
    ├── index.html      # version de référence
    └── V1HID/          # build obfusqué
```
