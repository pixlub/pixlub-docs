# Conversion : référence API

Convertit images, animations, vidéos et sons vers n’importe quel format de l’export : PNG, JPG, WebP, GIF, MP4, WebM, MP3, FLAC, WAV, PDF…

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/convert` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Une image ou plusieurs) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image(s) à convertir dans le format choisi. |

## Réglages

### Format de sortie

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `format` | `string` | `"png"` | `png` PNG<br />`jpg` JPG<br />`webp` WebP | **Format**<br />Format de sortie des images. |

### Qualité

> Ces réglages ne comptent que quand `format` = `jpg` (JPG) ou `webp` (WebP).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `quality` | `number` | `90` | min 1 % · max 100 % · pas de 1 | **Qualité**<br />Qualité de l'image compressée. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/convert \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"format":"png"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"format":"png"}))

const res = await fetch('https://api.pixlub.com/v1/modules/convert', {
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
    "https://api.pixlub.com/v1/modules/convert",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"format": "png"})},
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
result = client.tools.run("convert", image="photo.png", params={"format": "png"})
result.save(f"convert{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "convert", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"format": "png"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("convert"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

### 1 fichier

> **1 fichier** : Une seule image dans `in`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG`, `JPEG`, `WebP` | **Image(s)**<br />Image convertie, dans le format choisi par `format`.<br />Une seule image envoyée : le fichier garde la clé `out`.<br />Le format suit le réglage `format`. |

### Plusieurs fichiers

> **Plusieurs fichiers** : Plusieurs images dans `in`, jusqu'à 64 : leur nombre se déduit des fichiers envoyés, vous ne l'envoyez pas.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG`, `JPEG`, `WebP` | **Image(s)**<br />Image convertie, dans le format choisi par `format`.<br />Plusieurs images envoyées dans `in` : un fichier par image, sous les clés `out#0`, `out#1`…, dans l'ordre d'envoi.<br />Le format suit le réglage `format`. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "convert",
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

`GET /v1/modules/convert/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "format": {
      "title": "Format",
      "default": "png",
      "type": "string",
      "enum": [
        "png",
        "jpg",
        "webp"
      ]
    },
    "quality": {
      "title": "Quality",
      "default": 90,
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "multipleOf": 1
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
