# Rogner : référence API

Découpe une zone de l'image

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/crop` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Une image ou plusieurs) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image dans laquelle la zone est découpée. |

## Réglages

### Position

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `x` | `number` | `0` | min 0 | **X**<br />Coordonnée X du coin supérieur gauche de la zone à découper |
| `y` | `number` | `0` | min 0 | **Y**<br />Coordonnée Y du coin supérieur gauche de la zone à découper |

### Dimensions

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `width` | [`Dimension`](#type-dimension)<br />*Dimension* | `{"value":400,"unit":"px"}` | `px` Pixels : De 1 px à la largeur de l'image.<br />`%` Pourcentage : De 1 % à 100 %. En pourcentage de la largeur de l'image. | **Largeur**<br />Largeur de la zone à découper<br />*Dimension* : Objet `Dimension` : `{ "value": 50, "unit": "%" }`. Les bornes de `value` dépendent de `unit` : voir les valeurs permises. Sans `unit`, ou pour un nombre seul, `px`.<br />Structure de Dimension et exemple : [`Dimension`](#type-dimension) |
| `height` | [`Dimension`](#type-dimension)<br />*Dimension* | `{"value":300,"unit":"px"}` | `px` Pixels : De 1 px à la hauteur de l'image.<br />`%` Pourcentage : De 1 % à 100 %. En pourcentage de la hauteur de l'image. | **Hauteur**<br />Hauteur de la zone à découper<br />*Dimension* : Objet `Dimension` : `{ "value": 50, "unit": "%" }`. Les bornes de `value` dépendent de `unit` : voir les valeurs permises. Sans `unit`, ou pour un nombre seul, `px`.<br />Structure de Dimension et exemple : [`Dimension`](#type-dimension) |

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
curl -X POST https://api.pixlub.com/v1/modules/crop \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"x":0,"y":0,"width":{"value":400,"unit":"px"}}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"x":0,"y":0,"width":{"value":400,"unit":"px"}}))

const res = await fetch('https://api.pixlub.com/v1/modules/crop', {
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
    "https://api.pixlub.com/v1/modules/crop",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"x": 0, "y": 0, "width": {"value": 400, "unit": "px"}})},
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
result = client.tools.run("crop", image="photo.png", params={"x": 0, "y": 0, "width": {"value": 400, "unit": "px"}})
result.save(f"crop{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "crop", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"x": 0, "y": 0, "width": map[string]any{"value": 400, "unit": "px"}},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("crop"+result.Extension(), false)
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
  "module": "crop",
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

<a name="type-dimension"></a>

### Dimension

*Objet*. Longueur et son unité.

| Membre | Type | Description |
| --- | --- | --- |
| `value` | `number` | Longueur, dans l'unité `unit`. |
| `unit` | `"px" \| "%"` | *facultatif* · `px` : en pixels ; `%` : en pourcentage de la largeur (ou de la hauteur) de l'image. Chaque réglage dit les unités qu'il admet ; la première par défaut. |

**Exemple**

```json
{
  "value": 50,
  "unit": "%"
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/crop/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "x": {
      "title": "X",
      "default": 0,
      "type": "number",
      "minimum": 0
    },
    "y": {
      "title": "Y",
      "default": 0,
      "type": "number",
      "minimum": 0
    },
    "width": {
      "title": "Width",
      "default": {
        "value": 400,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 1
            },
            "unit": {
              "const": "px"
            }
          }
        },
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value",
            "unit"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 1,
              "maximum": 100
            },
            "unit": {
              "const": "%"
            }
          }
        }
      ]
    },
    "height": {
      "title": "Height",
      "default": {
        "value": 300,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 1
            },
            "unit": {
              "const": "px"
            }
          }
        },
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value",
            "unit"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 1,
              "maximum": 100
            },
            "unit": {
              "const": "%"
            }
          }
        }
      ]
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
