# Solide : référence API

Génère une forme remplie d'une couleur unie ou d'un dégradé

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/solid` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `background` (Image seule) | non | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Arrière-plan**<br />Image facultative placée sous la forme ; reliée, elle fixe aussi la taille du résultat. |
| `fill` (Image seule) | non | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Média**<br />Image facultative vue à travers la forme, à la place de sa couleur ; le contour reste par-dessus. |

## Réglages

### Forme

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"rectangle"` | `rectangle` Rectangle<br />`circle` Cercle<br />`ellipse` Ellipse<br />`ring` Anneau<br />`triangle` Triangle<br />`diamond` Losange<br />`polygon` Polygone<br />`star` Étoile | **Forme**<br />Forme à générer. |

### Couleur

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Couleur ou dégradé* | `"#4c9caf"` |  | **Couleur**<br />Couleur unie ou dégradé de la forme.<br />*Couleur ou dégradé* : Une couleur CSS (`"#ff8800"`) pour un aplat, ou un objet `ColorGradient` pour un dégradé.<br />Structure de Color \| ColorGradient et exemple : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `innerFill` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Remplissage intérieur**<br />Contour atténué de la forme depuis le centre. |

### Arrière-plan

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `backgroundOpacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité**<br />Opacité de l'image connectée à l'entrée Arrière-plan, peinte sous la forme. |

### Média dans la forme

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `fillFit` | `string` | `"cover"` | `cover` Remplir : Le média couvre toute la forme, quitte à être rogné.<br />`contain` Entier : Le média tient entier dans la forme ; sa couleur reste autour. | **Ajustement**<br />Comment le média relié à l'entrée Média se cale dans la forme. |
| `fillScale` | `number` | `100` | min 10 % · max 1000 % · pas de 0.1 | **Échelle**<br />Échelle du média une fois ajusté ; 100 % = ajusté. |
| `fillX` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **Décalage X**<br />Décalage horizontal du média, en part de la demi-largeur de la forme. |
| `fillY` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **Décalage Y**<br />Décalage vertical du média, en part de la demi-hauteur de la forme. |

### Contour

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `strokeWidth` | `number` | `0` | min 0 px · max 200 px · pas de 1 | **Épaisseur**<br />Épaisseur du contour de la forme. |
| `strokeColor` | `Color`<br />*Couleur unie* | `"#1c2535"` |  | **Couleur**<br />Couleur du contour de la forme.<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |

### Rotation

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `rotation` | `number` | `0` | min -180 ° · max 180 ° | **Angle**<br />Angle de rotation de la forme. |

### Dimensions

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | min 1 px · max 8000 px · pas de 1 | **Largeur**<br />Largeur de la zone. Ignorée quand une image est connectée à l'entrée Arrière-plan : la zone prend alors les dimensions de celle-ci. |
| `height` | `number` | `512` | min 1 px · max 8000 px · pas de 1 | **Hauteur**<br />Hauteur de la zone. Ignorée quand une image est connectée à l'entrée Arrière-plan : la zone prend alors les dimensions de celle-ci. |
| `scale` | `number` | `100` | min 1 % · max 400 % · pas de 1 | **Échelle**<br />Échelle de la forme par rapport à la largeur de la zone. |
| `relativeWidth` | `number` | `100` | min 1 % · max 100 % · pas de 1 | **Largeur relative**<br />Largeur de la forme par rapport à la largeur de la zone. |

### Position

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `offsetX` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage X**<br />Décalage horizontal de la forme depuis le centre. |
| `offsetY` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage Y**<br />Décalage vertical de la forme depuis le centre. |

### Coins

> Ces réglages ne comptent que quand `shape` = `rectangle` (Rectangle).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `cornerRadius` | `number` | `0` | min 0 % · max 100 % · pas de 1 | **Arrondi**<br />Arrondi des coins, en part de la moitié du plus petit côté : 100 % fait une pilule. |

### Anneau

> Ces réglages ne comptent que quand `shape` = `ring` (Anneau).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `ringThickness` | `number` | `40` | min 1 % · max 99 % · pas de 1 | **Épaisseur**<br />Épaisseur de l'anneau. |

### Polygone

> Ces réglages ne comptent que quand `shape` = `polygon` (Polygone).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `sides` | `number` | `6` | min 3 · max 12 · pas de 1 | **Côtés**<br />Nombre de côtés du polygone. |

### Étoile

> Ces réglages ne comptent que quand `shape` = `star` (Étoile).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `starPoints` | `number` | `5` | min 3 · max 12 · pas de 1 | **Branches**<br />Nombre de branches de l'étoile. |
| `innerRatio` | `number` | `50` | min 5 % · max 95 % · pas de 1 | **Creux**<br />Profondeur du creux de l'étoile, en part du rayon extérieur. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/solid \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F background=@background.png \
  -F 'params={"shape":"rectangle","color":"#4c9caf","innerFill":100}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('background', await openAsBlob('background.png'), 'background.png')
form.append('params', JSON.stringify({"shape":"rectangle","color":"#4c9caf","innerFill":100}))

const res = await fetch('https://api.pixlub.com/v1/modules/solid', {
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
    "https://api.pixlub.com/v1/modules/solid",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("background", open("background.png", "rb"))],
    data={"params": json.dumps({"shape": "rectangle", "color": "#4c9caf", "innerFill": 100})},
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
result = client.tools.run("solid", inputs={"background": "background.png"}, params={"shape": "rectangle", "color": "#4c9caf", "innerFill": 100})
result.save(f"solid{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "solid", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "background": pixlub.FromPath("background.png"),
    },
    Params: map[string]any{"shape": "rectangle", "color": "#4c9caf", "innerFill": 100},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("solid"+result.Extension(), false)
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
  "module": "solid",
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

`GET /v1/modules/solid/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "shape": {
      "title": "Shape",
      "default": "rectangle",
      "type": "string",
      "enum": [
        "rectangle",
        "circle",
        "ellipse",
        "ring",
        "triangle",
        "diamond",
        "polygon",
        "star"
      ]
    },
    "color": {
      "title": "Color",
      "default": "#4c9caf",
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
    "innerFill": {
      "title": "Inner filling",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "backgroundOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "fillFit": {
      "title": "Fit",
      "default": "cover",
      "type": "string",
      "enum": [
        "cover",
        "contain"
      ]
    },
    "fillScale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 10,
      "maximum": 1000,
      "multipleOf": 0.1
    },
    "fillX": {
      "title": "Offset X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "fillY": {
      "title": "Offset Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "strokeWidth": {
      "title": "Thickness",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    },
    "strokeColor": {
      "title": "Color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "rotation": {
      "title": "Angle",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180
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
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 400,
      "multipleOf": 1
    },
    "relativeWidth": {
      "title": "Relative width",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "multipleOf": 1
    },
    "offsetX": {
      "title": "Offset X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "offsetY": {
      "title": "Offset Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cornerRadius": {
      "title": "Roundness",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "ringThickness": {
      "title": "Thickness",
      "default": 40,
      "type": "number",
      "minimum": 1,
      "maximum": 99,
      "multipleOf": 1
    },
    "sides": {
      "title": "Sides",
      "default": 6,
      "type": "number",
      "minimum": 3,
      "maximum": 12,
      "multipleOf": 1
    },
    "starPoints": {
      "title": "Branches",
      "default": 5,
      "type": "number",
      "minimum": 3,
      "maximum": 12,
      "multipleOf": 1
    },
    "innerRatio": {
      "title": "Inset",
      "default": 50,
      "type": "number",
      "minimum": 5,
      "maximum": 95,
      "multipleOf": 1
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
