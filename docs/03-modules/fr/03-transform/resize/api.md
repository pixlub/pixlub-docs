# Redimensionner : référence API

Modifie les dimensions de l'image

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/resize` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Une image ou plusieurs) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image à redimensionner. |

## Réglages

### Dimensions

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `size` | [`Size`](#type-size)<br />*Taille* | `{"width":0,"height":0,"unit":"px"}` | `px` Pixels : De 0 px à 8000 px.<br />`%` Pourcentage : De 0 % à 800 %. En pourcentage de la largeur et de la hauteur de l'image.<br />`centimeters` Centimètres : De 0 cm à 500 cm. Converti en pixels par `dpi`.<br />`inches` Pouces : De 0 in à 200 in. Converti en pixels par `dpi`. | **Taille**<br />Largeur et hauteur visées, dans une même unité. Un côté à 0 (« Auto ») garde celui de l'image, ou suit les proportions quand elles sont verrouillées.<br />*Taille* : Objet `Size` : `{ "width": 1280, "height": 720, "unit": "px" }`. Les bornes de `width` et `height` dépendent de `unit` : voir les valeurs permises. Sans `unit`, `px`.<br />Structure de Size et exemple : [`Size`](#type-size) |
| `lockAspect` | `boolean`<br />*Proportions* | `true` |  | **Garder les proportions**<br />*Proportions* : Quand une seule des dimensions `size.width`, `size.height` est donnée, l'autre suit les proportions de l'image ; sans verrou, elle garde celle de l'image. |
| `dpi` | `number`<br />*Résolution* | `300` | min 1 dpi · max 2400 dpi | **Résolution**<br />*Résolution* : Points par pouce qui convertissent les `centimeters` et `inches` de `size` en pixels ; sans effet en `px` et en `%`. |

### Algorithme

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `algorithm` | `string` | `"bilinear"` | `bilinear` Bilinéaire<br />`nearest` Plus proche voisin<br />`bicubic` Bicubique | **Algorithme** |

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
curl -X POST https://api.pixlub.com/v1/modules/resize \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"size":{"width":50,"unit":"%"},"lockAspect":true,"dpi":300}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"size":{"width":50,"unit":"%"},"lockAspect":true,"dpi":300}))

const res = await fetch('https://api.pixlub.com/v1/modules/resize', {
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
    "https://api.pixlub.com/v1/modules/resize",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"size": {"width": 50, "unit": "%"}, "lockAspect": True, "dpi": 300})},
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
result = client.tools.run("resize", image="photo.png", params={"size": {"width": 50, "unit": "%"}, "lockAspect": True, "dpi": 300})
result.save(f"resize{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "resize", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"size": map[string]any{"width": 50, "unit": "%"}, "lockAspect": true, "dpi": 300},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("resize"+result.Extension(), false)
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
  "module": "resize",
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

**Exemple de Size**

```json
{
  "width": 50,
  "unit": "%"
}
```

<a name="type-size"></a>

### Size

*Objet*. Largeur et hauteur visées, dans une même unité.

| Membre | Type | Description |
| --- | --- | --- |
| `width` | `number` | *facultatif* · Largeur, dans l'unité `unit`. `0` ou absente : celle de l'image, ou celle qui garde les proportions quand elles sont verrouillées et que seule `height` est donnée. |
| `height` | `number` | *facultatif* · Hauteur, dans l'unité `unit`. `0` ou absente : celle de l'image, ou celle qui garde les proportions quand elles sont verrouillées et que seule `width` est donnée. |
| `unit` | `"px" \| "%" \| "centimeters" \| "inches"` | *facultatif* · `px` : en pixels ; `%` : en pourcentage de la largeur (pour `width`) et de la hauteur (pour `height`) de l'image ; `centimeters` et `inches` : longueurs d'impression, converties en pixels par la résolution. Chaque réglage dit les unités qu'il admet ; la première par défaut. |

**Exemple**

```json
{
  "width": 1280,
  "height": 720,
  "unit": "px"
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/resize/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "size": {
      "title": "Size",
      "default": {
        "width": 0,
        "height": 0,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 8000
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 8000
            },
            "unit": {
              "const": "px"
            }
          }
        },
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 800
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 800
            },
            "unit": {
              "const": "%"
            }
          },
          "required": [
            "unit"
          ]
        },
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 500
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 500
            },
            "unit": {
              "const": "centimeters"
            }
          },
          "required": [
            "unit"
          ]
        },
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 200
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 200
            },
            "unit": {
              "const": "inches"
            }
          },
          "required": [
            "unit"
          ]
        }
      ]
    },
    "lockAspect": {
      "type": "boolean",
      "default": true
    },
    "dpi": {
      "type": "number",
      "minimum": 1,
      "maximum": 2400,
      "default": 300
    },
    "algorithm": {
      "title": "Algorithm",
      "default": "bilinear",
      "type": "string",
      "enum": [
        "bilinear",
        "nearest",
        "bicubic"
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
