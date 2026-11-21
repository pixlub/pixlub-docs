# Particules : référence API

Disperse une image source (ou un mélange d'images d'un batch) en particules (forme d'émission, traînées, atténuation), pilotées par une graine

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/particles` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Image ou lot) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image dispersée en particules ; un batch mélange ses images entre les particules.<br />Envoyez une image, ou un lot en répétant le champ une fois par image : jusqu'à 8 images par appel. |

## Réglages

### Général

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `seed` | `number` | `1` | min 0 | **Graine**<br />Graine aléatoire pour générer les particules. |
| `count` | `number` | `200` | min 1 · max 3000 · pas de 1 | **Nombre**<br />Nombre de particules. |

### Émission

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `emission` | `string` | `"disk"` | `rectangle` Rectangle : Émission sur toute la surface du rectangle.<br />`disk` Disque : Émission depuis un centre, dans un rayon.<br />`ring` Anneau : Émission entre deux rayons.<br />`cone` Cône : Émission sous forme d'un éventail orienté.<br />`path` Tracé : Émission le long d'une courbe. | **Forme**<br />Type d'émission des particules. |

### Dimensions

> Ces réglages ne comptent que quand `emission` = `rectangle` (Rectangle) ou `path` (Tracé), ou `motion` = `true`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | min 1 px · max 4000 px · pas de 1 | **Largeur**<br />Largeur de la zone d'émission. |
| `height` | `number` | `512` | min 1 px · max 4000 px · pas de 1 | **Hauteur**<br />Hauteur de la zone d'émission. |

### Centre & rayon

> Ces réglages ne comptent que quand `emission` = `disk` (Disque) ou `ring` (Anneau) ou `cone` (Cône).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `centerX` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **Décalage X**<br />Décalage horizontal du centre de l'émission depuis le milieu, en % de la largeur. |
| `centerY` | `number` | `0` | min -100 % · max 100 % · pas de 0.1 | **Décalage Y**<br />Décalage vertical du centre de l'émission depuis le milieu, en % de la hauteur. |
| `radius` | `number` | `220` | min 1 px · max 4000 px · pas de 1 | **Rayon**<br />Rayon de l'émission. |

### Tracé

> Ces réglages ne comptent que quand `emission` = `path` (Tracé).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `path` | [`Path`](#type-path)<br />*Tracé* | [JSON](#default-path) |  | **Tracé**<br />Traçage de la trajectoire des particules.<br />*Tracé* : Objet `Path` : ses ancres `points` sont placées de 0 à 1 dans le cadre, détaillées ci-dessous.<br />Structure de Path et exemple : [`Path`](#type-path), [`PathPoint`](#type-pathpoint) |
| `pathMode` | `string` | `"along"` | `along` Le long : Les particules naissent n’importe où sur la portion du tracé, puis suivent leur élan.<br />`follow` Suivre : Chaque particule parcourt la portion du tracé, du début à la fin, au fil de sa vie (animation activée). | **Mode**<br />Le long du chemin : semées sur lui. Suivre le chemin : elles le parcourent, la durée de vie réglant le temps du trajet ; seule la turbulence s’y ajoute. |
| `pathSpread` | `number` | `0` | min 0 px · max 1000 px · pas de 1 | **Dispersion**<br />Écart des particules de part et d’autre du tracé : en mode Suivre, chacune garde son couloir. |

#### Portion du tracé

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `pathStart` | `number` | `0` | min 0 % · max 100 % · pas de 0.1 | **Début**<br />Début de la portion utilisée, en % de la longueur du tracé (départ du trajet en mode Suivre). |
| `pathEnd` | `number` | `100` | min 0 % · max 100 % · pas de 0.1 | **Fin**<br />Fin de la portion utilisée, en % de la longueur du tracé (arrivée du trajet en mode Suivre). |

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `pathLag` | `number` | `0` | min 0 % · max 100 % · pas de 1 | **Étalement**<br />Retard tiré pour chaque particule, en part du trajet : à 0 %, un groupe né ensemble avance en ligne ; plus haut, il s’étire en file comme un banc.<br />*Pris en compte quand `pathMode` = `follow` (Suivre) et `motion` = `true`.* |

<a name="default-path"></a>

**Valeur par défaut de `path`**

```json
{
  "points": [
    {
      "x": 0.12,
      "y": 0.68
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.88,
      "y": 0.66
    }
  ],
  "closed": false,
  "smooth": true,
  "rounding": 0.5,
  "curve": "arc",
  "w": 512,
  "h": 512
}
```

### Anneau

> Ces réglages ne comptent que quand `emission` = `ring` (Anneau).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `innerRadius` | `number` | `0` | min 0 % · max 100 % · pas de 1 | **Rayon interne**<br />Rayon interne de l'anneau. |

### Cône

> Ces réglages ne comptent que quand `emission` = `cone` (Cône).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `coneDir` | `number` | `0` | min -180 ° · max 180 ° · pas de 1 | **Direction**<br />Direction du cône d'émission. |
| `coneWidth` | `number` | `60` | min 1 ° · max 360 ° · pas de 1 | **Ouverture**<br />Ouverture du cône d'émission. |

### Taille

> **1 fichier** : Une seule image dans `in`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `minSize` | `number` | `16` | min 1 px · max 1000 px · pas de 1 | **Min**<br />Taille minimale des particules. |
| `maxSize` | `number` | `48` | min 1 px · max 1000 px · pas de 1 | **Max**<br />Taille maximale des particules. |

### Rotation

> **1 fichier** : Une seule image dans `in`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `minRotation` | `number` | `0` | min -360 ° · max 360 ° · pas de 1 | **Min**<br />Rotation minimale des particules. |
| `maxRotation` | `number` | `0` | min -360 ° · max 360 ° · pas de 1 | **Max**<br />Rotation maximale des particules. |

### Opacité

> **1 fichier** : Une seule image dans `in`.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `minOpacity` | `number` | `60` | min 0 % · max 100 % · pas de 1 | **Min**<br />Opacité minimale des particules. |
| `maxOpacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Max**<br />Opacité maximale des particules. |

### Images du batch

> **Plusieurs fichiers** : Plusieurs images dans `in`, jusqu'à 8 : leur nombre se déduit des fichiers envoyés, vous ne l'envoyez pas.

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `sprites` | [`ParticleSprite[]`](#type-particlesprite)<br />*Liste d'objets* | `[]` |  | **Images**<br />Liste des images utilisées pour les particules.<br />*Liste d'objets* : Un élément par fichier `in`, dans l'ordre d'envoi ; au plus 8. Liste d'objets `ParticleSprite`, détaillés ci-dessous ; un membre omis garde sa valeur par défaut.<br />Structure de ParticleSprite[] et exemple : [`ParticleSprite`](#type-particlesprite) |

### Direction & traînée

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `align` | `boolean` | `false` |  | **Orienter selon la direction**<br />Les particules sont orientées selon leur direction de déplacement. |
| `upright` | `boolean` | `false` |  | **Garder à l’endroit**<br />Une particule qui file vers la gauche se retourne en miroir plutôt que de passer la tête en bas.<br />*Pris en compte quand `align` = `true`.* |
| `trail` | `number` | `0` | min 0 % · max 1000 % · pas de 1 | **Traînée**<br />Longueur de la traînée des particules. |
| `falloff` | `number` | `0` | min 0 % · max 100 % · pas de 1 | **Atténuation (distance)**<br />Atténuation de la traînée selon la distance. |

### Rendu

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Mode de fusion* | `"normal"` | `normal` Normal : Le calque recouvre ce qui est dessous.<br />`multiply` Produit : Fonce : le blanc disparaît.<br />`screen` Écran : Éclaircit : le noir disparaît.<br />`overlay` Incrustation : Renforce le contraste du dessous.<br />`darken` Obscurcir : Garde le plus sombre des deux.<br />`color-burn` Densité + : Fonce en saturant les couleurs.<br />`lighten` Éclaircir : Garde le plus clair des deux.<br />`color-dodge` Densité - : Éclaircit jusqu'à l'éclat.<br />`soft-light` Lumière douce : Contraste doux, comme une lumière diffuse.<br />`hard-light` Lumière crue : Contraste franc, comme un projecteur.<br />`difference` Différence : Inverse là où le calque est clair.<br />`exclusion` Exclusion : Comme Différence, en plus doux.<br />`hue` Teinte : Prend seulement la teinte du calque.<br />`saturation` Saturation : Prend seulement la saturation du calque.<br />`color` Couleur : Prend teinte et saturation, garde la clarté.<br />`luminosity` Luminosité : Prend seulement la clarté du calque. | **Méthode de fusion**<br />Façon dont chaque particule se pose sur celles déjà dessinées. |

### Animation

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `motion` | `boolean` | `false` |  | **Animer les particules**<br />Active l’animation des particules. Sinon, elles restent figées à la phase choisie. |

### Naissance

> Ces réglages ne comptent que quand `motion` = `true`.

#### Cycle de vie

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `spawn` | `string` | `"loop"` | `loop` Boucle : Les particules se répètent en boucle.<br />`once` Une fois : Les particules apparaissent une seule fois.<br />`frozen` Figée : Les particules restent figées. | **Naissance**<br />Mode de naissance des particules. |
| `lifetime` | `number` | `2` | min 0 s · max 20 s · pas de 0.05 | **Durée de vie**<br />Durée de vie d’une particule, depuis sa naissance jusqu’à sa disparition. |
| `delay` | `number` | `0` | min 0 s · max 20 s · pas de 0.05 | **Délai**<br />Délai avant la naissance de la première particule.<br />*Pris en compte quand `spawn` = `once` (Une fois).* |

#### Phase

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `phaseDriven` | `boolean` | `false` |  | **Piloter par phase**<br />Les particules suivent leur Phase, posée en clés sur la timeline (0 % : début, 100 % : fin du cycle). Sinon, elles suivent leur propre durée de vie.<br />*Pris en compte quand `spawn` = `loop` (Boucle), ou `spawn` = `once` (Une fois).* |
| `phase` | `number` | `50` | min 0 % · max 100 % · pas de 0.1 | **Phase**<br />Instant montré, de 0 % (début) à 100 % (fin de l’animation).<br />*Pris en compte quand `phaseDriven` = `true`, ou `spawn` = `frozen` (Figée).* |

### Élan

> Ces réglages ne comptent que quand `motion` = `true` et `emission` = `rectangle` (Rectangle) ou `disk` (Disque) ou `ring` (Anneau) ou `cone` (Cône), ou `motion` = `true` et `pathMode` = `along` (Le long).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `launch` | `string` | `"outward"` | `outward` Explosion : Vers l’extérieur de l’émetteur.<br />`inward` Implosion : Vers le centre de l’émetteur.<br />`swirl` Tourbillon : Autour de l’émetteur.<br />`angle` Angle fixe : Toutes dans la même direction. | **Direction**<br />Direction initiale des particules. |

#### Direction

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `direction` | `number` | `-90` | min -180 ° · max 180 ° · pas de 1 | **Angle**<br />Angle de lancement des particules.<br />*Pris en compte quand `launch` = `angle` (Angle fixe).* |
| `spread` | `number` | `30` | min 0 ° · max 360 ° · pas de 1 | **Dispersion**<br />Angle de dispersion des particules autour de la direction. |

#### Vitesse

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `speed` | `number` | `120` | min 0 px/s · max 3000 px/s · pas de 1 | **Vitesse**<br />Vitesse initiale des particules. |
| `speedVariation` | `number` | `30` | min 0 % · max 100 % · pas de 1 | **Variation**<br />Variation de la vitesse des particules. |

### Forces

> Ces réglages ne comptent que quand `motion` = `true`.

#### Gravité

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `gravity` | `number` | `0` | min -3000 px/s² · max 3000 px/s² · pas de 1 | **Force**<br />Force de gravité appliquée aux particules.<br />*Pris en compte quand `emission` = `rectangle` (Rectangle) ou `disk` (Disque) ou `ring` (Anneau) ou `cone` (Cône), ou `pathMode` = `along` (Le long).* |
| `gravityAngle` | `number` | `90` | min -180 ° · max 180 ° · pas de 1 | **Direction**<br />Direction de la gravité appliquée aux particules.<br />*Pris en compte quand `emission` = `rectangle` (Rectangle) ou `disk` (Disque) ou `ring` (Anneau) ou `cone` (Cône), ou `pathMode` = `along` (Le long).* |

#### Turbulence

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `turbulence` | `number` | `0` | min 0 px · max 500 px · pas de 1 | **Amplitude**<br />Écart maximal des ondulations. |
| `turbulenceRate` | `number` | `1` | min 0 Hz · max 10 Hz · pas de 0.01 | **Fréquence**<br />Nombre d’ondulations par seconde. |

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `drag` | `number` | `0` | min 0 · max 10 · pas de 0.01 | **Frottement**<br />Coefficient de frottement appliqué aux particules.<br />*Pris en compte quand `emission` = `rectangle` (Rectangle) ou `disk` (Disque) ou `ring` (Anneau) ou `cone` (Cône), ou `pathMode` = `along` (Le long).* |

### Au fil de la vie

> Ces réglages ne comptent que quand `motion` = `true`.

#### Fondus

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `fadeIn` | `number` | `15` | min 0 % · max 100 % · pas de 1 | **Apparition**<br />Part de la vie passée à apparaître. |
| `fadeOut` | `number` | `30` | min 0 % · max 100 % · pas de 1 | **Extinction**<br />Part de la vie passée à s’éteindre. |

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `endScale` | `number` | `100` | min 0 % · max 400 % · pas de 1 | **Taille en fin de vie**<br />Taille finale des particules, en pourcentage de la taille initiale. |

#### Rotation propre

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `spin` | `number` | `0` | min -1080 °/s · max 1080 °/s · pas de 1 | **Vitesse**<br />Vitesse de rotation des particules. |
| `spinVariation` | `number` | `0` | min 0 % · max 100 % · pas de 1 | **Variation**<br />Variation de la vitesse de rotation des particules. |

### Instant

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `time` | `number` | `0` | min 0 s | **Instant rendu**<br />Moment de l'animation que l'image rend, en secondes depuis son départ. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/particles \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in-1.png \
  -F in=@in-2.png \
  -F 'params={"sprites":[{"weight":100},{"weight":30,"minSize":4,"maxSize":12,"maxOpacity":70}],"seed":1,"count":200}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in-1.png'), 'in-1.png')
form.append('in', await openAsBlob('in-2.png'), 'in-2.png')
form.append('params', JSON.stringify({"sprites":[{"weight":100},{"weight":30,"minSize":4,"maxSize":12,"maxOpacity":70}],"seed":1,"count":200}))

const res = await fetch('https://api.pixlub.com/v1/modules/particles', {
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
    "https://api.pixlub.com/v1/modules/particles",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in-1.png", "rb")), ("in", open("in-2.png", "rb"))],
    data={"params": json.dumps({"sprites": [{"weight": 100}, {"weight": 30, "minSize": 4, "maxSize": 12, "maxOpacity": 70}], "seed": 1, "count": 200})},
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
result = client.tools.run("particles", image="photo.png", params={"sprites": [{"weight": 100}, {"weight": 30, "minSize": 4, "maxSize": 12, "maxOpacity": 70}], "seed": 1, "count": 200})
result.save(f"particles{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "particles", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"sprites": []any{map[string]any{"weight": 100}, map[string]any{"weight": 30, "minSize": 4, "maxSize": 12, "maxOpacity": 70}}, "seed": 1, "count": 200},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("particles"+result.Extension(), false)
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
  "module": "particles",
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

**Exemple de ParticleSprite[]**

```json
[
  {
    "weight": 100
  },
  {
    "weight": 30,
    "minSize": 4,
    "maxSize": 12,
    "maxOpacity": 70
  }
]
```

<a name="type-path"></a>

### Path

*Objet*. Tracé de courbes de Bézier passant par des ancres, dans un cadre de référence.

| Membre | Type | Description |
| --- | --- | --- |
| `points` | `PathPoint[]` | Ancres du tracé, dans l'ordre ; au moins deux. |
| `closed` | `boolean` | *facultatif* · Relie la dernière ancre à la première. `false` par défaut. |
| `smooth` | `boolean` | *facultatif* · Arrondit le tracé entre les ancres `auto` ; `false` les relie en lignes droites. `true` par défaut. |
| `rounding` | `number` | *facultatif* · Force de l'arrondi, de 0 à 1. `0.5` par défaut. |
| `curve` | `"arc" \| "spline"` | *facultatif* · Courbure des ancres `auto` : `arc` en arcs de cercle (des ancres posées en rond donnent un cercle exact), `spline` en courbe de Catmull-Rom. `spline` par défaut. |
| `w` | `number` | *facultatif* · Largeur du cadre de référence, en pixels. Avec `h`, le tracé garde ses proportions et se centre dans l'image ; sans eux, il couvre l'image entière. |
| `h` | `number` | *facultatif* · Hauteur du cadre de référence, en pixels. |

**Exemple**

```json
{
  "points": [
    {
      "x": 0.1,
      "y": 0.7
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.9,
      "y": 0.7
    }
  ],
  "closed": false,
  "smooth": true
}
```

<a name="type-pathpoint"></a>

### PathPoint

*Objet*. Ancre d'un tracé.

| Membre | Type | Description |
| --- | --- | --- |
| `x` | `number` | Position horizontale, de 0 (gauche) à 1 (droite) du cadre. |
| `y` | `number` | Position verticale, de 0 (haut) à 1 (bas) du cadre. |
| `k` | `"auto" \| "corner" \| "free"` | *facultatif* · Type d'ancre : `auto` arrondie, `corner` angle vif, `free` poignées `i` et `o` données. `auto` par défaut. |
| `i` | `{ x, y }` | *facultatif* · Poignée d'entrée (ancre `free`), relative à l'ancre, en fraction du cadre. |
| `o` | `{ x, y }` | *facultatif* · Poignée de sortie (ancre `free`), relative à l'ancre. |
| `w` | `number` | *facultatif* · Épaisseur du trait à cette ancre, en % de l'épaisseur réglée. `100` par défaut. |

**Exemple**

```json
{
  "x": 0.5,
  "y": 0.3
}
```

<a name="type-particlesprite"></a>

### ParticleSprite

*Objet*. Part d'une image du batch dans le mélange, et ses propres bornes. Un membre omis reprend le réglage du même nom (`minSize`, `maxOpacity`…).

| Membre | Type | Description |
| --- | --- | --- |
| `weight` | `number` | *facultatif* · Poids relatif de l'image dans le mélange : la part réelle est indiquée à droite de son nom. De 0 à 100 %. `100` par défaut. |
| `minSize` | `number` | *facultatif* · Taille minimale des particules de cette image. De 1 à 1000 px. |
| `maxSize` | `number` | *facultatif* · Taille maximale des particules de cette image. De 1 à 1000 px. |
| `minOpacity` | `number` | *facultatif* · Opacité minimale des particules de cette image. De 0 à 100 %. |
| `maxOpacity` | `number` | *facultatif* · Opacité maximale des particules de cette image. De 0 à 100 %. |
| `minRotation` | `number` | *facultatif* · Rotation minimale des particules de cette image. De -360 à 360 °. |
| `maxRotation` | `number` | *facultatif* · Rotation maximale des particules de cette image. De -360 à 360 °. |

**Exemple**

```json
{
  "weight": 100
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/particles/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "seed": {
      "title": "Seed",
      "default": 1,
      "type": "number",
      "minimum": 0
    },
    "count": {
      "title": "Count",
      "default": 200,
      "type": "number",
      "minimum": 1,
      "maximum": 3000,
      "multipleOf": 1
    },
    "width": {
      "title": "Width",
      "default": 512,
      "type": "number",
      "minimum": 1,
      "maximum": 4000,
      "multipleOf": 1
    },
    "height": {
      "title": "Height",
      "default": 512,
      "type": "number",
      "minimum": 1,
      "maximum": 4000,
      "multipleOf": 1
    },
    "centerX": {
      "title": "Offset X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "centerY": {
      "title": "Offset Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "radius": {
      "title": "Radius",
      "default": 220,
      "type": "number",
      "minimum": 1,
      "maximum": 4000,
      "multipleOf": 1
    },
    "path": {
      "title": "Path",
      "default": {
        "points": [
          {
            "x": 0.12,
            "y": 0.68
          },
          {
            "x": 0.5,
            "y": 0.3
          },
          {
            "x": 0.88,
            "y": 0.66
          }
        ],
        "closed": false,
        "smooth": true,
        "rounding": 0.5,
        "curve": "arc",
        "w": 512,
        "h": 512
      },
      "type": "object",
      "required": [
        "points"
      ],
      "properties": {
        "points": {
          "type": "array",
          "items": {
            "type": "object",
            "required": [
              "x",
              "y"
            ],
            "properties": {
              "x": {
                "type": "number",
                "minimum": 0,
                "maximum": 1
              },
              "y": {
                "type": "number",
                "minimum": 0,
                "maximum": 1
              },
              "k": {
                "type": "string",
                "enum": [
                  "auto",
                  "corner",
                  "free"
                ]
              },
              "i": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "o": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "w": {
                "type": "number",
                "minimum": 0
              }
            }
          },
          "minItems": 2
        },
        "closed": {
          "type": "boolean"
        },
        "smooth": {
          "type": "boolean"
        },
        "rounding": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        },
        "curve": {
          "type": "string",
          "enum": [
            "arc",
            "spline"
          ]
        },
        "w": {
          "type": "number",
          "minimum": 1
        },
        "h": {
          "type": "number",
          "minimum": 1
        }
      }
    },
    "pathMode": {
      "title": "Mode",
      "default": "along",
      "type": "string",
      "enum": [
        "along",
        "follow"
      ]
    },
    "pathSpread": {
      "title": "Dispersion",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 1000,
      "multipleOf": 1
    },
    "pathStart": {
      "title": "Start",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "pathEnd": {
      "title": "End",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "pathLag": {
      "title": "Stagger",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "innerRadius": {
      "title": "Inner radius",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "coneDir": {
      "title": "Direction",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "coneWidth": {
      "title": "Aperture",
      "default": 60,
      "type": "number",
      "minimum": 1,
      "maximum": 360,
      "multipleOf": 1
    },
    "minSize": {
      "title": "Min",
      "default": 16,
      "type": "number",
      "minimum": 1,
      "maximum": 1000,
      "multipleOf": 1
    },
    "maxSize": {
      "title": "Max",
      "default": 48,
      "type": "number",
      "minimum": 1,
      "maximum": 1000,
      "multipleOf": 1
    },
    "minRotation": {
      "title": "Min",
      "default": 0,
      "type": "number",
      "minimum": -360,
      "maximum": 360,
      "multipleOf": 1
    },
    "maxRotation": {
      "title": "Max",
      "default": 0,
      "type": "number",
      "minimum": -360,
      "maximum": 360,
      "multipleOf": 1
    },
    "minOpacity": {
      "title": "Min",
      "default": 60,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "maxOpacity": {
      "title": "Max",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "sprites": {
      "title": "Images",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "weight": {
            "title": "Frequency",
            "default": 100,
            "type": "number",
            "minimum": 0,
            "maximum": 100,
            "multipleOf": 1
          },
          "minSize": {
            "title": "Min",
            "type": "number",
            "minimum": 1,
            "maximum": 1000,
            "multipleOf": 1
          },
          "maxSize": {
            "title": "Max",
            "type": "number",
            "minimum": 1,
            "maximum": 1000,
            "multipleOf": 1
          },
          "minOpacity": {
            "title": "Min",
            "type": "number",
            "minimum": 0,
            "maximum": 100,
            "multipleOf": 1
          },
          "maxOpacity": {
            "title": "Max",
            "type": "number",
            "minimum": 0,
            "maximum": 100,
            "multipleOf": 1
          },
          "minRotation": {
            "title": "Min",
            "type": "number",
            "minimum": -360,
            "maximum": 360,
            "multipleOf": 1
          },
          "maxRotation": {
            "title": "Max",
            "type": "number",
            "minimum": -360,
            "maximum": 360,
            "multipleOf": 1
          }
        }
      },
      "maxItems": 64
    },
    "align": {
      "title": "Orient along direction",
      "default": false,
      "type": "boolean"
    },
    "upright": {
      "title": "Keep upright",
      "default": false,
      "type": "boolean"
    },
    "trail": {
      "title": "Trail",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 1000,
      "multipleOf": 1
    },
    "falloff": {
      "title": "Falloff (distance)",
      "default": 0,
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
    "motion": {
      "title": "Animate particles",
      "default": false,
      "type": "boolean"
    },
    "spawn": {
      "title": "Spawn",
      "default": "loop",
      "type": "string",
      "enum": [
        "loop",
        "once",
        "frozen"
      ]
    },
    "lifetime": {
      "title": "Lifetime",
      "default": 2,
      "type": "number",
      "minimum": 0,
      "maximum": 20,
      "multipleOf": 0.05
    },
    "delay": {
      "title": "Delay",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 20,
      "multipleOf": 0.05
    },
    "phaseDriven": {
      "title": "Drive by phase",
      "default": false,
      "type": "boolean"
    },
    "phase": {
      "title": "Phase",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "direction": {
      "title": "Angle",
      "default": -90,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "spread": {
      "title": "Spread",
      "default": 30,
      "type": "number",
      "minimum": 0,
      "maximum": 360,
      "multipleOf": 1
    },
    "speed": {
      "title": "Speed",
      "default": 120,
      "type": "number",
      "minimum": 0,
      "maximum": 3000,
      "multipleOf": 1
    },
    "speedVariation": {
      "title": "Variation",
      "default": 30,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "gravity": {
      "title": "Strength",
      "default": 0,
      "type": "number",
      "minimum": -3000,
      "maximum": 3000,
      "multipleOf": 1
    },
    "gravityAngle": {
      "title": "Direction",
      "default": 90,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "turbulence": {
      "title": "Amplitude",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 500,
      "multipleOf": 1
    },
    "turbulenceRate": {
      "title": "Frequency",
      "default": 1,
      "type": "number",
      "minimum": 0,
      "maximum": 10,
      "multipleOf": 0.01
    },
    "drag": {
      "title": "Drag",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 10,
      "multipleOf": 0.01
    },
    "fadeIn": {
      "title": "Fade in",
      "default": 15,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "fadeOut": {
      "title": "Fade out",
      "default": 30,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "endScale": {
      "title": "End-of-life size",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 400,
      "multipleOf": 1
    },
    "spin": {
      "title": "Speed",
      "default": 0,
      "type": "number",
      "minimum": -1080,
      "maximum": 1080,
      "multipleOf": 1
    },
    "spinVariation": {
      "title": "Variation",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "time": {
      "title": "Rendered time",
      "default": 0,
      "type": "number",
      "minimum": 0
    },
    "emission": {
      "type": "string",
      "default": "disk"
    },
    "launch": {
      "type": "string",
      "default": "outward"
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
