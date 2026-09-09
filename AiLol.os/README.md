# AILOL.OS

**Chat LLM 100 % local, dans le navigateur.** Aucune clé API, aucun serveur, aucune donnée qui sort de la machine.

![Type](https://img.shields.io/badge/type-single--file-000?style=flat-square)
![Stack](https://img.shields.io/badge/stack-WebLLM%20%2F%20Transformers.js-4ade80?style=flat-square)
![Runtime](https://img.shields.io/badge/runtime-WebGPU%20%7C%20WASM-3b82f6?style=flat-square)

---

## Principe

Au chargement, l'app teste le GPU du poste et choisit son moteur d'inférence :

| Moteur | Condition | Modèles disponibles |
| --- | --- | --- |
| **WebLLM** (MLC) | WebGPU disponible | Llama 3.2 1B · Gemma 2 2B · Llama 3.2 3B |
| **Transformers.js** | Fallback CPU / WASM | TinyLlama 1.1B · Qwen 1.5 0.5B |

Les poids sont téléchargés une fois depuis le CDN, puis mis en cache par le navigateur. L'inférence, elle, ne quitte jamais la machine.

## Fonctionnalités

- **Sélection de modèle** avec barre de progression de téléchargement
- **Télémétrie temps réel** — tokens/seconde, latence du 1er token (TTFT), temps total, tokens générés
- **System prompt** et **température** réglables à chaud
- **Deux thèmes** — `Brutal` (néo-brutaliste, Space Mono) et `Glass` (sombre, glassmorphism)
- Détection matérielle affichée dans la barre supérieure

## Lancer

L'app utilise des modules ES : elle doit être servie en HTTP (l'ouvrir en `file://` ne fonctionnera pas).

```bash
python3 -m http.server 8000
# → http://localhost:8000/AiLol.os/
```

Puis : choisir un modèle → **INITIALISER** → attendre le téléchargement → écrire.

## Contraintes

- Le premier chargement d'un modèle pèse de **300 Mo à 2 Go** selon la sélection.
- WebGPU exige un navigateur récent (Chrome / Edge 113+, Safari 17.4+).
- Sans WebGPU, le mode WASM reste fonctionnel mais nettement plus lent.

## Structure

```
AiLol.os/
└── index.html    # application complète (UI + logique + styles)
```
