# Courber sur chemin : référence API

Déforme une image le long d'un chemin (ruban / trail courbé)

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/warpPath` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image courbée le long du chemin : sa largeur suit le tracé, sa hauteur devient l'épaisseur du ruban. |

## Réglages

### Tracé

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `path` | [`Path`](#type-path)<br />*Tracé* | [JSON](#default-path) |  | **Tracé**<br />Dessinez le tracé, ou branchez un module Tracé sur l'entrée du nœud : la connexion prend alors le dessus. Le résultat a la taille du cadre du tracé.<br />*Tracé* : Objet `Path` : ses ancres `points` sont placées de 0 à 1 dans le cadre, détaillées ci-dessous.<br />Structure de Path et exemple : [`Path`](#type-path), [`PathPoint`](#type-pathpoint) |

<a name="default-path"></a>

**Valeur par défaut de `path`**

```json
{
  "points": [
    {
      "x": 0.12,
      "y": 0.68
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.88,
      "y": 0.66
    }
  ],
  "closed": false,
  "smooth": true,
  "rounding": 0.5,
  "curve": "arc",
  "w": 512,
  "h": 512
}
```

### Ruban

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `thickness` | `number` | `100` | min 10 % · max 200 % · pas de 1 | **Épaisseur**<br />À 100 %, l'image garde ses proportions le long du tracé, sans dépasser ce que le virage le plus serré permet. Plus bas le ruban s'affine ; plus haut il s'épaissit, au risque de se resserrer à l'intérieur des virages. |
| `side` | `string` | `"center"` | `left` À gauche : Le ruban longe le tracé sur sa gauche, dans le sens du dessin.<br />`center` Centré : Le tracé passe au milieu du ruban.<br />`right` À droite : Le ruban longe le tracé sur sa droite. | **Position**<br />Place du ruban par rapport au tracé. Le haut de l'image est toujours du côté gauche. |
| `fill` | `string` | `"stretch"` | `stretch` Étirer : L'image s'étire une fois sur toute la longueur du tracé.<br />`repeat` Répéter : L'image garde ses proportions et se répète le long du tracé. | **Remplissage**<br />Façon dont l'image couvre la longueur du tracé. |

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
curl -X POST https://api.pixlub.com/v1/modules/warpPath \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"thickness":100,"side":"center","fill":"stretch"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"thickness":100,"side":"center","fill":"stretch"}))

const res = await fetch('https://api.pixlub.com/v1/modules/warpPath', {
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
    "https://api.pixlub.com/v1/modules/warpPath",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"thickness": 100, "side": "center", "fill": "stretch"})},
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
result = client.tools.run("warpPath", image="photo.png", params={"thickness": 100, "side": "center", "fill": "stretch"})
result.save(f"warpPath{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "warpPath", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"thickness": 100, "side": "center", "fill": "stretch"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("warpPath"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produite par le module. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "warpPath",
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

<a name="type-path"></a>

### Path

*Objet*. Tracé de courbes de Bézier passant par des ancres, dans un cadre de référence.

| Membre | Type | Description |
| --- | --- | --- |
| `points` | `PathPoint[]` | Ancres du tracé, dans l'ordre ; au moins deux. |
| `closed` | `boolean` | *facultatif* · Relie la dernière ancre à la première. `false` par défaut. |
| `smooth` | `boolean` | *facultatif* · Arrondit le tracé entre les ancres `auto` ; `false` les relie en lignes droites. `true` par défaut. |
| `rounding` | `number` | *facultatif* · Force de l'arrondi, de 0 à 1. `0.5` par défaut. |
| `curve` | `"arc" \| "spline"` | *facultatif* · Courbure des ancres `auto` : `arc` en arcs de cercle (des ancres posées en rond donnent un cercle exact), `spline` en courbe de Catmull-Rom. `spline` par défaut. |
| `w` | `number` | *facultatif* · Largeur du cadre de référence, en pixels. Avec `h`, le tracé garde ses proportions et se centre dans l'image ; sans eux, il couvre l'image entière. |
| `h` | `number` | *facultatif* · Hauteur du cadre de référence, en pixels. |

**Exemple**

```json
{
  "points": [
    {
      "x": 0.1,
      "y": 0.7
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.9,
      "y": 0.7
    }
  ],
  "closed": false,
  "smooth": true
}
```

<a name="type-pathpoint"></a>

### PathPoint

*Objet*. Ancre d'un tracé.

| Membre | Type | Description |
| --- | --- | --- |
| `x` | `number` | Position horizontale, de 0 (gauche) à 1 (droite) du cadre. |
| `y` | `number` | Position verticale, de 0 (haut) à 1 (bas) du cadre. |
| `k` | `"auto" \| "corner" \| "free"` | *facultatif* · Type d'ancre : `auto` arrondie, `corner` angle vif, `free` poignées `i` et `o` données. `auto` par défaut. |
| `i` | `{ x, y }` | *facultatif* · Poignée d'entrée (ancre `free`), relative à l'ancre, en fraction du cadre. |
| `o` | `{ x, y }` | *facultatif* · Poignée de sortie (ancre `free`), relative à l'ancre. |
| `w` | `number` | *facultatif* · Épaisseur du trait à cette ancre, en % de l'épaisseur réglée. `100` par défaut. |

**Exemple**

```json
{
  "x": 0.5,
  "y": 0.3
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/warpPath/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "path": {
      "title": "Path",
      "default": {
        "points": [
          {
            "x": 0.12,
            "y": 0.68
          },
          {
            "x": 0.5,
            "y": 0.3
          },
          {
            "x": 0.88,
            "y": 0.66
          }
        ],
        "closed": false,
        "smooth": true,
        "rounding": 0.5,
        "curve": "arc",
        "w": 512,
        "h": 512
      },
      "type": "object",
      "required": [
        "points"
      ],
      "properties": {
        "points": {
          "type": "array",
          "items": {
            "type": "object",
            "required": [
              "x",
              "y"
            ],
            "properties": {
              "x": {
                "type": "number",
                "minimum": 0,
                "maximum": 1
              },
              "y": {
                "type": "number",
                "minimum": 0,
                "maximum": 1
              },
              "k": {
                "type": "string",
                "enum": [
                  "auto",
                  "corner",
                  "free"
                ]
              },
              "i": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "o": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "w": {
                "type": "number",
                "minimum": 0
              }
            }
          },
          "minItems": 2
        },
        "closed": {
          "type": "boolean"
        },
        "smooth": {
          "type": "boolean"
        },
        "rounding": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        },
        "curve": {
          "type": "string",
          "enum": [
            "arc",
            "spline"
          ]
        },
        "w": {
          "type": "number",
          "minimum": 1
        },
        "h": {
          "type": "number",
          "minimum": 1
        }
      }
    },
    "thickness": {
      "title": "Thickness",
      "default": 100,
      "type": "number",
      "minimum": 10,
      "maximum": 200,
      "multipleOf": 1
    },
    "side": {
      "title": "Position",
      "default": "center",
      "type": "string",
      "enum": [
        "left",
        "center",
        "right"
      ]
    },
    "fill": {
      "title": "Fill",
      "default": "stretch",
      "type": "string",
      "enum": [
        "stretch",
        "repeat"
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
