# Fusion : référence API

Superpose une ou plusieurs images (calques) sur une autre

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/merge` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `base` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Base**<br />Image de fond sur laquelle les calques sont posés. |
| `overlay` (Image ou lot) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Calque(s)**<br />Calque ou batch de calques superposés à la base, dans l'ordre.<br />Envoyez une image, ou un lot en répétant le champ une fois par image : jusqu'à 7 images par appel. |

## Réglages

### Placement

> **1 fichier** : Une seule image dans `overlay`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `scale` | `number` | `100` | min 1 % · max 800 % · pas de 1 | **Échelle**<br />Échelle du calque. |
| `rotation` | `number` | `0` | min -180 ° · max 180 ° · pas de 1 | **Rotation**<br />Rotation du calque. |
| `offsetX` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **X**<br />Décalage horizontal du calque depuis le centre, en % de la largeur de la base. |
| `offsetY` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **Y**<br />Décalage vertical du calque depuis le centre, en % de la hauteur de la base. |

### Calque

> **1 fichier** : Une seule image dans `overlay`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `opacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité**<br />Opacité du calque. |
| `blendMode` | `string`<br />*Mode de fusion* | `"normal"` | `normal` Normal : Le calque recouvre ce qui est dessous.<br />`multiply` Produit : Fonce : le blanc disparaît.<br />`screen` Écran : Éclaircit : le noir disparaît.<br />`overlay` Incrustation : Renforce le contraste du dessous.<br />`darken` Obscurcir : Garde le plus sombre des deux.<br />`color-burn` Densité + : Fonce en saturant les couleurs.<br />`lighten` Éclaircir : Garde le plus clair des deux.<br />`color-dodge` Densité - : Éclaircit jusqu'à l'éclat.<br />`soft-light` Lumière douce : Contraste doux, comme une lumière diffuse.<br />`hard-light` Lumière crue : Contraste franc, comme un projecteur.<br />`difference` Différence : Inverse là où le calque est clair.<br />`exclusion` Exclusion : Comme Différence, en plus doux.<br />`hue` Teinte : Prend seulement la teinte du calque.<br />`saturation` Saturation : Prend seulement la saturation du calque.<br />`color` Couleur : Prend teinte et saturation, garde la clarté.<br />`luminosity` Luminosité : Prend seulement la clarté du calque. | **Mode de fusion**<br />Mode de fusion du calque. |

### Composition

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `overlayOnTop` | `boolean` | `true` |  | **Calque au-dessus de la base**<br />Passe le ou les calques au-dessus de la base ; sinon, la base les recouvre. |

### Calques

> **Plusieurs fichiers** : Plusieurs images dans `overlay`, jusqu'à 7 : leur nombre se déduit des fichiers envoyés, vous ne l'envoyez pas.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `layers` | [`MergeLayer[]`](#type-mergelayer)<br />*Liste d'objets* | `[]` |  | **Calques**<br />Liste des calques avec leur placement et mode de fusion.<br />*Liste d'objets* : Un élément par fichier `overlay`, dans l'ordre d'envoi ; au plus 7. Liste d'objets `MergeLayer`, détaillés ci-dessous ; un membre omis garde sa valeur par défaut.<br />Structure de MergeLayer[] et exemple : [`MergeLayer`](#type-mergelayer) |

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
curl -X POST https://api.pixlub.com/v1/modules/merge \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F base=@base.png \
  -F overlay=@overlay-1.png \
  -F overlay=@overlay-2.png \
  -F 'params={"layers":[{"scale":60,"offsetX":-25,"offsetY":0},{"scale":40,"rotation":15,"offsetX":25,"opacity":80,"blendMode":"multiply"}],"overlayOnTop":true}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('base', await openAsBlob('base.png'), 'base.png')
form.append('overlay', await openAsBlob('overlay-1.png'), 'overlay-1.png')
form.append('overlay', await openAsBlob('overlay-2.png'), 'overlay-2.png')
form.append('params', JSON.stringify({"layers":[{"scale":60,"offsetX":-25,"offsetY":0},{"scale":40,"rotation":15,"offsetX":25,"opacity":80,"blendMode":"multiply"}],"overlayOnTop":true}))

const res = await fetch('https://api.pixlub.com/v1/modules/merge', {
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
    "https://api.pixlub.com/v1/modules/merge",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("base", open("base.png", "rb")), ("overlay", open("overlay-1.png", "rb")), ("overlay", open("overlay-2.png", "rb"))],
    data={"params": json.dumps({"layers": [{"scale": 60, "offsetX": -25, "offsetY": 0}, {"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}], "overlayOnTop": True})},
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
result = client.tools.run("merge", inputs={"base": "base.png", "overlay": "overlay.png"}, params={"layers": [{"scale": 60, "offsetX": -25, "offsetY": 0}, {"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}], "overlayOnTop": True})
result.save(f"merge{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "merge", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "base": pixlub.FromPath("base.png"),
        "overlay": pixlub.FromPath("overlay.png"),
    },
    Params: map[string]any{"layers": []any{map[string]any{"scale": 60, "offsetX": -25, "offsetY": 0}, map[string]any{"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}}, "overlayOnTop": true},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("merge"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Base et calques fusionnés en une image. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "merge",
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

**Exemple de MergeLayer[]**

```json
[
  {
    "scale": 60,
    "offsetX": -25,
    "offsetY": 0
  },
  {
    "scale": 40,
    "rotation": 15,
    "offsetX": 25,
    "opacity": 80,
    "blendMode": "multiply"
  }
]
```

<a name="type-mergelayer"></a>

### MergeLayer

*Objet*. Placement et aspect d'un calque, posé au centre de la base puis décalé.

| Membre | Type | Description |
| --- | --- | --- |
| `scale` | `number` | *facultatif* · Échelle du calque. De 1 à 800 %. `100` par défaut. |
| `rotation` | `number` | *facultatif* · Rotation du calque. De -180 à 180 °. `0` par défaut. |
| `offsetX` | `number` | *facultatif* · Décalage horizontal du calque depuis le centre, en % de la largeur de la base. De -100 à 100 %. `0` par défaut. |
| `offsetY` | `number` | *facultatif* · Décalage vertical du calque depuis le centre, en % de la hauteur de la base. De -100 à 100 %. `0` par défaut. |
| `opacity` | `number` | *facultatif* · Opacité du calque. De 0 à 100 %. `100` par défaut. |
| `blendMode` | `string` | *facultatif* · Mode de fusion du calque. `"normal"` par défaut.<br />`normal` Normal : Le calque recouvre ce qui est dessous.<br />`multiply` Produit : Fonce : le blanc disparaît.<br />`screen` Écran : Éclaircit : le noir disparaît.<br />`overlay` Incrustation : Renforce le contraste du dessous.<br />`darken` Obscurcir : Garde le plus sombre des deux.<br />`color-burn` Densité + : Fonce en saturant les couleurs.<br />`lighten` Éclaircir : Garde le plus clair des deux.<br />`color-dodge` Densité - : Éclaircit jusqu'à l'éclat.<br />`soft-light` Lumière douce : Contraste doux, comme une lumière diffuse.<br />`hard-light` Lumière crue : Contraste franc, comme un projecteur.<br />`difference` Différence : Inverse là où le calque est clair.<br />`exclusion` Exclusion : Comme Différence, en plus doux.<br />`hue` Teinte : Prend seulement la teinte du calque.<br />`saturation` Saturation : Prend seulement la saturation du calque.<br />`color` Couleur : Prend teinte et saturation, garde la clarté.<br />`luminosity` Luminosité : Prend seulement la clarté du calque. |

**Exemple**

```json
{
  "scale": 60,
  "offsetX": -25,
  "offsetY": 0
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/merge/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 800,
      "multipleOf": 1
    },
    "rotation": {
      "title": "Rotation",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "offsetX": {
      "title": "X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "offsetY": {
      "title": "Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "opacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "blendMode": {
      "title": "Blend mode",
      "default": "normal",
      "type": "string",
      "enum": [
        "normal",
        "multiply",
        "screen",
        "overlay",
        "darken",
        "color-burn",
        "lighten",
        "color-dodge",
        "soft-light",
        "hard-light",
        "difference",
        "exclusion",
        "hue",
        "saturation",
        "color",
        "luminosity"
      ]
    },
    "overlayOnTop": {
      "title": "Layer above the base",
      "default": true,
      "type": "boolean"
    },
    "layers": {
      "title": "Layers",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "scale": {
            "title": "Scale",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 800,
            "multipleOf": 1
          },
          "rotation": {
            "title": "Rotation",
            "default": 0,
            "type": "number",
            "minimum": -180,
            "maximum": 180,
            "multipleOf": 1
          },
          "offsetX": {
            "title": "X",
            "default": 0,
            "type": "number",
            "minimum": -100,
            "maximum": 100,
            "multipleOf": 0.1
          },
          "offsetY": {
            "title": "Y",
            "default": 0,
            "type": "number",
            "minimum": -100,
            "maximum": 100,
            "multipleOf": 0.1
          },
          "opacity": {
            "title": "Opacity",
            "default": 100,
            "type": "number",
            "minimum": 0,
            "maximum": 100,
            "multipleOf": 1
          },
          "blendMode": {
            "title": "Blend mode",
            "default": "normal",
            "type": "string",
            "enum": [
              "normal",
              "multiply",
              "screen",
              "overlay",
              "darken",
              "color-burn",
              "lighten",
              "color-dodge",
              "soft-light",
              "hard-light",
              "difference",
              "exclusion",
              "hue",
              "saturation",
              "color",
              "luminosity"
            ]
          }
        }
      },
      "maxItems": 16
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
