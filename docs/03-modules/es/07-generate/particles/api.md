# Partículas: referencia de la API

Dispersa una imagen de origen (o una mezcla de imágenes de un lote) en partículas (forma de emisión, estelas, atenuación), controladas por una semilla

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/particles` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Imagen o lote) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen dispersada en partículas; un lote reparte sus imágenes entre las partículas.<br />Envíe una imagen, o un lote repitiendo el campo una vez por imagen: hasta 8 imágenes por llamada. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `seed` | `number` | `1` | mín. 0 | **Semilla**<br />Semilla aleatoria para generar las partículas. |
| `count` | `number` | `200` | mín. 1 · máx. 3000 · paso de 1 | **Número**<br />Número de partículas. |

### Emisión

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `emission` | `string` | `"disk"` | `rectangle` Rectángulo : Emisión en toda la superficie del rectángulo.<br />`disk` Disco : Emisión desde un centro, dentro de un radio.<br />`ring` Anillo : Emisión entre dos radios.<br />`cone` Cono : Emisión en forma de abanico orientado.<br />`path` Trazado : Emisión a lo largo de una curva. | **Forma**<br />Tipo de emisión de las partículas. |

### Dimensiones

> Estos ajustes solo cuentan cuando `emission` = `rectangle` (Rectángulo) o `path` (Trazado), o `motion` = `true`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | mín. 1 px · máx. 4000 px · paso de 1 | **Ancho**<br />Ancho de la zona de emisión. |
| `height` | `number` | `512` | mín. 1 px · máx. 4000 px · paso de 1 | **Alto**<br />Alto de la zona de emisión. |

### Centro y radio

> Estos ajustes solo cuentan cuando `emission` = `disk` (Disco) o `ring` (Anillo) o `cone` (Cono).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `centerX` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **Desplazamiento X**<br />Desplazamiento horizontal del centro de la emisión desde el medio, en % del ancho. |
| `centerY` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **Desplazamiento Y**<br />Desplazamiento vertical del centro de la emisión desde el medio, en % del alto. |
| `radius` | `number` | `220` | mín. 1 px · máx. 4000 px · paso de 1 | **Radio**<br />Radio de la emisión. |

### Trazado

> Estos ajustes solo cuentan cuando `emission` = `path` (Trazado).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `path` | [`Path`](#type-path)<br />*Trazado* | [JSON](#default-path) |  | **Trazado**<br />Trazado de la trayectoria de las partículas.<br />*Trazado* : Objeto `Path`: sus anclas `points` se colocan de 0 a 1 dentro del marco, como se detalla a continuación.<br />Estructura de Path y ejemplo : [`Path`](#type-path), [`PathPoint`](#type-pathpoint) |
| `pathMode` | `string` | `"along"` | `along` A lo largo : Las partículas nacen en cualquier punto del tramo del trazado y luego siguen su impulso.<br />`follow` Seguir : Cada partícula recorre el tramo del trazado, del inicio al final, a lo largo de su vida (animación activada). | **Modo**<br />A lo largo del camino: sembradas sobre él. Seguir el camino: lo recorren, y la duración de vida marca el tiempo del trayecto; solo se le añade la turbulencia. |
| `pathSpread` | `number` | `0` | mín. 0 px · máx. 1000 px · paso de 1 | **Dispersión**<br />Separación de las partículas a uno y otro lado del trazado: en modo Seguir, cada una conserva su carril. |

#### Tramo del trazado

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `pathStart` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 0.1 | **Inicio**<br />Inicio del tramo utilizado, en % de la longitud del trazado (inicio del trayecto en modo Seguir). |
| `pathEnd` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 0.1 | **Fin**<br />Final del tramo utilizado, en % de la longitud del trazado (final del trayecto en modo Seguir). |

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `pathLag` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 1 | **Escalonamiento**<br />Retraso elegido al azar para cada partícula, como parte del trayecto: al 0 %, un grupo nacido a la vez avanza en línea; más alto, se estira en fila como un banco.<br />*Se aplica cuando `pathMode` = `follow` (Seguir) y `motion` = `true`.* |

<a name="default-path"></a>

**Valor por defecto de `path`**

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

### Anillo

> Estos ajustes solo cuentan cuando `emission` = `ring` (Anillo).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `innerRadius` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 1 | **Radio interior**<br />Radio interior del anillo. |

### Cono

> Estos ajustes solo cuentan cuando `emission` = `cone` (Cono).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `coneDir` | `number` | `0` | mín. -180 ° · máx. 180 ° · paso de 1 | **Dirección**<br />Dirección del cono de emisión. |
| `coneWidth` | `number` | `60` | mín. 1 ° · máx. 360 ° · paso de 1 | **Apertura**<br />Apertura del cono de emisión. |

### Tamaño

> **1 archivo** : Una sola imagen en `in`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `minSize` | `number` | `16` | mín. 1 px · máx. 1000 px · paso de 1 | **Mín.**<br />Tamaño mínimo de las partículas. |
| `maxSize` | `number` | `48` | mín. 1 px · máx. 1000 px · paso de 1 | **Máx.**<br />Tamaño máximo de las partículas. |

### Rotación

> **1 archivo** : Una sola imagen en `in`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `minRotation` | `number` | `0` | mín. -360 ° · máx. 360 ° · paso de 1 | **Mín.**<br />Rotación mínima de las partículas. |
| `maxRotation` | `number` | `0` | mín. -360 ° · máx. 360 ° · paso de 1 | **Máx.**<br />Rotación máxima de las partículas. |

### Opacidad

> **1 archivo** : Una sola imagen en `in`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `minOpacity` | `number` | `60` | mín. 0 % · máx. 100 % · paso de 1 | **Mín.**<br />Opacidad mínima de las partículas. |
| `maxOpacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Máx.**<br />Opacidad máxima de las partículas. |

### Imágenes del lote

> **Varios archivos** : Varias imágenes en `in`, hasta 8: su número se deduce de los archivos enviados, usted no lo envía.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `sprites` | [`ParticleSprite[]`](#type-particlesprite)<br />*Lista de objetos* | `[]` |  | **Imágenes**<br />Lista de las imágenes usadas para las partículas.<br />*Lista de objetos* : Un elemento por cada archivo `in`, en el orden de envío; como máximo 8. Lista de objetos `ParticleSprite`, detallados a continuación; un miembro omitido conserva su valor por defecto.<br />Estructura de ParticleSprite[] y ejemplo : [`ParticleSprite`](#type-particlesprite) |

### Dirección y estela

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `align` | `boolean` | `false` |  | **Orientar según la dirección**<br />Las partículas se orientan según su dirección de desplazamiento. |
| `upright` | `boolean` | `false` |  | **Mantener derecho**<br />Una partícula que va hacia la izquierda se voltea en espejo en lugar de ponerse cabeza abajo.<br />*Se aplica cuando `align` = `true`.* |
| `trail` | `number` | `0` | mín. 0 % · máx. 1000 % · paso de 1 | **Estela**<br />Longitud de la estela de las partículas. |
| `falloff` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 1 | **Atenuación (distancia)**<br />Atenuación de la estela según la distancia. |

### Renderizado

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Modo de fusión* | `"normal"` | `normal` Normal : La capa cubre lo que está debajo.<br />`multiply` Multiplicar : Oscurece: el blanco desaparece.<br />`screen` Trama : Aclara: el negro desaparece.<br />`overlay` Superponer : Refuerza el contraste de lo que está debajo.<br />`darken` Oscurecer : Conserva el más oscuro de los dos.<br />`color-burn` Subexponer color : Oscurece saturando los colores.<br />`lighten` Aclarar : Conserva el más claro de los dos.<br />`color-dodge` Sobreexponer color : Aclara hasta el destello.<br />`soft-light` Luz suave : Contraste suave, como una luz difusa.<br />`hard-light` Luz fuerte : Contraste marcado, como un foco.<br />`difference` Diferencia : Invierte donde la capa es clara.<br />`exclusion` Exclusión : Como Diferencia, pero más suave.<br />`hue` Tono : Toma solo el tono de la capa.<br />`saturation` Saturación : Toma solo la saturación de la capa.<br />`color` Color : Toma el tono y la saturación, conserva la luminosidad.<br />`luminosity` Luminosidad : Toma solo la luminosidad de la capa. | **Modo de fusión**<br />Cómo se aplica cada partícula sobre las ya dibujadas. |

### Animación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `motion` | `boolean` | `false` |  | **Animar las partículas**<br />Activa la animación de las partículas. Si no, permanecen fijas en la fase elegida. |

### Nacimiento

> Estos ajustes solo cuentan cuando `motion` = `true`.

#### Ciclo de vida

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `spawn` | `string` | `"loop"` | `loop` Bucle : Las partículas se repiten en bucle.<br />`once` Una vez : Las partículas aparecen una sola vez.<br />`frozen` Fija : Las partículas permanecen fijas. | **Nacimiento**<br />Modo de nacimiento de las partículas. |
| `lifetime` | `number` | `2` | mín. 0 s · máx. 20 s · paso de 0.05 | **Duración de vida**<br />Duración de vida de una partícula, desde su nacimiento hasta su desaparición. |
| `delay` | `number` | `0` | mín. 0 s · máx. 20 s · paso de 0.05 | **Retraso**<br />Retraso antes del nacimiento de la primera partícula.<br />*Se aplica cuando `spawn` = `once` (Una vez).* |

#### Fase

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `phaseDriven` | `boolean` | `false` |  | **Controlar por fase**<br />Las partículas siguen su Fase, definida con fotogramas clave en la línea de tiempo (0 %: inicio, 100 %: final del ciclo). Si no, siguen su propia duración de vida.<br />*Se aplica cuando `spawn` = `loop` (Bucle), o `spawn` = `once` (Una vez).* |
| `phase` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 0.1 | **Fase**<br />Instante mostrado, de 0 % (inicio) a 100 % (final de la animación).<br />*Se aplica cuando `phaseDriven` = `true`, o `spawn` = `frozen` (Fija).* |

### Impulso

> Estos ajustes solo cuentan cuando `motion` = `true` y `emission` = `rectangle` (Rectángulo) o `disk` (Disco) o `ring` (Anillo) o `cone` (Cono), o `motion` = `true` y `pathMode` = `along` (A lo largo).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `launch` | `string` | `"outward"` | `outward` Explosión : Hacia fuera del emisor.<br />`inward` Implosión : Hacia el centro del emisor.<br />`swirl` Remolino : Alrededor del emisor.<br />`angle` Ángulo fijo : Todas en la misma dirección. | **Dirección**<br />Dirección inicial de las partículas. |

#### Dirección

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `direction` | `number` | `-90` | mín. -180 ° · máx. 180 ° · paso de 1 | **Ángulo**<br />Ángulo de lanzamiento de las partículas.<br />*Se aplica cuando `launch` = `angle` (Ángulo fijo).* |
| `spread` | `number` | `30` | mín. 0 ° · máx. 360 ° · paso de 1 | **Dispersión**<br />Ángulo de dispersión de las partículas alrededor de la dirección. |

#### Velocidad

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `speed` | `number` | `120` | mín. 0 px/s · máx. 3000 px/s · paso de 1 | **Velocidad**<br />Velocidad inicial de las partículas. |
| `speedVariation` | `number` | `30` | mín. 0 % · máx. 100 % · paso de 1 | **Variación**<br />Variación de la velocidad de las partículas. |

### Fuerzas

> Estos ajustes solo cuentan cuando `motion` = `true`.

#### Gravedad

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `gravity` | `number` | `0` | mín. -3000 px/s² · máx. 3000 px/s² · paso de 1 | **Fuerza**<br />Fuerza de gravedad aplicada a las partículas.<br />*Se aplica cuando `emission` = `rectangle` (Rectángulo) o `disk` (Disco) o `ring` (Anillo) o `cone` (Cono), o `pathMode` = `along` (A lo largo).* |
| `gravityAngle` | `number` | `90` | mín. -180 ° · máx. 180 ° · paso de 1 | **Dirección**<br />Dirección de la gravedad aplicada a las partículas.<br />*Se aplica cuando `emission` = `rectangle` (Rectángulo) o `disk` (Disco) o `ring` (Anillo) o `cone` (Cono), o `pathMode` = `along` (A lo largo).* |

#### Turbulencia

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `turbulence` | `number` | `0` | mín. 0 px · máx. 500 px · paso de 1 | **Amplitud**<br />Separación máxima de las ondulaciones. |
| `turbulenceRate` | `number` | `1` | mín. 0 Hz · máx. 10 Hz · paso de 0.01 | **Frecuencia**<br />Número de ondulaciones por segundo. |

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `drag` | `number` | `0` | mín. 0 · máx. 10 · paso de 0.01 | **Rozamiento**<br />Coeficiente de rozamiento aplicado a las partículas.<br />*Se aplica cuando `emission` = `rectangle` (Rectángulo) o `disk` (Disco) o `ring` (Anillo) o `cone` (Cono), o `pathMode` = `along` (A lo largo).* |

### A lo largo de la vida

> Estos ajustes solo cuentan cuando `motion` = `true`.

#### Fundidos

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `fadeIn` | `number` | `15` | mín. 0 % · máx. 100 % · paso de 1 | **Aparición**<br />Parte de la vida dedicada a aparecer. |
| `fadeOut` | `number` | `30` | mín. 0 % · máx. 100 % · paso de 1 | **Extinción**<br />Parte de la vida dedicada a apagarse. |

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `endScale` | `number` | `100` | mín. 0 % · máx. 400 % · paso de 1 | **Tamaño al final de la vida**<br />Tamaño final de las partículas, en porcentaje del tamaño inicial. |

#### Rotación propia

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `spin` | `number` | `0` | mín. -1080 °/s · máx. 1080 °/s · paso de 1 | **Velocidad**<br />Velocidad de rotación de las partículas. |
| `spinVariation` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 1 | **Variación**<br />Variación de la velocidad de rotación de las partículas. |

### Instante

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `time` | `number` | `0` | mín. 0 s | **Instante renderizado**<br />Momento de la animación que renderiza la imagen, en segundos desde su inicio. |

## Ejemplos

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

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

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

## Tipos

Los valores estructurados de los ajustes, detallados como clases: cada miembro con su tipo y, después, un ejemplo.

**Ejemplo de ParticleSprite[]**

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

*Objeto*. Trazado de curvas de Bézier que pasa por anclas, dentro de un marco de referencia.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `points` | `PathPoint[]` | Anclas del trazado, en orden; al menos dos. |
| `closed` | `boolean` | *opcional* · Une la última ancla con la primera. `false` por defecto. |
| `smooth` | `boolean` | *opcional* · Redondea el trazado entre las anclas `auto`; `false` las une con líneas rectas. `true` por defecto. |
| `rounding` | `number` | *opcional* · Fuerza del redondeo, de 0 a 1. `0.5` por defecto. |
| `curve` | `"arc" \| "spline"` | *opcional* · Curvatura de las anclas `auto`: `arc` en arcos de círculo (unas anclas colocadas en redondo dan un círculo exacto), `spline` en curva de Catmull-Rom. `spline` por defecto. |
| `w` | `number` | *opcional* · Ancho del marco de referencia, en píxeles. Con `h`, el trazado conserva sus proporciones y se centra en la imagen; sin ellos, cubre toda la imagen. |
| `h` | `number` | *opcional* · Alto del marco de referencia, en píxeles. |

**Ejemplo**

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

*Objeto*. Ancla de un trazado.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `x` | `number` | Posición horizontal, de 0 (izquierda) a 1 (derecha) del marco. |
| `y` | `number` | Posición vertical, de 0 (arriba) a 1 (abajo) del marco. |
| `k` | `"auto" \| "corner" \| "free"` | *opcional* · Tipo de ancla: `auto` redondeada, `corner` ángulo marcado, `free` con los tiradores `i` y `o` indicados. `auto` por defecto. |
| `i` | `{ x, y }` | *opcional* · Tirador de entrada (ancla `free`), relativo al ancla, en fracción del marco. |
| `o` | `{ x, y }` | *opcional* · Tirador de salida (ancla `free`), relativo al ancla. |
| `w` | `number` | *opcional* · Grosor del trazo en esta ancla, en % del grosor ajustado. `100` por defecto. |

**Ejemplo**

```json
{
  "x": 0.5,
  "y": 0.3
}
```

<a name="type-particlesprite"></a>

### ParticleSprite

*Objeto*. Proporción de una imagen del lote en la mezcla, y sus propios límites. Un miembro omitido toma el ajuste del mismo nombre (`minSize`, `maxOpacity`…).

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `weight` | `number` | *opcional* · Peso relativo de la imagen en la mezcla: la proporción real se indica a la derecha de su nombre. De 0 a 100 %. `100` por defecto. |
| `minSize` | `number` | *opcional* · Tamaño mínimo de las partículas de esta imagen. De 1 a 1000 px. |
| `maxSize` | `number` | *opcional* · Tamaño máximo de las partículas de esta imagen. De 1 a 1000 px. |
| `minOpacity` | `number` | *opcional* · Opacidad mínima de las partículas de esta imagen. De 0 a 100 %. |
| `maxOpacity` | `number` | *opcional* · Opacidad máxima de las partículas de esta imagen. De 0 a 100 %. |
| `minRotation` | `number` | *opcional* · Rotación mínima de las partículas de esta imagen. De -360 a 360 °. |
| `maxRotation` | `number` | *opcional* · Rotación máxima de las partículas de esta imagen. De -360 a 360 °. |

**Ejemplo**

```json
{
  "weight": 100
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

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

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
