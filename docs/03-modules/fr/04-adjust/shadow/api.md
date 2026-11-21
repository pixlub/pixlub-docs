# Ombre : référence API

Projette une ombre (extérieure ou intérieure) à partir de l'alpha de l'image

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/shadow` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Une image ou plusieurs) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image dont l'alpha projette l'ombre. |

## Réglages

### Général

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `side` | `string` | `"outside"` | `outside` Extérieur : L'ombre est projetée à l'extérieur du contenu.<br />`inside` Intérieur : L'ombre est projetée à l'intérieur du contenu. | **Côté**<br />Côté de l'ombre projetée par l'alpha de l'image. |

### Couleur

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Couleur ou dégradé* | `"#000000"` |  | **Couleur**<br />Couleur de l'ombre projetée.<br />*Couleur ou dégradé* : Une couleur CSS (`"#ff8800"`) pour un aplat, ou un objet `ColorGradient` pour un dégradé.<br />Structure de Color \| ColorGradient et exemple : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |

### Ombre

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `strength` | `number` | `60` | min 0 % · max 100 % · pas de 1 | **Intensité**<br />Intensité de l'ombre projetée. |
| `grow` | `number` | `0` | min 0 px · max 200 px · pas de 1 | **Dilatation**<br />Dilatation de l'ombre projetée. |
| `blur` | `number` | `8` | min 0 px · max 200 px · pas de 1 | **Flou**<br />Flou de l'ombre projetée. |

### Décalage

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `offsetX` | `number` | `1.5` | min -50 % · max 50 % · pas de 0.1 | **X**<br />Décalage horizontal de l'ombre, en % de la largeur de l'image. Positif vers la droite. |
| `offsetY` | `number` | `1.5` | min -50 % · max 50 % · pas de 0.1 | **Y**<br />Décalage vertical de l'ombre, en % de la hauteur de l'image. Positif vers le bas. |

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
curl -X POST https://api.pixlub.com/v1/modules/shadow \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"side":"outside","color":"#000000","strength":60}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"side":"outside","color":"#000000","strength":60}))

const res = await fetch('https://api.pixlub.com/v1/modules/shadow', {
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
    "https://api.pixlub.com/v1/modules/shadow",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"side": "outside", "color": "#000000", "strength": 60})},
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
result = client.tools.run("shadow", image="photo.png", params={"side": "outside", "color": "#000000", "strength": 60})
result.save(f"shadow{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "shadow", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"side": "outside", "color": "#000000", "strength": 60},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("shadow"+result.Extension(), false)
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
  "module": "shadow",
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

`GET /v1/modules/shadow/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "side": {
      "title": "Side",
      "default": "outside",
      "type": "string",
      "enum": [
        "outside",
        "inside"
      ]
    },
    "color": {
      "title": "Color",
      "default": "#000000",
      "anyOf": [
        {
          "type": "string",
          "minLength": 1
        },
        {
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
            },
            "type": {
              "type": "string",
              "enum": [
                "linear",
                "radial"
              ]
            },
            "angle": {
              "type": "number"
            }
          }
        }
      ]
    },
    "strength": {
      "title": "Intensity",
      "default": 60,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "grow": {
      "title": "Dilation",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    },
    "blur": {
      "title": "Blur",
      "default": 8,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetX": {
      "title": "X",
      "default": 1.5,
      "type": "number",
      "minimum": -50,
      "maximum": 50,
      "multipleOf": 0.1
    },
    "offsetY": {
      "title": "Y",
      "default": 1.5,
      "type": "number",
      "minimum": -50,
      "maximum": 50,
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
