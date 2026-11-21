# Floutage de visages : référence API

Floute des zones tracées à la main, ou détecte les visages via IA (nos services). Les zones sont éditables dans la préview : créer, déplacer, redimensionner, supprimer.

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/faceBlurApi` | 10 crédits par fichier quand `mode` vaut `auto` ; 1 crédit par fichier avec une autre valeur de `mode` |

> Ce module n'appelle le service distant que lorsque mode vaut « auto ». Avec un autre réglage, l'API le calcule elle-même, au tarif d'un module standard.

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `image` (Image seule) | oui | `PNG`, `JPEG`, `WebP` | **Image**<br />Image dont les zones sont floutées. En mode automatique, elle est envoyée au serveur pour y détecter les visages. |

## Réglages

### Détection

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `mode` | `string` | `"manual"` | `manual` Manuel : Vous tracez les zones à flouter.<br />`auto` Automatique : Nos services détecte les visages. | **Mode**<br />Mode de détection des zones à flouter. |

### Flou

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `radius` | `number` | `18` | min 1 px · max 60 px | **Intensité**<br />Intensité du flou appliqué aux zones. |

### Zones

> Ces réglages ne comptent que quand `mode` = `manual` (Manuel).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `zones` | [`BlurZone[]`](#type-blurzone)<br />*Liste d'objets* | `[]` |  | **Zones**<br />Liste des zones à flouter.<br />*Liste d'objets* : Liste d'objets `BlurZone`, détaillés ci-dessous ; un membre omis garde sa valeur par défaut.<br />Structure de BlurZone[] et exemple : [`BlurZone`](#type-blurzone) |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/faceBlurApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F 'params={"zones":[{"x":0.42,"y":0.18,"w":0.16,"h":0.24,"shape":"circle"},{"x":0.05,"y":0.8,"w":0.3,"h":0.12}],"mode":"manual","radius":18}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('params', JSON.stringify({"zones":[{"x":0.42,"y":0.18,"w":0.16,"h":0.24,"shape":"circle"},{"x":0.05,"y":0.8,"w":0.3,"h":0.12}],"mode":"manual","radius":18}))

const res = await fetch('https://api.pixlub.com/v1/modules/faceBlurApi', {
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
    "https://api.pixlub.com/v1/modules/faceBlurApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb"))],
    data={"params": json.dumps({"zones": [{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, {"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}], "mode": "manual", "radius": 18})},
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
result = client.tools.run("faceBlurApi", inputs={"image": "image.png"}, params={"zones": [{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, {"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}], "mode": "manual", "radius": 18})
result.save(f"faceBlurApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "faceBlurApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
    },
    Params: map[string]any{"zones": []any{map[string]any{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, map[string]any{"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}}, "mode": "manual", "radius": 18},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("faceBlurApi"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produite par le module. |
| `data` | [`FaceDetection`](#type-facedetection) | `JSON` | **Données**<br />Données détectées par le service distant, en JSON.<br />Contenu du fichier : un objet `FaceDetection`.<br />Rendue seulement quand `mode` = `auto`. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "faceBlurApi",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    },
    {
      "key": "data",
      "name": "data",
      "url": "https://files.pixlub.com/r/5f0c2a91-8d3e-4b7a-a1c4-6e2d9b0f3a58_result.json?exp=1767268800&sig=…",
      "content_type": "application/json",
      "bytes": 82
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 10,
    "balance": 190
  }
}
```

## Types

Les valeurs structurées des réglages, détaillées comme des classes : chaque membre avec son type, puis un exemple.

**Exemple de BlurZone[]**

```json
[
  {
    "x": 0.42,
    "y": 0.18,
    "w": 0.16,
    "h": 0.24,
    "shape": "circle"
  },
  {
    "x": 0.05,
    "y": 0.8,
    "w": 0.3,
    "h": 0.12
  }
]
```

<a name="type-blurzone"></a>

### BlurZone

*Objet*. Zone floutée : un rectangle, ou l'ellipse qu'il contient, placé de 0 à 1 dans l'image.

| Membre | Type | Description |
| --- | --- | --- |
| `x` | `number` | Bord gauche, de 0 (gauche) à 1 (droite) de l'image. De 0 à 1. |
| `y` | `number` | Bord haut, de 0 (haut) à 1 (bas) de l'image. De 0 à 1. |
| `w` | `number` | Largeur, en fraction de la largeur de l'image. De 0 à 1. |
| `h` | `number` | Hauteur, en fraction de la hauteur de l'image. De 0 à 1. |
| `shape` | `"square" \| "circle"` | *facultatif* · Rectangle, ou ellipse inscrite dans le rectangle. `"square"` par défaut. |

**Exemple**

```json
{
  "x": 0.42,
  "y": 0.18,
  "w": 0.16,
  "h": 0.24,
  "shape": "circle"
}
```

<a name="type-facedetection"></a>

### FaceDetection

*Objet*. Visages détectés dans l'image envoyée, en pixels de cette image.

| Membre | Type | Description |
| --- | --- | --- |
| `image_width` | `integer` | Largeur de l'image analysée, en pixels. |
| `image_height` | `integer` | Hauteur de l'image analysée, en pixels. |
| `faces_count` | `integer` | Nombre de visages trouvés, quelle que soit leur confiance. |
| `faces` | `DetectedFace[]` | Les visages trouvés. Seuls ceux de confiance `0.6` ou plus sont floutés. |

**Exemple**

```json
{
  "image_width": 1280,
  "image_height": 853,
  "faces_count": 1,
  "faces": [
    {
      "bbox": {
        "x": 512.4,
        "y": 188.9,
        "width": 164.2,
        "height": 211.7
      },
      "landmarks": {
        "right_eye": [
          561.3,
          268.1
        ],
        "left_eye": [
          628.8,
          266.4
        ],
        "nose_tip": [
          596.2,
          307.5
        ],
        "right_mouth": [
          567.9,
          345.2
        ],
        "left_mouth": [
          622.4,
          343.8
        ]
      },
      "confidence": 0.9731
    }
  ]
}
```

<a name="type-detectedface"></a>

### DetectedFace

*Objet*. Un visage détecté.

| Membre | Type | Description |
| --- | --- | --- |
| `bbox` | `FaceBox` | Cadre du visage, borné à l'image. |
| `landmarks` | `FaceLandmarks` | Cinq repères du visage, chacun `[x, y]` en pixels. |
| `confidence` | `number` | Confiance de la détection, de 0 à 1. |

**Exemple**

```json
{
  "bbox": {
    "x": 512.4,
    "y": 188.9,
    "width": 164.2,
    "height": 211.7
  },
  "confidence": 0.9731
}
```

<a name="type-facebox"></a>

### FaceBox

*Objet*. Rectangle en pixels, depuis le coin haut gauche de l'image.

| Membre | Type | Description |
| --- | --- | --- |
| `x` | `number` | Bord gauche. |
| `y` | `number` | Bord haut. |
| `width` | `number` | Largeur. |
| `height` | `number` | Hauteur. |

**Exemple**

```json
{
  "x": 512.4,
  "y": 188.9,
  "width": 164.2,
  "height": 211.7
}
```

<a name="type-facelandmarks"></a>

### FaceLandmarks

*Objet*. Repères d'un visage, du point de vue de la personne photographiée.

| Membre | Type | Description |
| --- | --- | --- |
| `right_eye` | `[number, number]` | Œil droit. |
| `left_eye` | `[number, number]` | Œil gauche. |
| `nose_tip` | `[number, number]` | Bout du nez. |
| `right_mouth` | `[number, number]` | Coin droit de la bouche. |
| `left_mouth` | `[number, number]` | Coin gauche de la bouche. |

**Exemple**

```json
{
  "right_eye": [
    561.3,
    268.1
  ],
  "left_eye": [
    628.8,
    266.4
  ],
  "nose_tip": [
    596.2,
    307.5
  ],
  "right_mouth": [
    567.9,
    345.2
  ],
  "left_mouth": [
    622.4,
    343.8
  ]
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/faceBlurApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "mode": {
      "title": "Mode",
      "default": "manual",
      "type": "string",
      "enum": [
        "manual",
        "auto"
      ]
    },
    "radius": {
      "title": "Intensity",
      "default": 18,
      "type": "number",
      "minimum": 1,
      "maximum": 60
    },
    "zones": {
      "title": "Zones",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "x": {
            "title": "X",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y": {
            "title": "Y",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "w": {
            "title": "W",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "h": {
            "title": "H",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "shape": {
            "title": "Shape",
            "default": "square",
            "type": "string",
            "enum": [
              "square",
              "circle"
            ]
          }
        },
        "required": [
          "x",
          "y",
          "w",
          "h"
        ]
      }
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
