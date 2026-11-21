# Bruit : référence API

Génère un bruit procédural (Perlin, simplex, aléatoire, Voronoï, pastilles, cubiste, éclats) avec post-traitement et fusion

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/noise` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `blend` (Une image ou plusieurs) | non | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image à fusionner**<br />Image facultative fusionnée avec le bruit ; reliée, elle en fixe aussi la taille. |

## Réglages

### Type de bruit

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `type` | `string` | `"perlin"` | `perlin` Perlin<br />`simplex` Simplex<br />`random` Aléatoire<br />`voronoi` Voronoï<br />`spots` Pastilles<br />`cubist` Cubiste<br />`shard` Éclats | **Type** |

### Perlin

> Ces réglages ne comptent que quand `type` = `perlin` (Perlin).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `ridged` | `boolean` | `false` |  | **Crêtes (ridged)**<br />Replie le bruit sur lui-même pour transformer les vallées en crêtes nettes : donne un relief de montagnes ou de nervures. |

### Aléatoire

> Ces réglages ne comptent que quand `type` = `random` (Aléatoire).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `randomGamma` | `number` | `100` | min 10 % · max 500 % · pas de 1 | **Gamma**<br />Courbe la répartition des valeurs. Sous 100 %, le bruit s'éclaircit ; au-dessus, il s'assombrit et les points clairs se raréfient. |

### Voronoï

> Ces réglages ne comptent que quand `type` = `voronoi` (Voronoï).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `voronoiMode` | `string` | `"f1"` | `f1` Distance<br />`ridge` Crêtes<br />`f2` Craquelures<br />`cells` Aplats | **Mode**<br />Ce qui est mesuré dans chaque cellule : distance au centre, arêtes entre cellules, craquelures, ou aplat uniforme par cellule. |
| `voronoiJitter` | `number` | `100` | min 0 % · max 100 % | **Irrégularité**<br />Décalage aléatoire du centre de chaque cellule. À 0 % la grille est régulière, à 100 % les cellules sont pleinement irrégulières. |
| `voronoiInvert` | `boolean` | `false` |  | **Inverser**<br />Échange le clair et le sombre du motif cellulaire. |

### Pastilles

> Ces réglages ne comptent que quand `type` = `spots` (Pastilles).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `spotsRadius` | `number` | `40` | min 1 % · max 100 % | **Rayon**<br />Taille des pastilles, en proportion de leur cellule. Au-delà de 100 % elles se chevauchent et fusionnent. |
| `spotsSoftness` | `number` | `60` | min 0 % · max 100 % | **Douceur**<br />Étendue du dégradé sur le bord. À 0 % le bord est net, à 100 % la pastille est un halo sans centre plein. |
| `spotsDensity` | `number` | `70` | min 0 % · max 100 % | **Densité**<br />Proportion de cellules qui reçoivent une pastille. Plus la valeur est basse, plus le semis est clairsemé. |
| `spotsSizeJitter` | `number` | `40` | min 0 % · max 100 % | **Variation de taille**<br />Variation aléatoire du rayon d'une pastille à l'autre. |
| `spotsInvert` | `boolean` | `false` |  | **Inverser**<br />Pastilles sombres sur fond clair au lieu de l'inverse. |

### Cubiste

> Ces réglages ne comptent que quand `type` = `cubist` (Cubiste).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `cubistJitter` | `number` | `90` | min 0 % · max 100 % | **Irrégularité**<br />Décalage aléatoire du centre des facettes. Plus il est haut, moins les facettes se ressemblent. |
| `cubistShade` | `number` | `60` | min 0 % · max 100 % | **Inclinaison des facettes**<br />Force de l'inclinaison du plan de chaque facette : à 0 % chaque facette est un aplat, plus haut elle se dégrade comme éclairée de biais. |
| `cubistEdge` | `number` | `30` | min 0 % · max 100 % | **Arêtes**<br />Assombrit les arêtes entre facettes pour marquer les plis. |

### Éclats

> Ces réglages ne comptent que quand `type` = `shard` (Éclats).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `shardJitter` | `number` | `100` | min 0 % · max 100 % | **Irrégularité**<br />Irrégularité de la découpe des éclats. |
| `shardSharpness` | `number` | `50` | min 1 % · max 100 % | **Netteté**<br />Finesse des arêtes. Bas, les éclats sont larges et diffus ; haut, ce sont des fils fins. |
| `shardStretch` | `number` | `200` | min 20 % · max 800 % · pas de 5 | **Étirement**<br />Allonge les éclats dans une direction. À 100 % ils sont compacts, au-delà ils s'étirent en échardes. |
| `shardAngle` | `number` | `25` | min -180 ° · max 180 ° · pas de 1 | **Angle**<br />Direction dans laquelle les éclats sont étirés. |
| `shardInvert` | `boolean` | `false` |  | **Inverser**<br />Échange le clair et le sombre des éclats. |

### Bruit

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `octaves` | `number` | `4` | min 1 · max 8 · pas de 1 | **Octaves**<br />Nombre de couches de bruit superposées, chacune deux fois plus fine que la précédente. Plus il y en a, plus le détail est riche, et plus le calcul est long. |
| `octaveRamp` | [`CurvePoint[]`](#type-curvepoint)<br />*Courbe* | `[{"x":0,"y":1},{"x":1,"y":0}]` |  | **Rampe des octaves**<br />Poids de chaque couche, de la plus grossière (gauche) à la plus fine (droite). Une descente marquée donne un bruit doux, une rampe plate un bruit granuleux.<br />Structure de CurvePoint[] et exemple : [`CurvePoint`](#type-curvepoint) |
| `intensity` | `number` | `100` | min 0 % · max 400 % · pas de 1 | **Intensité**<br />Contraste autour du gris moyen. À 0 % l'image devient uniforme, au-delà de 100 % les extrêmes sont écrasés. |
| `seed` | `number` | `1` | min 0 | **Graine**<br />Change le tirage aléatoire. À réglages identiques, une même graine redonne toujours exactement le même bruit. Entre deux entiers, le bruit glisse d'un tirage à l'autre : animée dans la timeline, la graine fait bouger les cellules au lieu de les faire sauter. |

### Cadrage

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `posX` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **X**<br />Déplace le bruit horizontalement sans changer sa forme, en % de la largeur : sert à recadrer sur une zone qui plaît. |
| `posY` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **Y**<br />Déplace le bruit verticalement sans changer sa forme, en % de la hauteur. |
| `rotation` | `number` | `0` | min -180 ° · max 180 ° · pas de 1 | **Rotation**<br />Fait pivoter le motif dans l'image. |
| `scale` | `number` | `64` | min 1 px · max 1024 px · pas de 1 | **Échelle**<br />Taille du bruit en pixels. |
| `tileOverlap` | `number` | `0` | min 0 % · max 50 % | **Recouvrement (tuilage)**<br />Fond le bord droit avec la gauche (et le bas avec le haut) sur cette largeur, pour que l'image se répète sans couture visible. |

### Dimensions

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | min 1 px · max 8000 px · pas de 1 | **Largeur**<br />Largeur de l'image générée. Ignorée si une image est reliée à l'entrée de fusion. |
| `height` | `number` | `512` | min 1 px · max 8000 px · pas de 1 | **Hauteur**<br />Hauteur de l'image générée. Ignorée si une image est reliée à l'entrée de fusion. |

### Post-traitement

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `autoLevel` | `boolean` | `false` |  | **Niveaux automatiques**<br />Étire le bruit pour qu'il occupe toute la plage du noir au blanc. Utile quand le résultat paraît terne. |
| `remap` | [`CurvePoint[]`](#type-curvepoint)<br />*Courbe* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Remap**<br />Retrace la correspondance entre valeur produite (horizontale) et valeur affichée (verticale). Sert à isoler une plage ou à inverser le bruit.<br />Structure de CurvePoint[] et exemple : [`CurvePoint`](#type-curvepoint) |
| `quantize` | `boolean` | `false` |  | **Quantifier**<br />Réduit le dégradé continu à un petit nombre de tons, pour un rendu en aplats. |

### Quantification

> Ces réglages ne comptent que quand `quantize` = `true`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `quantizeLevels` | `number` | `4` | min 2 · max 64 · pas de 1 | **Niveaux**<br />Nombre de tons conservés, du noir au blanc. |
| `quantizeBias` | `number` | `0` | min -100 % · max 100 % | **Biais**<br />Décale les seuils entre tons : négatif assombrit l'ensemble, positif l'éclaircit. |

### Fusion

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Mode de fusion* | `"multiply"` | `normal` Normal : Le calque recouvre ce qui est dessous.<br />`multiply` Produit : Fonce : le blanc disparaît.<br />`screen` Écran : Éclaircit : le noir disparaît.<br />`overlay` Incrustation : Renforce le contraste du dessous.<br />`darken` Obscurcir : Garde le plus sombre des deux.<br />`lighten` Éclaircir : Garde le plus clair des deux.<br />`color-dodge` Densité - : Éclaircit jusqu'à l'éclat.<br />`color-burn` Densité + : Fonce en saturant les couleurs.<br />`hard-light` Lumière crue : Contraste franc, comme un projecteur.<br />`soft-light` Lumière douce : Contraste doux, comme une lumière diffuse.<br />`difference` Différence : Inverse là où le calque est clair.<br />`exclusion` Exclusion : Comme Différence, en plus doux.<br />`luminosity` Luminosité : Prend seulement la clarté du calque. | **Mode de fusion**<br />Façon dont le bruit se combine à l'image reliée à l'entrée. Sans entrée connectée, ce réglage ne s'applique pas. |
| `blendOpacity` | `number` | `50` | min 0 % · max 100 % · pas de 1 | **Opacité**<br />Dosage du bruit dans la fusion. À 0 % l'image source ressort intacte. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/noise \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F blend=@blend.png \
  -F 'params={"type":"perlin","ridged":false,"octaves":4}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('blend', await openAsBlob('blend.png'), 'blend.png')
form.append('params', JSON.stringify({"type":"perlin","ridged":false,"octaves":4}))

const res = await fetch('https://api.pixlub.com/v1/modules/noise', {
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
    "https://api.pixlub.com/v1/modules/noise",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("blend", open("blend.png", "rb"))],
    data={"params": json.dumps({"type": "perlin", "ridged": False, "octaves": 4})},
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
result = client.tools.run("noise", inputs={"blend": "blend.png"}, params={"type": "perlin", "ridged": False, "octaves": 4})
result.save(f"noise{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "noise", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "blend": pixlub.FromPath("blend.png"),
    },
    Params: map[string]any{"type": "perlin", "ridged": false, "octaves": 4},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("noise"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

### 1 fichier

> **1 fichier** : Une seule image dans `blend`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Bruit généré, fondu sur l'image reçue.<br />Une seule image envoyée : le fichier garde la clé `out`. |

### Plusieurs fichiers

> **Plusieurs fichiers** : Plusieurs images dans `blend`, jusqu'à 64 : leur nombre se déduit des fichiers envoyés, vous ne l'envoyez pas.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Image(s)**<br />Bruit généré, fondu sur l'image reçue.<br />Plusieurs images envoyées dans `blend` : un fichier par image, sous les clés `out#0`, `out#1`…, dans l'ordre d'envoi. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "noise",
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

**Exemple de CurvePoint[]**

```json
[
  {
    "x": 0,
    "y": 0
  },
  {
    "x": 0.5,
    "y": 0.65
  },
  {
    "x": 1,
    "y": 1
  }
]
```

<a name="type-curvepoint"></a>

### CurvePoint

*Objet*. Point d'une courbe de correspondance.

| Membre | Type | Description |
| --- | --- | --- |
| `x` | `number` | Valeur d'entrée, de 0 à 1. |
| `y` | `number` | Valeur de sortie, de 0 à 1. |
| `i` | `"smooth" \| "bezier" \| "linear" \| "constant"` | *facultatif* · Raccord vers le point suivant. `smooth` par défaut. |
| `a` | `number` | *facultatif* · Angle de la tangente en degrés, de -85 à 85 (raccord `bezier`). |

**Exemple**

```json
{
  "x": 0.5,
  "y": 0.6
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/noise/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "ridged": {
      "title": "Ridged",
      "default": false,
      "type": "boolean"
    },
    "randomGamma": {
      "title": "Gamma",
      "default": 100,
      "type": "number",
      "minimum": 10,
      "maximum": 500,
      "multipleOf": 1
    },
    "voronoiMode": {
      "title": "Mode",
      "default": "f1",
      "type": "string",
      "enum": [
        "f1",
        "ridge",
        "f2",
        "cells"
      ]
    },
    "voronoiJitter": {
      "title": "Irregularity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "voronoiInvert": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "spotsRadius": {
      "title": "Radius",
      "default": 40,
      "type": "number",
      "minimum": 1,
      "maximum": 100
    },
    "spotsSoftness": {
      "title": "Softness",
      "default": 60,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "spotsDensity": {
      "title": "Density",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "spotsSizeJitter": {
      "title": "Size variation",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "spotsInvert": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "cubistJitter": {
      "title": "Irregularity",
      "default": 90,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "cubistShade": {
      "title": "Facet slope",
      "default": 60,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "cubistEdge": {
      "title": "Edges",
      "default": 30,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "shardJitter": {
      "title": "Irregularity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "shardSharpness": {
      "title": "Sharpness",
      "default": 50,
      "type": "number",
      "minimum": 1,
      "maximum": 100
    },
    "shardStretch": {
      "title": "Stretch",
      "default": 200,
      "type": "number",
      "minimum": 20,
      "maximum": 800,
      "multipleOf": 5
    },
    "shardAngle": {
      "title": "Angle",
      "default": 25,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "shardInvert": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "octaves": {
      "title": "Octaves",
      "default": 4,
      "type": "number",
      "minimum": 1,
      "maximum": 8,
      "multipleOf": 1
    },
    "octaveRamp": {
      "title": "Octave ramp",
      "default": [
        {
          "x": 0,
          "y": 1
        },
        {
          "x": 1,
          "y": 0
        }
      ],
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
          "i": {
            "type": "string",
            "enum": [
              "smooth",
              "bezier",
              "linear",
              "constant"
            ]
          },
          "a": {
            "type": "number",
            "minimum": -85,
            "maximum": 85
          }
        }
      },
      "minItems": 2
    },
    "intensity": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 400,
      "multipleOf": 1
    },
    "seed": {
      "title": "Seed",
      "default": 1,
      "type": "number",
      "minimum": 0
    },
    "posX": {
      "title": "X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "posY": {
      "title": "Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "rotation": {
      "title": "Rotation",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "scale": {
      "title": "Scale",
      "default": 64,
      "type": "number",
      "minimum": 1,
      "maximum": 1024,
      "multipleOf": 1
    },
    "tileOverlap": {
      "title": "Tiling overlap",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 50
    },
    "width": {
      "title": "Width",
      "default": 512,
      "type": "number",
      "minimum": 1,
      "maximum": 8000,
      "multipleOf": 1
    },
    "height": {
      "title": "Height",
      "default": 512,
      "type": "number",
      "minimum": 1,
      "maximum": 8000,
      "multipleOf": 1
    },
    "autoLevel": {
      "title": "Auto level",
      "default": false,
      "type": "boolean"
    },
    "remap": {
      "title": "Remap",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
        }
      ],
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
          "i": {
            "type": "string",
            "enum": [
              "smooth",
              "bezier",
              "linear",
              "constant"
            ]
          },
          "a": {
            "type": "number",
            "minimum": -85,
            "maximum": 85
          }
        }
      },
      "minItems": 2
    },
    "quantize": {
      "title": "Quantize",
      "default": false,
      "type": "boolean"
    },
    "quantizeLevels": {
      "title": "Levels",
      "default": 4,
      "type": "number",
      "minimum": 2,
      "maximum": 64,
      "multipleOf": 1
    },
    "quantizeBias": {
      "title": "Bias",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100
    },
    "blendMode": {
      "title": "Blend mode",
      "default": "multiply",
      "type": "string",
      "enum": [
        "normal",
        "multiply",
        "screen",
        "overlay",
        "darken",
        "lighten",
        "color-dodge",
        "color-burn",
        "hard-light",
        "soft-light",
        "difference",
        "exclusion",
        "luminosity"
      ]
    },
    "blendOpacity": {
      "title": "Opacity",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "type": {
      "type": "string",
      "default": "perlin"
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
