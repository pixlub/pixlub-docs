# Masque : référence API

Module l'opacité d'une image par la luminance (ou l'alpha) d'un masque

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/mask` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `image` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image dont l'opacité est modulée. |
| `mask` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Masque**<br />Masque : sa luminance (ou son alpha) fixe l'opacité de l'image, blanc = visible, noir = transparent. |

## Réglages

### Masque

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `source` | `string` | `"luminance"` | `luminance` Luminance : Utiliser la luminance du masque.<br />`alpha` Alpha : Utiliser l'alpha du masque. | **Canal du masque**<br />Canal du masque utilisé pour moduler l'opacité de l'image. |
| `fit` | `string` | `"native"` | `native` Native (taille réelle)<br />`contain` Contenir (ratio préservé) : Ajuste le masque pour qu'il tienne dans l'image.<br />`cover` Couvrir (ratio préservé) : Ajuste le masque pour qu'il couvre toute l'image.<br />`stretch` Étirer (déforme) : Étire le masque pour remplir l'espace disponible. | **Ajustement**<br />Ajustement du masque sur l'image. |
| `anchor` | `string`<br />*Ancrage* | `"center"` | [grille ci-dessous](#anchor-anchor) | **Position**<br />Position du masque sur l'image.<br />*Ancrage* : Point d'une grille 3 × 3, du coin haut gauche au coin bas droit. |
| `offsetX` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **X**<br />Décalage horizontal du masque, en % de la largeur de l'image. |
| `offsetY` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **Y**<br />Décalage vertical du masque, en % de la hauteur de l'image. |
| `invert` | `boolean` | `false` |  | **Inverser le masque**<br />Inverser le masque. |

<a name="anchor-anchor"></a>

**Positions de `anchor`**

| | Gauche | Centre | Droite |
| --- | --- | --- | --- |
| **Haut** | `top-left`<br />En haut à gauche | `top`<br />En haut | `top-right`<br />En haut à droite |
| **Milieu** | `left`<br />À gauche | **`center`**<br />**Au centre** | `right`<br />À droite |
| **Bas** | `bottom-left`<br />En bas à gauche | `bottom`<br />En bas | `bottom-right`<br />En bas à droite |

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
curl -X POST https://api.pixlub.com/v1/modules/mask \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F mask=@mask.png \
  -F 'params={"source":"luminance","fit":"native","anchor":"center"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('mask', await openAsBlob('mask.png'), 'mask.png')
form.append('params', JSON.stringify({"source":"luminance","fit":"native","anchor":"center"}))

const res = await fetch('https://api.pixlub.com/v1/modules/mask', {
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
    "https://api.pixlub.com/v1/modules/mask",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb")), ("mask", open("mask.png", "rb"))],
    data={"params": json.dumps({"source": "luminance", "fit": "native", "anchor": "center"})},
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
result = client.tools.run("mask", inputs={"image": "image.png", "mask": "mask.png"}, params={"source": "luminance", "fit": "native", "anchor": "center"})
result.save(f"mask{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "mask", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
        "mask": pixlub.FromPath("mask.png"),
    },
    Params: map[string]any{"source": "luminance", "fit": "native", "anchor": "center"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("mask"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image dont l'opacité suit le masque. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "mask",
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

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/mask/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "source": {
      "title": "Mask channel",
      "default": "luminance",
      "type": "string",
      "enum": [
        "luminance",
        "alpha"
      ]
    },
    "fit": {
      "title": "Adjustment",
      "default": "native",
      "type": "string",
      "enum": [
        "native",
        "contain",
        "cover",
        "stretch"
      ]
    },
    "anchor": {
      "title": "Position",
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
    "invert": {
      "title": "Invert the mask",
      "default": false,
      "type": "boolean"
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
