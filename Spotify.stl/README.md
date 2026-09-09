# SPOTIFY.STL

**Générateur de porte-clés Spotify prêts à imprimer.** Un lien Spotify entre, un fichier STL imprimable en 3D sort.

![Type](https://img.shields.io/badge/type-single--file-000?style=flat-square)
![Stack](https://img.shields.io/badge/stack-three.js-1db954?style=flat-square)
![Export](https://img.shields.io/badge/export-STL-000?style=flat-square)

---

## Principe

1. Le lien Spotify est converti en URI (`spotify:track:…`), puis le **Spotify Code** correspondant est récupéré en image.
2. L'image est analysée pixel par pixel dans un canvas pour détecter chaque barre du code et mesurer sa hauteur.
3. Les barres sont reconstruites en géométrie 3D avec **three.js**, fusionnées avec la plaque de base, le logo et le texte.
4. Le résultat est exporté en **STL** via `STLExporter`.

Une image de code peut aussi être déposée directement en drag & drop, sans passer par un lien.

## Fonctionnalités

- **Aperçu 3D temps réel** — orbite, zoom, grille de référence
- **Formes de plaque** — Stadium (arrondi), Standard (rectangle), Framed (avec cadre, rect ou arrondi)
- **Texte personnalisé** gravé en relief
- **Logo Spotify** optionnel
- **Trou de porte-clés** — cercle, carré, cœur ou étoile, taille réglable
- **Cotes d'impression** — épaisseur de base et relief du code en millimètres
- **Aperçu bicolore** base / code, pour anticiper un changement de filament

## Versions

| Version | Apports |
| --- | --- |
| **V1** | Génération complète, plaque rectangulaire, formes de trou, export STL |
| **V2** | *Version de référence.* Ajout des **styles de plaque** (Stadium / Framed) et des géométries capsule associées |

`V1/V1HID/` et `V2/V2HID/` contiennent les builds obfusqués correspondants.

## Lancer

L'app utilise un import map et des modules ES : elle doit être servie en HTTP.

```bash
python3 -m http.server 8000
# → http://localhost:8000/Spotify.stl/V2/
```

Coller un lien → **GÉNÉRER** → ajuster les paramètres → **EXPORT STL**.

## Contraintes

- Une **connexion internet** est requise : le Spotify Code est récupéré en ligne (via un proxy d'image pour contourner CORS) et three.js est chargé depuis un CDN.
- L'analyse suppose un code Spotify **en barres claires sur fond sombre, largeur 640 px** — c'est le format demandé automatiquement à partir d'un lien, à reproduire en cas d'import manuel.
- Pour l'impression : prévoir un relief de code suffisant (≥ 0,6 mm) pour rester lisible après la buse.

## Structure

```
Spotify.stl/
├── V1/
│   ├── index.html
│   └── V1HID/          # build obfusqué
└── V2/
    ├── index.html      # version de référence
    └── V2HID/          # build obfusqué
```
