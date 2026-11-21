# Balance des couleurs : référence API

Ajuste les teintes par plage de tons (clairs, moyens, foncés), masquable

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/colorBalance` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image dont les teintes sont ajustées. |
| `mask` (Image seule) | non | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Masque**<br />Masque facultatif : le réglage suit sa clarté, blanc = plein effet, noir = aucun. Absent, toute l'image est réglée. |

## Réglages

### Général

#### Clairs

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `highsCR` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Cyan ↔ Rouge**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |
| `highsMG` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Magenta ↔ Vert**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |
| `highsYB` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Jaune ↔ Bleu**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |

#### Moyens

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `midsCR` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Cyan ↔ Rouge**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |
| `midsMG` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Magenta ↔ Vert**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |
| `midsYB` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Jaune ↔ Bleu**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |

#### Foncés

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `shadowsCR` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Cyan ↔ Rouge**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |
| `shadowsMG` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Magenta ↔ Vert**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |
| `shadowsYB` | `number`<br />*Axe de couleur* | `0` | min -100 · max 100 | **Jaune ↔ Bleu**<br />*Axe de couleur* : De -100 (première teinte) à 100 (seconde teinte) ; 0 ne change rien. |

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `preserveLum` | `boolean` | `true` |  | **Préserver la luminosité**<br />Garde la clarté de l'image telle quelle : seule la teinte change, jamais la luminosité générale. |

### Fusion

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Mode de fusion* | `"normal"` | `normal` Normal : Le calque recouvre ce qui est dessous.<br />`multiply` Produit : Fonce : le blanc disparaît.<br />`screen` Écran : Éclaircit : le noir disparaît.<br />`overlay` Incrustation : Renforce le contraste du dessous.<br />`darken` Obscurcir : Garde le plus sombre des deux.<br />`color-burn` Densité + : Fonce en saturant les couleurs.<br />`lighten` Éclaircir : Garde le plus clair des deux.<br />`color-dodge` Densité - : Éclaircit jusqu'à l'éclat.<br />`soft-light` Lumière douce : Contraste doux, comme une lumière diffuse.<br />`hard-light` Lumière crue : Contraste franc, comme un projecteur.<br />`difference` Différence : Inverse là où le calque est clair.<br />`exclusion` Exclusion : Comme Différence, en plus doux.<br />`hue` Teinte : Prend seulement la teinte du calque.<br />`saturation` Saturation : Prend seulement la saturation du calque.<br />`color` Couleur : Prend teinte et saturation, garde la clarté.<br />`luminosity` Luminosité : Prend seulement la clarté du calque. | **Méthode de fusion**<br />Façon dont le réglage se pose sur l'image d'origine. |
| `blendOpacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité**<br />Dosage du réglage. |

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
curl -X POST https://api.pixlub.com/v1/modules/colorBalance \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"highsCR":0,"highsMG":0,"highsYB":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"highsCR":0,"highsMG":0,"highsYB":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/colorBalance', {
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
    "https://api.pixlub.com/v1/modules/colorBalance",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"highsCR": 0, "highsMG": 0, "highsYB": 0})},
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
result = client.tools.run("colorBalance", image="photo.png", params={"highsCR": 0, "highsMG": 0, "highsYB": 0})
result.save(f"colorBalance{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "colorBalance", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"highsCR": 0, "highsMG": 0, "highsYB": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("colorBalance"+result.Extension(), false)
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
  "module": "colorBalance",
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

`GET /v1/modules/colorBalance/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "highsCR": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "highsMG": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "highsYB": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "midsCR": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "midsMG": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "midsYB": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "shadowsCR": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "shadowsMG": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "shadowsYB": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "preserveLum": {
      "title": "Preserve brightness",
      "default": true,
      "type": "boolean"
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
    "blendOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
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
