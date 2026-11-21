# Gomme : référence API

Efface à la main des parties de l'image, avec une palette de pointes réglables

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/eraser` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image à gommer. |

## Réglages

### Traits

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `strokes` | [`BrushStroke[]`](#type-brushstroke)<br />*Liste d'objets* | `[]` |  | **Traits**<br />Traits de gomme, retirés de l'image dans l'ordre ; chacun garde sa pointe. Sans trait, l'image reste telle quelle.<br />*Liste d'objets* : Liste d'objets `BrushStroke`, détaillés ci-dessous ; un membre omis garde sa valeur par défaut.<br />Structure de BrushStroke[] et exemple : [`BrushStroke`](#type-brushstroke), [`StrokePoint`](#type-strokepoint) |

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
curl -X POST https://api.pixlub.com/v1/modules/eraser \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"strokes":[{"points":[[0.1,0.2],[0.3,0.25],[0.5,0.2]],"size":40,"hardness":100},{"points":[[0.8,0.8]],"size":120,"hardness":0,"opacity":50},{"points":[[0.25,0.2],[0.35,0.22]],"size":30,"mode":"restore"}]}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"strokes":[{"points":[[0.1,0.2],[0.3,0.25],[0.5,0.2]],"size":40,"hardness":100},{"points":[[0.8,0.8]],"size":120,"hardness":0,"opacity":50},{"points":[[0.25,0.2],[0.35,0.22]],"size":30,"mode":"restore"}]}))

const res = await fetch('https://api.pixlub.com/v1/modules/eraser', {
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
    "https://api.pixlub.com/v1/modules/eraser",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"strokes": [{"points": [[0.1, 0.2], [0.3, 0.25], [0.5, 0.2]], "size": 40, "hardness": 100}, {"points": [[0.8, 0.8]], "size": 120, "hardness": 0, "opacity": 50}, {"points": [[0.25, 0.2], [0.35, 0.22]], "size": 30, "mode": "restore"}]})},
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
result = client.tools.run("eraser", image="photo.png", params={"strokes": [{"points": [[0.1, 0.2], [0.3, 0.25], [0.5, 0.2]], "size": 40, "hardness": 100}, {"points": [[0.8, 0.8]], "size": 120, "hardness": 0, "opacity": 50}, {"points": [[0.25, 0.2], [0.35, 0.22]], "size": 30, "mode": "restore"}]})
result.save(f"eraser{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "eraser", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"strokes": []any{map[string]any{"points": []any{[]any{0.1, 0.2}, []any{0.3, 0.25}, []any{0.5, 0.2}}, "size": 40, "hardness": 100}, map[string]any{"points": []any{[]any{0.8, 0.8}}, "size": 120, "hardness": 0, "opacity": 50}, map[string]any{"points": []any{[]any{0.25, 0.2}, []any{0.35, 0.22}}, "size": 30, "mode": "restore"}}},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("eraser"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image dont les parties gommées sont devenues transparentes. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "eraser",
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

**Exemple de BrushStroke[]**

```json
[
  {
    "points": [
      [
        0.1,
        0.2
      ],
      [
        0.3,
        0.25
      ],
      [
        0.5,
        0.2
      ]
    ],
    "size": 40,
    "hardness": 100
  },
  {
    "points": [
      [
        0.8,
        0.8
      ]
    ],
    "size": 120,
    "hardness": 0,
    "opacity": 50
  },
  {
    "points": [
      [
        0.25,
        0.2
      ],
      [
        0.35,
        0.22
      ]
    ],
    "size": 30,
    "mode": "restore"
  }
]
```

<a name="type-brushstroke"></a>

### BrushStroke

*Objet*. Trait de brosse : les points parcourus, de 0 à 1 dans l'image, et la pointe qui les a suivis.

| Membre | Type | Description |
| --- | --- | --- |
| `points` | `StrokePoint[]` | Points du trait, dans l'ordre ; un seul point pose une empreinte. |
| `size` | `number` | *facultatif* · Diamètre de la pointe, en pixels de l'image. De 1 à 500 px. `20` par défaut. |
| `hardness` | `number` | *facultatif* · Netteté du bord, de 0 (fondu) à 100 (franc). De 0 à 100 %. `100` par défaut. |
| `flow` | `number` | *facultatif* · Force de chaque empreinte. De 1 à 100 %. `100` par défaut. |
| `opacity` | `number` | *facultatif* · Plafond du trait entier. De 1 à 100 %. `100` par défaut. |
| `mode` | `"erase" \| "restore"` | *facultatif* · Retirer, ou remettre une partie déjà gommée. `"erase"` par défaut. |

**Exemple**

```json
{
  "points": [
    [
      0.1,
      0.2
    ],
    [
      0.3,
      0.25
    ],
    [
      0.5,
      0.2
    ]
  ],
  "size": 40,
  "hardness": 100
}
```

<a name="type-strokepoint"></a>

### StrokePoint

*Tableau de 2 éléments, dans cet ordre*. Point d'un trait de brosse.

| Membre | Type | Description |
| --- | --- | --- |
| `[0]` | `number` | Position horizontale, de 0 (gauche) à 1 (droite) de l'image ; au-delà, la pointe déborde du bord. |
| `[1]` | `number` | Position verticale, de 0 (haut) à 1 (bas) de l'image. |

**Exemple**

```json
[
  0.5,
  0.3
]
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/eraser/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "strokes": {
      "title": "Strokes",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "points": {
            "title": "Points",
            "type": "array",
            "items": {
              "type": "array",
              "items": {
                "type": "number"
              },
              "minItems": 2,
              "maxItems": 2
            },
            "minItems": 1
          },
          "size": {
            "title": "Size",
            "default": 20,
            "type": "number",
            "minimum": 1,
            "maximum": 500
          },
          "hardness": {
            "title": "Hardness",
            "default": 100,
            "type": "number",
            "minimum": 0,
            "maximum": 100
          },
          "flow": {
            "title": "Flow",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 100
          },
          "opacity": {
            "title": "Opacity",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 100
          },
          "mode": {
            "title": "Mode",
            "default": "erase",
            "type": "string",
            "enum": [
              "erase",
              "restore"
            ]
          }
        },
        "required": [
          "points"
        ]
      }
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
