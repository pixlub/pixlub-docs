# Particles: API reference

Scatters a source image (or a mix of images from a batch) into particles (emission shape, trails, falloff), driven by a seed

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/particles` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (Image or batch) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image scattered into particles; a batch mixes its images across the particles.<br />Send one image, or a batch by repeating the field once per image: up to 8 images per call. |

## Settings

### General

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `seed` | `number` | `1` | min 0 | **Seed**<br />Random seed to generate the particles. |
| `count` | `number` | `200` | min 1 · max 3000 · step 1 | **Count**<br />Number of particles. |

### Emission

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `emission` | `string` | `"disk"` | `rectangle` Rectangle : Emits across the entire rectangle area.<br />`disk` Disc : Emits from a center, within a radius.<br />`ring` Ring : Emits between two radii.<br />`cone` Cone : Emits in the form of an oriented fan.<br />`path` Path : Emits along a curve. | **Shape**<br />Type of particle emission. |

### Dimensions

> These settings only count when `emission` = `rectangle` (Rectangle) or `path` (Path), or `motion` = `true`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | min 1 px · max 4000 px · step 1 | **Width**<br />Width of the emission area. |
| `height` | `number` | `512` | min 1 px · max 4000 px · step 1 | **Height**<br />Height of the emission area. |

### Center & radius

> These settings only count when `emission` = `disk` (Disc) or `ring` (Ring) or `cone` (Cone).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `centerX` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **Offset X**<br />Horizontal offset of the emission center from the middle, in % of the width. |
| `centerY` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **Offset Y**<br />Vertical offset of the emission center from the middle, in % of the height. |
| `radius` | `number` | `220` | min 1 px · max 4000 px · step 1 | **Radius**<br />Radius of the emission. |

### Path

> These settings only count when `emission` = `path` (Path).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `path` | [`Path`](#type-path)<br />*Path* | [JSON](#default-path) |  | **Path**<br />Tracing the trajectory of the particles.<br />*Path* : `Path` object: its `points` anchors are placed from 0 to 1 within the frame, detailed below.<br />Path structure and example : [`Path`](#type-path), [`PathPoint`](#type-pathpoint) |
| `pathMode` | `string` | `"along"` | `along` Along : Particles are born anywhere on the path portion, then follow their launch.<br />`follow` Follow : Each particle travels the path portion, from start to end, over its life (animation on). | **Mode**<br />Along the path: scattered on it. Follow the path: they travel it, the lifetime setting the trip duration; only turbulence is added. |
| `pathSpread` | `number` | `0` | min 0 px · max 1000 px · step 1 | **Dispersion**<br />Spread of the particles to either side of the path: in Follow mode, each keeps its lane. |

#### Path portion

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `pathStart` | `number` | `0` | min 0 % · max 100 % · step 0.1 | **Start**<br />Start of the portion used, in % of the path length (trip start in Follow mode). |
| `pathEnd` | `number` | `100` | min 0 % · max 100 % · step 0.1 | **End**<br />End of the portion used, in % of the path length (trip end in Follow mode). |

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `pathLag` | `number` | `0` | min 0 % · max 100 % · step 1 | **Stagger**<br />Delay drawn for each particle, as a share of the trip: at 0%, a group born together moves in a line; higher, it stretches out like a school.<br />*Applies when `pathMode` = `follow` (Follow) and `motion` = `true`.* |

<a name="default-path"></a>

**Default value of `path`**

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

### Ring

> These settings only count when `emission` = `ring` (Ring).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `innerRadius` | `number` | `0` | min 0 % · max 100 % · step 1 | **Inner radius**<br />Inner radius of the ring. |

### Cone

> These settings only count when `emission` = `cone` (Cone).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `coneDir` | `number` | `0` | min -180 ° · max 180 ° · step 1 | **Direction**<br />Direction of the emission cone. |
| `coneWidth` | `number` | `60` | min 1 ° · max 360 ° · step 1 | **Aperture**<br />Aperture of the emission cone. |

### Size

> **1 file** : A single image in `in`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `minSize` | `number` | `16` | min 1 px · max 1000 px · step 1 | **Min**<br />Minimum size of the particles. |
| `maxSize` | `number` | `48` | min 1 px · max 1000 px · step 1 | **Max**<br />Maximum size of the particles. |

### Rotation

> **1 file** : A single image in `in`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `minRotation` | `number` | `0` | min -360 ° · max 360 ° · step 1 | **Min**<br />Minimum rotation of the particles. |
| `maxRotation` | `number` | `0` | min -360 ° · max 360 ° · step 1 | **Max**<br />Maximum rotation of the particles. |

### Opacity

> **1 file** : A single image in `in`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `minOpacity` | `number` | `60` | min 0 % · max 100 % · step 1 | **Min**<br />Minimum opacity of the particles. |
| `maxOpacity` | `number` | `100` | min 0 % · max 100 % · step 1 | **Max**<br />Maximum opacity of the particles. |

### Batch images

> **Several files** : Several images in `in`, up to 8: their number comes from the files sent, you do not send it.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `sprites` | [`ParticleSprite[]`](#type-particlesprite)<br />*List of objects* | `[]` |  | **Images**<br />List of images used for the particles.<br />*List of objects* : One item per `in` file, in upload order; 8 at most. List of `ParticleSprite` objects, detailed below; an omitted member keeps its default value.<br />ParticleSprite[] structure and example : [`ParticleSprite`](#type-particlesprite) |

### Direction & trail

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `align` | `boolean` | `false` |  | **Orient along direction**<br />Particles are oriented along their direction of movement. |
| `upright` | `boolean` | `false` |  | **Keep upright**<br />A particle heading left is mirrored rather than turned upside down.<br />*Applies when `align` = `true`.* |
| `trail` | `number` | `0` | min 0 % · max 1000 % · step 1 | **Trail**<br />Length of the particle trail. |
| `falloff` | `number` | `0` | min 0 % · max 100 % · step 1 | **Falloff (distance)**<br />Falloff of the trail according to distance. |

### Rendering

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Blend mode* | `"normal"` | `normal` Normal : The layer simply covers what is below.<br />`multiply` Multiply : Darkens: white disappears.<br />`screen` Screen : Lightens: black disappears.<br />`overlay` Overlay : Boosts the contrast below.<br />`darken` Darken : Keeps the darker of the two.<br />`color-burn` Color burn : Darkens and deepens colors.<br />`lighten` Lighten : Keeps the lighter of the two.<br />`color-dodge` Color dodge : Brightens up to a glow.<br />`soft-light` Soft light : Gentle contrast, like diffused light.<br />`hard-light` Hard light : Strong contrast, like a spotlight.<br />`difference` Difference : Inverts where the layer is bright.<br />`exclusion` Exclusion : Like Difference, but softer.<br />`hue` Hue : Takes only the layer's hue.<br />`saturation` Saturation : Takes only the layer's saturation.<br />`color` Color : Takes hue and saturation, keeps the lightness.<br />`luminosity` Luminosity : Takes only the layer's lightness. | **Blend mode**<br />How each particle sits on the ones already drawn. |

### Animation

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `motion` | `boolean` | `false` |  | **Animate particles**<br />Enables particle animation. Otherwise, they remain frozen at the chosen phase. |

### Spawn

> These settings only count when `motion` = `true`.

#### Life cycle

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `spawn` | `string` | `"loop"` | `loop` Loop : Particles repeat in a loop.<br />`once` Once : Particles appear only once.<br />`frozen` Frozen : Particles remain frozen. | **Spawn**<br />Mode of particle spawn. |
| `lifetime` | `number` | `2` | min 0 s · max 20 s · step 0.05 | **Lifetime**<br />Lifetime of a particle, from its birth to its disappearance. |
| `delay` | `number` | `0` | min 0 s · max 20 s · step 0.05 | **Delay**<br />Delay before the first particle spawns.<br />*Applies when `spawn` = `once` (Once).* |

#### Phase

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `phaseDriven` | `boolean` | `false` |  | **Drive by phase**<br />Particles follow their Phase, keyed on the timeline (0%: start, 100%: end of the cycle). Otherwise, they follow their own lifetime.<br />*Applies when `spawn` = `loop` (Loop), or `spawn` = `once` (Once).* |
| `phase` | `number` | `50` | min 0 % · max 100 % · step 0.1 | **Phase**<br />Instant shown, from 0% (start) to 100% (end of the animation).<br />*Applies when `phaseDriven` = `true`, or `spawn` = `frozen` (Frozen).* |

### Launch

> These settings only count when `motion` = `true` and `emission` = `rectangle` (Rectangle) or `disk` (Disc) or `ring` (Ring) or `cone` (Cone), or `motion` = `true` and `pathMode` = `along` (Along).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `launch` | `string` | `"outward"` | `outward` Explode : Away from the emitter.<br />`inward` Implode : Toward the center of the emitter.<br />`swirl` Swirl : Around the emitter.<br />`angle` Fixed angle : All in the same direction. | **Direction**<br />Initial direction of the particles. |

#### Direction

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `direction` | `number` | `-90` | min -180 ° · max 180 ° · step 1 | **Angle**<br />Launch angle of the particles.<br />*Applies when `launch` = `angle` (Fixed angle).* |
| `spread` | `number` | `30` | min 0 ° · max 360 ° · step 1 | **Spread**<br />Spread angle of the particles around the direction. |

#### Speed

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `speed` | `number` | `120` | min 0 px/s · max 3000 px/s · step 1 | **Speed**<br />Initial speed of the particles. |
| `speedVariation` | `number` | `30` | min 0 % · max 100 % · step 1 | **Variation**<br />Variation of the speed of the particles. |

### Forces

> These settings only count when `motion` = `true`.

#### Gravity

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `gravity` | `number` | `0` | min -3000 px/s² · max 3000 px/s² · step 1 | **Strength**<br />Gravity force applied to the particles.<br />*Applies when `emission` = `rectangle` (Rectangle) or `disk` (Disc) or `ring` (Ring) or `cone` (Cone), or `pathMode` = `along` (Along).* |
| `gravityAngle` | `number` | `90` | min -180 ° · max 180 ° · step 1 | **Direction**<br />Direction of the gravity applied to the particles.<br />*Applies when `emission` = `rectangle` (Rectangle) or `disk` (Disc) or `ring` (Ring) or `cone` (Cone), or `pathMode` = `along` (Along).* |

#### Turbulence

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `turbulence` | `number` | `0` | min 0 px · max 500 px · step 1 | **Amplitude**<br />Largest wiggle offset. |
| `turbulenceRate` | `number` | `1` | min 0 Hz · max 10 Hz · step 0.01 | **Frequency**<br />Wiggles per second. |

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `drag` | `number` | `0` | min 0 · max 10 · step 0.01 | **Drag**<br />Drag coefficient applied to the particles.<br />*Applies when `emission` = `rectangle` (Rectangle) or `disk` (Disc) or `ring` (Ring) or `cone` (Cone), or `pathMode` = `along` (Along).* |

### Over lifetime

> These settings only count when `motion` = `true`.

#### Fades

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `fadeIn` | `number` | `15` | min 0 % · max 100 % · step 1 | **Fade in**<br />Share of the lifetime spent fading in. |
| `fadeOut` | `number` | `30` | min 0 % · max 100 % · step 1 | **Fade out**<br />Share of the lifetime spent fading out. |

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `endScale` | `number` | `100` | min 0 % · max 400 % · step 1 | **End-of-life size**<br />Final size of the particles, as a percentage of the initial size. |

#### Spin

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `spin` | `number` | `0` | min -1080 °/s · max 1080 °/s · step 1 | **Speed**<br />Rotation speed of the particles. |
| `spinVariation` | `number` | `0` | min 0 % · max 100 % · step 1 | **Variation**<br />Variation of the rotation speed of the particles. |

### Time

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `time` | `number` | `0` | min 0 s | **Rendered time**<br />Moment of the animation the image renders, in seconds from its start. |

## Examples

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

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produced by the module. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

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

The structured values of the settings, detailed like classes: each member with its type, then an example.

**ParticleSprite[] example**

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

*Object*. Bézier path running through anchors, inside a reference frame.

| Member | Type | Description |
| --- | --- | --- |
| `points` | `PathPoint[]` | Anchors of the path, in order; at least two. |
| `closed` | `boolean` | *optional* · Joins the last anchor to the first. `false` by default. |
| `smooth` | `boolean` | *optional* · Rounds the path between `auto` anchors; `false` joins them with straight lines. `true` by default. |
| `rounding` | `number` | *optional* · Rounding strength, from 0 to 1. `0.5` by default. |
| `curve` | `"arc" \| "spline"` | *optional* · Curvature of `auto` anchors: `arc` as circular arcs (anchors placed in a ring give an exact circle), `spline` as a Catmull-Rom curve. `spline` by default. |
| `w` | `number` | *optional* · Width of the reference frame, in pixels. With `h`, the path keeps its proportions and is centered in the image; without them, it spans the whole image. |
| `h` | `number` | *optional* · Height of the reference frame, in pixels. |

**Example**

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

*Object*. Anchor of a path.

| Member | Type | Description |
| --- | --- | --- |
| `x` | `number` | Horizontal position, from 0 (left) to 1 (right) of the frame. |
| `y` | `number` | Vertical position, from 0 (top) to 1 (bottom) of the frame. |
| `k` | `"auto" \| "corner" \| "free"` | *optional* · Anchor type: `auto` rounded, `corner` sharp angle, `free` with the given `i` and `o` handles. `auto` by default. |
| `i` | `{ x, y }` | *optional* · Incoming handle (`free` anchor), relative to the anchor, as a fraction of the frame. |
| `o` | `{ x, y }` | *optional* · Outgoing handle (`free` anchor), relative to the anchor. |
| `w` | `number` | *optional* · Stroke width at this anchor, in % of the set width. `100` by default. |

**Example**

```json
{
  "x": 0.5,
  "y": 0.3
}
```

<a name="type-particlesprite"></a>

### ParticleSprite

*Object*. Share of one batch image in the mix, and its own bounds. An omitted member takes the setting of the same name (`minSize`, `maxOpacity`…).

| Member | Type | Description |
| --- | --- | --- |
| `weight` | `number` | *optional* · Relative weight of the image in the mix: the actual share is shown next to its name. From 0 to 100 %. `100` by default. |
| `minSize` | `number` | *optional* · Minimum size of this image's particles. From 1 to 1000 px. |
| `maxSize` | `number` | *optional* · Maximum size of this image's particles. From 1 to 1000 px. |
| `minOpacity` | `number` | *optional* · Minimum opacity of this image's particles. From 0 to 100 %. |
| `maxOpacity` | `number` | *optional* · Maximum opacity of this image's particles. From 0 to 100 %. |
| `minRotation` | `number` | *optional* · Minimum rotation of this image's particles. From -360 to 360 °. |
| `maxRotation` | `number` | *optional* · Maximum rotation of this image's particles. From -360 to 360 °. |

**Example**

```json
{
  "weight": 100
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

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

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
