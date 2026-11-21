# Décalcomanie : référence API

Reconstruit via IA (nos services) le relief 3D de l'objet, puis y drape l'image que vous placez librement dessus. Seule la photo est envoyée, une seule fois ; l'image posée reste sur votre machine.

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/decalApi` | 25 crédits par opération |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `base` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF` | **Surface**<br />Photo de l'objet dont le relief 3D est reconstruit. C'est la seule image envoyée au serveur. |
| `decal` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF` | **Motif**<br />Image posée et drapée sur l'objet. |

## Réglages

### Placement

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `anchorX` | `number` | `50` | min 0 % · max 100 % · pas de 0.1 | **X**<br />Position horizontale de l'image sur la surface de l'objet. |
| `anchorY` | `number` | `50` | min 0 % · max 100 % · pas de 0.1 | **Y**<br />Position verticale de l'image sur la surface de l'objet. |
| `size` | `number` | `40` | min 1 % · max 150 % · pas de 0.1 | **Taille**<br />Taille de l'image posée, en pourcentage de la largeur de l'objet. |
| `rotation` | `number` | `0` | min -180 ° · max 180 ° · pas de 1 | **Rotation**<br />Rotation de l'image posée, en degrés. |
| `reliefDepth` | `number` | `100` | min 0 % · max 300 % · pas de 1 | **Profondeur du relief**<br />Accentue ou aplatit la forme reconstruite. |

### Lumière

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `lighting` | `number` | `50` | min 0 % · max 100 % | **Reflets et ombres**<br />Intensité des reflets et ombres sur l'image posée. |
| `folds` | `number` | `0` | min 0 % · max 100 % | **Plis**<br />Intensité des plis et ondulations sur l'image posée. |

### Calque

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `opacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité**<br />Opacité du calque. |
| `blendMode` | `string`<br />*Mode de fusion* | `"normal"` | `normal` Normal : Le calque recouvre ce qui est dessous.<br />`multiply` Produit : Fonce : le blanc disparaît.<br />`screen` Écran : Éclaircit : le noir disparaît.<br />`overlay` Incrustation : Renforce le contraste du dessous.<br />`darken` Obscurcir : Garde le plus sombre des deux.<br />`color-burn` Densité + : Fonce en saturant les couleurs.<br />`lighten` Éclaircir : Garde le plus clair des deux.<br />`color-dodge` Densité - : Éclaircit jusqu'à l'éclat.<br />`soft-light` Lumière douce : Contraste doux, comme une lumière diffuse.<br />`hard-light` Lumière crue : Contraste franc, comme un projecteur.<br />`difference` Différence : Inverse là où le calque est clair.<br />`exclusion` Exclusion : Comme Différence, en plus doux.<br />`hue` Teinte : Prend seulement la teinte du calque.<br />`saturation` Saturation : Prend seulement la saturation du calque.<br />`color` Couleur : Prend teinte et saturation, garde la clarté.<br />`luminosity` Luminosité : Prend seulement la clarté du calque. | **Mode de fusion**<br />Mode de fusion du calque. |
| `clipToBase` | `boolean` | `true` |  | **Rester sur l'objet**<br />Si activé, l'image posée ne dépasse pas les bords de l'objet. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/decalApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F base=@base.png \
  -F decal=@decal.png \
  -F 'params={"anchorX":50,"anchorY":50,"size":40}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('base', await openAsBlob('base.png'), 'base.png')
form.append('decal', await openAsBlob('decal.png'), 'decal.png')
form.append('params', JSON.stringify({"anchorX":50,"anchorY":50,"size":40}))

const res = await fetch('https://api.pixlub.com/v1/modules/decalApi', {
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
    "https://api.pixlub.com/v1/modules/decalApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("base", open("base.png", "rb")), ("decal", open("decal.png", "rb"))],
    data={"params": json.dumps({"anchorX": 50, "anchorY": 50, "size": 40})},
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
result = client.tools.run("decalApi", inputs={"base": "base.png", "decal": "decal.png"}, params={"anchorX": 50, "anchorY": 50, "size": 40})
result.save(f"decalApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "decalApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "base": pixlub.FromPath("base.png"),
        "decal": pixlub.FromPath("decal.png"),
    },
    Params: map[string]any{"anchorX": 50, "anchorY": 50, "size": 40},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("decalApi"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image**<br />Photo avec l'image posée drapée sur son relief. |
| `data` | [`DecalSurface`](#type-decalsurface) | `JSON` | **Données**<br />Données détectées par le service distant, en JSON.<br />Contenu du fichier : un objet `DecalSurface`. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "decalApi",
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
    "cost": 25,
    "balance": 190
  }
}
```

## Types

Les valeurs structurées des réglages, détaillées comme des classes : chaque membre avec son type, puis un exemple.

<a name="type-decalsurface"></a>

### DecalSurface

*Objet*. Relief 3D reconstruit de l'objet photographié, sur lequel l'image posée a été drapée. Positions de 0 à 1 dans l'image envoyée.

| Membre | Type | Description |
| --- | --- | --- |
| `relief` | `ReliefGrid` | Hauteur de la surface en chaque point d'une grille. |
| `outline` | `[number, number][] \| null` | Silhouette de l'objet, points `[x, y]` dans l'ordre ; `null` quand aucun objet ne se détache du fond. |
| `anchor` | `[number, number]` | Centre de l'objet `[x, y]` : le placement proposé quand `anchorX` et `anchorY` ne sont pas envoyés. |
| `width` | `number` | Taille proposée de l'image posée, en fraction de la largeur, quand `size` n'est pas envoyé. |
| `size` | `[number, number]` | Taille `[largeur, hauteur]` de l'image analysée, en pixels (réduite à 768 au plus). |

**Exemple**

```json
{
  "relief": {
    "w": 96,
    "h": 72,
    "depth": 0.18342,
    "data": "AAAAAAAAAAD/f/9//3//f…"
  },
  "outline": [
    [
      0.2141,
      0.1875
    ],
    [
      0.7969,
      0.2031
    ],
    [
      0.8125,
      0.8594
    ],
    [
      0.1953,
      0.8438
    ]
  ],
  "anchor": [
    0.5021,
    0.5234
  ],
  "width": 0.4688,
  "size": [
    768,
    576
  ]
}
```

<a name="type-reliefgrid"></a>

### ReliefGrid

*Objet*. Grille de hauteurs, ligne par ligne depuis le haut.

| Membre | Type | Description |
| --- | --- | --- |
| `w` | `integer` | Colonnes de la grille. |
| `h` | `integer` | Lignes de la grille. |
| `depth` | `number` | Profondeur du relief le plus haut, en fraction de la largeur de l'image. |
| `data` | `string` | Hauteurs de 0 (fond) à 1 (le plus proche) : `w × h` entiers 16 bits petit boutiste (0 à 65535), en base64. |

**Exemple**

```json
{
  "w": 96,
  "h": 72,
  "depth": 0.18342,
  "data": "AAAAAAAAAAD/f/9//3//f…"
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/decalApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "anchorX": {
      "title": "X",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "anchorY": {
      "title": "Y",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "size": {
      "title": "Size",
      "default": 40,
      "type": "number",
      "minimum": 1,
      "maximum": 150,
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
    "reliefDepth": {
      "title": "Relief depth",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 300,
      "multipleOf": 1
    },
    "lighting": {
      "title": "Highlights and shadows",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "folds": {
      "title": "Folds",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100
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
    "clipToBase": {
      "title": "Stay on the object",
      "default": true,
      "type": "boolean"
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
