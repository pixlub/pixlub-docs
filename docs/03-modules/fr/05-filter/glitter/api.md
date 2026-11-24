# Paillettes : référence API

Couvre l'image de paillettes qui scintillent : facettes irisées, étoiles et reflet, en boucle.

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/glitter` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Une image ou plusieurs) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image pailletée ; sa transparence donne la forme couverte. |

## Réglages

### Paillettes

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"facet"` | `facet` Facettes : Éclats polygonaux jointifs, comme une feuille pailletée<br />`round` Rondes : Paillettes rondes séparées<br />`diamond` Losanges : Petits losanges orientés au hasard | **Forme**<br />Dessin de chaque éclat. |
| `size` | `number` | `6` | min 1 px · max 80 px · pas de 0.5 | **Taille**<br />Taille d'un éclat, en pixels de l'image. |
| `sizeVariation` | `number` | `40` | min 0 % · max 100 % | **Variation de taille**<br />Écart de taille entre les éclats.<br />*Pris en compte quand `shape` = `round` (Rondes) ou `diamond` (Losanges).* |
| `density` | `number` | `65` | min 0 % · max 100 % | **Densité**<br />Part de la surface couverte d'éclats. |
| `gap` | `number` | `12` | min 0 % · max 100 % | **Joint**<br />Espace entre deux facettes.<br />*Pris en compte quand `shape` = `facet` (Facettes).* |
| `seed` | `number` | `1` | min 0 | **Graine**<br />Change le tirage des éclats ; une même graine redonne le même semis. |

### Couleurs

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `colors` | [`ColorGradient`](#type-colorgradient)<br />*Dégradé* | [JSON](#default-colors) |  | **Couleurs**<br />Couleurs des éclats, tirées le long de ce dégradé. Une couleur transparente laisse des éclats invisibles.<br />Structure de ColorGradient et exemple : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `colorMode` | `string` | `"iridescent"` | `iridescent` Irisée : Les couleurs ondulent sur la surface et glissent avec le temps, comme un hologramme<br />`random` Aléatoire : Chaque éclat garde sa couleur | **Répartition**<br />Façon de répartir les couleurs du dégradé. |
| `opacity` | `number` | `70` | min 0 % · max 100 % | **Opacité**<br />Couvrance des éclats sur l'image. |
| `blend` | `string` | `"overlay"` | `normal` Normale<br />`screen` Superposition claire<br />`overlay` Incrustation<br />`lighten` Éclaircir | **Fusion**<br />Mélange des éclats avec l'image : en incrustation ou superposition claire, le dessin reste lisible dessous. |

<a name="default-colors"></a>

**Valeur par défaut de `colors`**

```json
{
  "stops": [
    {
      "color": "#ffb3e6",
      "at": 0
    },
    {
      "color": "#ffe6a3",
      "at": 20
    },
    {
      "color": "#b5ffd8",
      "at": 40
    },
    {
      "color": "#a6e3ff",
      "at": 60
    },
    {
      "color": "#cdb6ff",
      "at": 80
    },
    {
      "color": "#ffb3e6",
      "at": 100
    }
  ]
}
```

### Éclat

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `brightness` | `number` | `100` | min 0 % · max 200 % | **Luminosité**<br />Luminosité des éclats et des étoiles. |
| `twinkle` | `number` | `70` | min 0 % · max 100 % | **Scintillement**<br />Écart entre un éclat éteint et allumé. |
| `glints` | `number` | `35` | min 0 % · max 100 % | **Étoiles**<br />Nombre d'éclats qui jettent une brève étoile. |
| `glintSize` | `number` | `16` | min 0 px · max 200 px · pas de 1 | **Taille des étoiles**<br />Longueur d'une branche d'étoile. |
| `glintsOutside` | `boolean` | `true` |  | **Étoiles hors de la forme**<br />Les étoiles débordent de la forme, comme un vrai reflet. |
| `sheen` | `number` | `40` | min 0 % · max 100 % | **Reflet**<br />Bande de lumière qui balaie la surface une fois par cycle. |
| `sheenAngle` | `number` | `35` | min -180 ° · max 180 ° | **Angle du reflet**<br />Direction du balayage. |
| `sheenWidth` | `number` | `25` | min 2 % · max 100 % | **Largeur du reflet**<br />Largeur de la bande de lumière. |

### Animation

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `animate` | `boolean` | `true` |  | **Animer**<br />Les paillettes scintillent dans la timeline ; décoché, l'image reste fixe. |
| `cycle` | `number` | `2` | min 0.2 s · max 20 s · pas de 0.1 | **Durée du cycle**<br />Durée d'une boucle complète, sans raccord visible.<br />*Pris en compte quand `animate` = `true`.* |
| `area` | `string` | `"shape"` | `shape` Forme : Seulement sur la partie opaque de l'image<br />`whole` Toute l'image : Partout, transparence comprise | **Zone**<br />Où les paillettes se posent. |

#### Phase

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `phaseDriven` | `boolean` | `false` |  | **Piloter par phase**<br />Le scintillement suit la phase posée en clés plutôt que le temps.<br />*Pris en compte quand `animate` = `true`.* |
| `phase` | `number` | `0` | min 0 % · max 100 % · pas de 0.1 | **Phase**<br />Instant montré, de 0 % (début) à 100 % (fin de l’animation).<br />*Pris en compte quand `phaseDriven` = `true`.* |

### Taille

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `frameMethod` | `string` | `"module"` | `module` Module : Le module agrandit ou réduit l'image selon ce qu'il produit.<br />`source` Source : Le rendu garde la taille de l'image reçue.<br />`custom` Libre : Le rendu prend la largeur et la hauteur choisies. | **Méthode**<br />D'où vient la taille du rendu. |
| `frameWidth` | `number` |  | min 1 px · max 16384 px | **Largeur**<br />Largeur du rendu, en pixels.<br />*Pris en compte quand `frameMethod` = `custom` (Libre).* |
| `frameHeight` | `number` |  | min 1 px · max 16384 px | **Hauteur**<br />Hauteur du rendu, en pixels.<br />*Pris en compte quand `frameMethod` = `custom` (Libre).* |
| `frameFit` | `string` | `"none"` | `none` Aucun (recadre) : Le rendu garde son échelle et se recadre.<br />`contain` Contenir : Le rendu entier tient dans la taille.<br />`cover` Couvrir : Le rendu remplit la taille, quitte à déborder.<br />`stretch` Étirer : Le rendu s'étire à la taille, sans garder ses proportions. | **Ajustement**<br />Comment le rendu se place dans la taille imposée.<br />*Pris en compte quand `frameMethod` = `source` (Source) ou `custom` (Libre).* |
| `frameAnchor` | `string`<br />*Ancrage* | `"center"` | [grille ci-dessous](#anchor-frameanchor) | **Ancrage**<br />Côté où le rendu s'accroche.<br />*Pris en compte quand `frameMethod` = `source` (Source) ou `custom` (Libre) et `frameFit` = `none` (Aucun (recadre)) ou `contain` (Contenir) ou `cover` (Couvrir).*<br />*Ancrage* : Point d'une grille 3 × 3, du coin haut gauche au coin bas droit. |

<a name="anchor-frameanchor"></a>

**Positions de `frameAnchor`**

| | Gauche | Centre | Droite |
| --- | --- | --- | --- |
| **Haut** | `top-left`<br />En haut à gauche | `top`<br />En haut | `top-right`<br />En haut à droite |
| **Milieu** | `left`<br />À gauche | **`center`**<br />**Au centre** | `right`<br />À droite |
| **Bas** | `bottom-left`<br />En bas à gauche | `bottom`<br />En bas | `bottom-right`<br />En bas à droite |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/glitter \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"shape":"facet","size":6,"density":65}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"shape":"facet","size":6,"density":65}))

const res = await fetch('https://api.pixlub.com/v1/modules/glitter', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/glitter",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"shape": "facet", "size": 6, "density": 65})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("glitter", image="photo.png", params={"shape": "facet", "size": 6, "density": 65})
result.save(f"glitter{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "glitter", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"shape": "facet", "size": 6, "density": 65},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("glitter"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

### 1 fichier

> **1 fichier** : Une seule image dans `in`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produite par le module.<br />Une seule image envoyée : le fichier garde la clé `out`. |

### Plusieurs fichiers

> **Plusieurs fichiers** : Plusieurs images dans `in`, jusqu'à 64 : leur nombre se déduit des fichiers envoyés, vous ne l'envoyez pas.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Image(s)**<br />Image produite par le module.<br />Plusieurs images envoyées dans `in` : un fichier par image, sous les clés `out#0`, `out#1`…, dans l'ordre d'envoi. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "glitter",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 1,
    "balance": 190
  }
}
```

## Types

Les valeurs structurées des réglages, détaillées comme des classes : chaque membre avec son type, puis un exemple.

<a name="type-colorgradient"></a>

### ColorGradient

*Objet*. Dégradé de couleurs : des arrêts placés le long d'un axe, et la façon de les étaler.

| Membre | Type | Description |
| --- | --- | --- |
| `stops` | `GradientStop[]` | Arrêts de couleur, au moins deux, dans n'importe quel ordre. |
| `type` | `"linear" \| "radial"` | *facultatif* · Linéaire le long de `angle`, ou en cercles depuis le centre. `linear` par défaut ; sans effet quand seul l'ordre des couleurs compte (Mappe dégradé). |
| `angle` | `number` | *facultatif* · Direction d'un dégradé linéaire, en degrés : 0 vers le haut, 90 vers la droite. `90` par défaut. |

**Exemple**

```json
{
  "type": "linear",
  "angle": 90,
  "stops": [
    {
      "color": "#140a2e",
      "at": 0
    },
    {
      "color": "#c264c2",
      "at": 55
    },
    {
      "color": "#ffffff",
      "at": 100
    }
  ]
}
```

<a name="type-gradientstop"></a>

### GradientStop

*Objet*. Arrêt d'un dégradé.

| Membre | Type | Description |
| --- | --- | --- |
| `color` | `Color` | Couleur CSS de l'arrêt ; l'alpha (`#rrggbbaa`) est gardé. |
| `at` | `number` | Position de l'arrêt, de 0 (début) à 100 (fin), en %. |

**Exemple**

```json
{
  "color": "#c264c2",
  "at": 55
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/glitter/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "shape": {
      "title": "Shape",
      "default": "facet",
      "type": "string",
      "enum": [
        "facet",
        "round",
        "diamond"
      ]
    },
    "size": {
      "title": "Size",
      "default": 6,
      "type": "number",
      "minimum": 1,
      "maximum": 80,
      "multipleOf": 0.5
    },
    "sizeVariation": {
      "title": "Size variation",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "density": {
      "title": "Density",
      "default": 65,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "gap": {
      "title": "Gap",
      "default": 12,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "seed": {
      "title": "Seed",
      "default": 1,
      "type": "number",
      "minimum": 0
    },
    "colors": {
      "title": "Colors",
      "default": {
        "stops": [
          {
            "color": "#ffb3e6",
            "at": 0
          },
          {
            "color": "#ffe6a3",
            "at": 20
          },
          {
            "color": "#b5ffd8",
            "at": 40
          },
          {
            "color": "#a6e3ff",
            "at": 60
          },
          {
            "color": "#cdb6ff",
            "at": 80
          },
          {
            "color": "#ffb3e6",
            "at": 100
          }
        ]
      },
      "type": "object",
      "required": [
        "stops"
      ],
      "properties": {
        "stops": {
          "type": "array",
          "items": {
            "type": "object",
            "required": [
              "color",
              "at"
            ],
            "properties": {
              "color": {
                "type": "string",
                "minLength": 1
              },
              "at": {
                "type": "number",
                "minimum": 0,
                "maximum": 100
              }
            }
          },
          "minItems": 2
        }
      }
    },
    "colorMode": {
      "title": "Distribution",
      "default": "iridescent",
      "type": "string",
      "enum": [
        "iridescent",
        "random"
      ]
    },
    "opacity": {
      "title": "Opacity",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "blend": {
      "title": "Blend",
      "default": "overlay",
      "type": "string",
      "enum": [
        "normal",
        "screen",
        "overlay",
        "lighten"
      ]
    },
    "brightness": {
      "title": "Brightness",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 200
    },
    "twinkle": {
      "title": "Twinkle",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "glints": {
      "title": "Glints",
      "default": 35,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "glintSize": {
      "title": "Glint size",
      "default": 16,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    },
    "glintsOutside": {
      "title": "Glints past the edge",
      "default": true,
      "type": "boolean"
    },
    "sheen": {
      "title": "Sheen",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "sheenAngle": {
      "title": "Sheen angle",
      "default": 35,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "sheenWidth": {
      "title": "Sheen width",
      "default": 25,
      "type": "number",
      "minimum": 2,
      "maximum": 100
    },
    "animate": {
      "title": "Animate",
      "default": true,
      "type": "boolean"
    },
    "cycle": {
      "title": "Cycle length",
      "default": 2,
      "type": "number",
      "minimum": 0.2,
      "maximum": 20,
      "multipleOf": 0.1
    },
    "area": {
      "title": "Area",
      "default": "shape",
      "type": "string",
      "enum": [
        "shape",
        "whole"
      ]
    },
    "phaseDriven": {
      "title": "Drive by phase",
      "default": false,
      "type": "boolean"
    },
    "phase": {
      "title": "Phase",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "frameMethod": {
      "title": "Method",
      "default": "module",
      "type": "string",
      "enum": [
        "module",
        "source",
        "custom"
      ]
    },
    "frameWidth": {
      "title": "Width",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameHeight": {
      "title": "Height",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameFit": {
      "title": "Fit",
      "default": "none",
      "type": "string",
      "enum": [
        "none",
        "contain",
        "cover",
        "stretch"
      ]
    },
    "frameAnchor": {
      "title": "Anchor",
      "default": "center",
      "type": "string",
      "enum": [
        "top-left",
        "top",
        "top-right",
        "left",
        "center",
        "right",
        "bottom-left",
        "bottom",
        "bottom-right"
      ]
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
