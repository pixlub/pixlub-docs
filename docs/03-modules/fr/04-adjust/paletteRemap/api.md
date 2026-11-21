# Palette : recolorer : référence API

Génère une variante recolorée de l'image par couleur de la palette (batch)

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/paletteRemap` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image recolorée. |

## Réglages

### Palette

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `colors` | `Color[]`<br />*Liste de couleurs* | [JSON](#default-colors) |  | **Couleurs**<br />Couleurs de la palette : une variante de l'image par couleur. Ignorées quand une palette est reliée à l'entrée Palette.<br />*Liste de couleurs* : Liste de couleurs CSS, dans l'ordre. |

<a name="default-colors"></a>

**Valeur par défaut de `colors`**

```json
[
  "#264653",
  "#2a9d8f",
  "#e9c46a",
  "#f4a261",
  "#e76f51"
]
```

### Général

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `preserveLum` | `boolean` | `true` |  | **Préserver la luminosité**<br />Garde la clarté de l'image telle quelle : seule la teinte change, jamais la luminosité générale. |
| `mix` | `number` | `100` | min 0 % · max 100 % | **Intensité**<br />Dosage de la recoloration : 0 % laisse l'image intacte, 100 % la recolore complètement. |

### Correspondance

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `limitToBase` | `boolean` | `false` |  | **Limiter à une couleur de base**<br />Ne recolore que les pixels proches de la couleur de base. |
| `minSaturation` | `number` | `0` | min 0 % · max 100 % | **Saturation minimale**<br />Ne recolore que les pixels dont la saturation est au moins de ce pourcentage. |
| `feather` | `number` | `25` | min 0 % · max 100 % | **Adoucissement**<br />Adoucit les transitions entre les zones recolorées et les zones non recolorées. |

### Couleur de base

> Ces réglages ne comptent que quand `limitToBase` = `true`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `baseColor` | `Color`<br />*Couleur unie* | `"#e76f51"` |  | **Couleur**<br />Couleur de base : les pixels proches de cette couleur sont recolorés.<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |
| `hueTolerance` | `number` | `60` | min 1 ° · max 180 ° | **Tolérance de teinte**<br />Tolérance de teinte : les pixels proches de la couleur de base sont recolorés. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/paletteRemap \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"preserveLum":true,"mix":100,"limitToBase":false}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"preserveLum":true,"mix":100,"limitToBase":false}))

const res = await fetch('https://api.pixlub.com/v1/modules/paletteRemap', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out#0')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/paletteRemap",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"preserveLum": True, "mix": 100, "limitToBase": False})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out#0")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("paletteRemap", image="photo.png", params={"preserveLum": True, "mix": 100, "limitToBase": False})
result.save(f"paletteRemap{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "paletteRemap", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"preserveLum": true, "mix": 100, "limitToBase": false},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("paletteRemap"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image[]` | `PNG` | **Batch**<br />Une variante recolorée par couleur de la palette, dans l'ordre des couleurs.<br />Un fichier par image du lot, sous les clés `out#0`, `out#1`… |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "paletteRemap",
  "outputs": [
    {
      "key": "out#0",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    },
    {
      "key": "out#1",
      "name": "image",
      "url": "https://files.pixlub.com/r/5f0c2a91-8d3e-4b7a-a1c4-6e2d9b0f3a58_result.png?exp=1767268800&sig=…",
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

`GET /v1/modules/paletteRemap/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "colors": {
      "title": "Colors",
      "default": [
        "#264653",
        "#2a9d8f",
        "#e9c46a",
        "#f4a261",
        "#e76f51"
      ],
      "type": "array",
      "items": {
        "type": "string",
        "minLength": 1
      },
      "minItems": 1,
      "maxItems": 32
    },
    "preserveLum": {
      "title": "Preserve brightness",
      "default": true,
      "type": "boolean"
    },
    "mix": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "limitToBase": {
      "title": "Limit to a base color",
      "default": false,
      "type": "boolean"
    },
    "minSaturation": {
      "title": "Minimum saturation",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "feather": {
      "title": "Softness",
      "default": 25,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "baseColor": {
      "title": "Color",
      "default": "#e76f51",
      "type": "string",
      "minLength": 1
    },
    "hueTolerance": {
      "title": "Hue tolerance",
      "default": 60,
      "type": "number",
      "minimum": 1,
      "maximum": 180
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
