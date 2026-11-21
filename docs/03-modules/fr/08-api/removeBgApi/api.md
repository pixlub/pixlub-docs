# Retirer un fond : référence API

Détecte le sujet par IA (par nos services) et rend transparent tout le reste, quel que soit le fond.

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/removeBgApi` | 10 crédits par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `image` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF` | **Image**<br />Image envoyée au serveur, dont le sujet est détecté et le fond rendu transparent. |

## Réglages

Ce module n'a aucun réglage.

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F 'params={}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('params', JSON.stringify({}))

const res = await fetch('https://api.pixlub.com/v1/modules/removeBgApi', {
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
    "https://api.pixlub.com/v1/modules/removeBgApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb"))],
    data={"params": json.dumps({})},
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
result = client.tools.run("removeBgApi", inputs={"image": "image.png"})
result.save(f"removeBgApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "removeBgApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
    },
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("removeBgApi"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `WebP` | **Image(s)**<br />Image détourée sur fond transparent, en WebP sans perte. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "removeBgApi",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.webp?exp=1767268800&sig=…",
      "content_type": "image/webp",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 10,
    "balance": 190
  }
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/removeBgApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {}
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
