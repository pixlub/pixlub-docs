# Desplazamiento: referencia de la API

Deforma la imagen según un mapa de desplazamiento (ruido, degradado…)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/displace` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen**<br />Imagen deformada. |
| `map` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Mapa**<br />Imagen de referencia para el desplazamiento de los píxeles. |

## Ajustes

### Desplazamiento

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `amount` | `number` | `20` | mín. 0 px · máx. 500 px · paso de 1 | **Fuerza**<br />Intensidad del desplazamiento aplicado a la imagen |
| `source` | `string` | `"rg"` | `rg` R a X, G a Y : Usa el canal rojo para desplazar los píxeles en X y el canal verde para desplazarlos en Y<br />`luminance` Luminancia (X + Y) : Usa la luminancia para desplazar los píxeles en X y en Y | **Canales**<br />Elección de los canales del mapa de desplazamiento que se van a usar |

### Tamaño

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `frameMethod` | `string` | `"module"` | `module` Módulo : El módulo amplía o reduce la imagen según lo que genera.<br />`source` Origen : El resultado conserva el tamaño de la imagen recibida.<br />`custom` Libre : El resultado toma el ancho y el alto elegidos. | **Método**<br />De dónde procede el tamaño del resultado. |
| `frameWidth` | `number` |  | mín. 1 px · máx. 16384 px | **Ancho**<br />Ancho del resultado, en píxeles.<br />*Se aplica cuando `frameMethod` = `custom` (Libre).* |
| `frameHeight` | `number` |  | mín. 1 px · máx. 16384 px | **Alto**<br />Alto del resultado, en píxeles.<br />*Se aplica cuando `frameMethod` = `custom` (Libre).* |
| `frameFit` | `string` | `"none"` | `none` Ninguno (recorta) : El resultado conserva su escala y se recorta.<br />`contain` Contener : Todo el resultado cabe en el tamaño.<br />`cover` Cubrir : El resultado llena el tamaño, aunque sobresalga.<br />`stretch` Estirar : El resultado se estira hasta el tamaño, sin conservar sus proporciones. | **Ajuste**<br />Cómo se coloca el resultado en el tamaño impuesto.<br />*Se aplica cuando `frameMethod` = `source` (Origen) o `custom` (Libre).* |
| `frameAnchor` | `string`<br />*Anclaje* | `"center"` | [cuadrícula de abajo](#anchor-frameanchor) | **Anclaje**<br />Lado al que se ancla el resultado.<br />*Se aplica cuando `frameMethod` = `source` (Origen) o `custom` (Libre) y `frameFit` = `none` (Ninguno (recorta)) o `contain` (Contener) o `cover` (Cubrir).*<br />*Anclaje* : Punto de una cuadrícula de 3 × 3, desde la esquina superior izquierda hasta la esquina inferior derecha. |

<a name="anchor-frameanchor"></a>

**Posiciones de `frameAnchor`**

| | Izquierda | Centro | Derecha |
| --- | --- | --- | --- |
| **Arriba** | `top-left`<br />Arriba a la izquierda | `top`<br />Arriba | `top-right`<br />Arriba a la derecha |
| **Medio** | `left`<br />A la izquierda | **`center`**<br />**En el centro** | `right`<br />A la derecha |
| **Abajo** | `bottom-left`<br />Abajo a la izquierda | `bottom`<br />Abajo | `bottom-right`<br />Abajo a la derecha |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/displace \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F map=@map.png \
  -F 'params={"amount":20,"source":"rg"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('map', await openAsBlob('map.png'), 'map.png')
form.append('params', JSON.stringify({"amount":20,"source":"rg"}))

const res = await fetch('https://api.pixlub.com/v1/modules/displace', {
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
    "https://api.pixlub.com/v1/modules/displace",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb")), ("map", open("map.png", "rb"))],
    data={"params": json.dumps({"amount": 20, "source": "rg"})},
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
result = client.tools.run("displace", inputs={"in": "in.png", "map": "map.png"}, params={"amount": 20, "source": "rg"})
result.save(f"displace{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "displace", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "in": pixlub.FromPath("in.png"),
        "map": pixlub.FromPath("map.png"),
    },
    Params: map[string]any{"amount": 20, "source": "rg"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("displace"+result.Extension(), false)
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
  "module": "displace",
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

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/displace/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "amount": {
      "title": "Strength",
      "default": 20,
      "type": "number",
      "minimum": 0,
      "maximum": 500,
      "multipleOf": 1
    },
    "source": {
      "title": "Channels",
      "default": "rg",
      "type": "string",
      "enum": [
        "rg",
        "luminance"
      ]
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

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
