# PHOTO.TGR

**Renommage et tri de photos en masse, 100 % local.** Un dossier entre, un ZIP nommé proprement et un récapitulatif sortent.

![Type](https://img.shields.io/badge/type-single--file-000?style=flat-square)
![Stack](https://img.shields.io/badge/stack-JSZip-000?style=flat-square)
![Privacy](https://img.shields.io/badge/privacy-100%25%20local-4ade80?style=flat-square)

---

## Principe

Le dossier est lu directement par le navigateur (`webkitdirectory`). Chaque photo reçoit une **localisation**, et l'export produit un ZIP dont les fichiers suivent une convention stricte :

```
<appareil>_<localisation>_<numéro>_matteocean.<ext>
        ex.  dji_calanques_007_matteocean.jpg
```

Aucune image n'est envoyée nulle part : lecture, vignettes, scoring et compression se font dans l'onglet.

## Fonctionnalités

- **Import de dossier complet**, avec barre de progression et génération de vignettes
- **Deux appareils** — DJI (drone) ou GoPro, qui pilotent le préfixe des noms
- **Deux vues de travail**
  - **Grille** — vue d'ensemble, saisie rapide des localisations
  - **Tinder** — une photo à la fois, en plein écran, pour trier au clavier sans réfléchir
- **Score qualité** calculé sur le petit côté de l'image, gradué de `INSUFFISANT` à `PARFAIT` — il indique jusqu'à quel format la photo reste imprimable
- **Statistiques live** sur le lot en cours
- **Export ZIP** contenant les fichiers renommés et un récapitulatif `_recap_matteocean.txt`
- **Deux thèmes** — `Brutal` / `Glass`

## Lancer

```bash
python3 -m http.server 8000
# → http://localhost:8000/photo.tgr/phototagger_matteocean.html
```

Charger un dossier → renseigner les localisations (grille ou mode Tinder) → **EXPORTER**.

## Contraintes

- L'import de dossier repose sur `webkitdirectory` : **Chrome / Edge recommandés** (support partiel ailleurs).
- Tout passe par la mémoire du navigateur — sur un lot très volumineux (plusieurs Go), traiter par paquets.
- Le score est une mesure de **définition**, pas de netteté ni de composition.

## Structure

```
photo.tgr/
└── phototagger_matteocean.html    # application complète
```
