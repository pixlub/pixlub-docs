# Marionnette : référence API

Déforme l'image en déplaçant des épingles sur un maillage (puppet warp)

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/puppet` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Image seule) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image déformée par les épingles. |

## Réglages

### Déformation

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `rigidity` | `number` | `40` | min 0 % · max 100 % | **Rigidité**<br />Détermine à quel point le reste de l'image suit les épingles déplacées |

### Épingles

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `pins` | [`PuppetPin[]`](#type-puppetpin)<br />*Liste d'objets* | `[]` |  | **Épingles**<br />Épingles plantées dans l'image puis déplacées : le maillage suit chacune de sa position de départ à sa cible. Sans épingle déplacée, l'image reste telle quelle.<br />*Liste d'objets* : Liste d'objets `PuppetPin`, détaillés ci-dessous ; un membre omis garde sa valeur par défaut.<br />Structure de PuppetPin[] et exemple : [`PuppetPin`](#type-puppetpin) |

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
curl -X POST https://api.pixlub.com/v1/modules/puppet \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"pins":[{"x0":0.5,"y0":0.3,"x1":0.58,"y1":0.22},{"x0":0.5,"y0":0.8,"x1":0.5,"y1":0.8}],"rigidity":40}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"pins":[{"x0":0.5,"y0":0.3,"x1":0.58,"y1":0.22},{"x0":0.5,"y0":0.8,"x1":0.5,"y1":0.8}],"rigidity":40}))

const res = await fetch('https://api.pixlub.com/v1/modules/puppet', {
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
    "https://api.pixlub.com/v1/modules/puppet",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"pins": [{"x0": 0.5, "y0": 0.3, "x1": 0.58, "y1": 0.22}, {"x0": 0.5, "y0": 0.8, "x1": 0.5, "y1": 0.8}], "rigidity": 40})},
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
result = client.tools.run("puppet", image="photo.png", params={"pins": [{"x0": 0.5, "y0": 0.3, "x1": 0.58, "y1": 0.22}, {"x0": 0.5, "y0": 0.8, "x1": 0.5, "y1": 0.8}], "rigidity": 40})
result.save(f"puppet{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "puppet", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"pins": []any{map[string]any{"x0": 0.5, "y0": 0.3, "x1": 0.58, "y1": 0.22}, map[string]any{"x0": 0.5, "y0": 0.8, "x1": 0.5, "y1": 0.8}}, "rigidity": 40},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("puppet"+result.Extension(), false)
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
  "module": "puppet",
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

**Exemple de PuppetPin[]**

```json
[
  {
    "x0": 0.5,
    "y0": 0.3,
    "x1": 0.58,
    "y1": 0.22
  },
  {
    "x0": 0.5,
    "y0": 0.8,
    "x1": 0.5,
    "y1": 0.8
  }
]
```

<a name="type-puppetpin"></a>

### PuppetPin

*Objet*. Épingle : le point de l'image qu'elle tient, puis là où elle l'emmène, de 0 à 1 dans l'image.

| Membre | Type | Description |
| --- | --- | --- |
| `x0` | `number` | Départ, horizontal : de 0 (gauche) à 1 (droite). De 0 à 1. |
| `y0` | `number` | Départ, vertical : de 0 (haut) à 1 (bas). De 0 à 1. |
| `x1` | `number` | Cible, horizontale. De 0 à 1. |
| `y1` | `number` | Cible, verticale. Une épingle dont la cible est son départ tient l'image en place. De 0 à 1. |

**Exemple**

```json
{
  "x0": 0.5,
  "y0": 0.3,
  "x1": 0.58,
  "y1": 0.22
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/puppet/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "rigidity": {
      "title": "Stiffness",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "pins": {
      "title": "Pins",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "x0": {
            "title": "x0",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y0": {
            "title": "y0",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "x1": {
            "title": "x1",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y1": {
            "title": "y1",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          }
        },
        "required": [
          "x0",
          "y0",
          "x1",
          "y1"
        ]
      }
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
