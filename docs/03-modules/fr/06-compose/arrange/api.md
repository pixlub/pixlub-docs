# Disposition : référence API

Aligne plusieurs images côte à côte ou empilées (bandeaux, comparatifs)

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/arrange` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `a1` (Image ou lot) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image 1**<br />Image (ou batch) placée en position 1 de la disposition.<br />Envoyez une image, ou un lot en répétant le champ une fois par image : jusqu'à 8 images par appel. |

## Réglages

### Général

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `direction` | `string` | `"horizontal"` | `horizontal` Horizontal : Disposition horizontale des images.<br />`vertical` Vertical : Disposition verticale des images. | **Direction**<br />Direction de la disposition des images. |
| `align` | `string` | `"center"` | `start` Début : Aligner les images en haut de la disposition.<br />`center` Centre : Aligner les images au centre de la disposition.<br />`end` Fin : Aligner les images en bas de la disposition. | **Alignement**<br />Alignement des images dans la disposition. |
| `fit` | `string` | `"none"` | `none` Aucun : Ne pas ajuster les images.<br />`fit` Ajuster : Ajuster les images pour qu'elles s'adaptent à la disposition.<br />`stretch` Étirer : Étirer les images pour remplir l'espace disponible. | **Ajustement**<br />Ajustement des images dans la disposition. |
| `gap` | `number` | `0` | min 0 px · max 500 px · pas de 1 | **Espacement**<br />Espacement entre les images de la disposition. |

### Fond

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `bgTransparent` | `boolean` | `true` |  | **Transparent** |
| `bgColor` | `Color`<br />*Couleur unie* | `"#ffffff"` |  | **Couleur**<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/arrange \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F a1=@a1-1.png \
  -F a1=@a1-2.png \
  -F 'params={"direction":"horizontal","align":"center","fit":"none"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('a1', await openAsBlob('a1-1.png'), 'a1-1.png')
form.append('a1', await openAsBlob('a1-2.png'), 'a1-2.png')
form.append('params', JSON.stringify({"direction":"horizontal","align":"center","fit":"none"}))

const res = await fetch('https://api.pixlub.com/v1/modules/arrange', {
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
    "https://api.pixlub.com/v1/modules/arrange",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("a1", open("a1-1.png", "rb")), ("a1", open("a1-2.png", "rb"))],
    data={"params": json.dumps({"direction": "horizontal", "align": "center", "fit": "none"})},
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
result = client.tools.run("arrange", inputs={"a1": "a1.png"}, params={"direction": "horizontal", "align": "center", "fit": "none"})
result.save(f"arrange{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "arrange", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "a1": pixlub.FromPath("a1.png"),
    },
    Params: map[string]any{"direction": "horizontal", "align": "center", "fit": "none"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("arrange"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Images reçues disposées sur une même image. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "arrange",
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

`GET /v1/modules/arrange/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "direction": {
      "title": "Direction",
      "default": "horizontal",
      "type": "string",
      "enum": [
        "horizontal",
        "vertical"
      ]
    },
    "align": {
      "title": "Alignment",
      "default": "center",
      "type": "string",
      "enum": [
        "start",
        "center",
        "end"
      ]
    },
    "fit": {
      "title": "Adjustment",
      "default": "none",
      "type": "string",
      "enum": [
        "none",
        "fit",
        "stretch"
      ]
    },
    "gap": {
      "title": "Spacing",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 500,
      "multipleOf": 1
    },
    "bgTransparent": {
      "title": "Transparent",
      "default": true,
      "type": "boolean"
    },
    "bgColor": {
      "title": "Color",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
