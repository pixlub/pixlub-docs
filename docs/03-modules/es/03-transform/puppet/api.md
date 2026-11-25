# Marioneta: referencia de la API

Deforma la imagen moviendo alfileres sobre una malla (puppet warp)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/puppet` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen**<br />Imagen deformada por los alfileres. |

## Ajustes

### Deformación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `rigidity` | `number` | `40` | mín. 0 % · máx. 100 % | **Rigidez**<br />Determina hasta qué punto el resto de la imagen sigue a los alfileres desplazados |

### Alfileres

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `pins` | [`PuppetPin[]`](#type-puppetpin)<br />*Lista de objetos* | `[]` |  | **Alfileres**<br />Alfileres clavados en la imagen y luego desplazados: la malla sigue a cada uno desde su posición inicial hasta su destino. Sin alfileres desplazados, la imagen se queda tal cual.<br />*Lista de objetos* : Lista de objetos `PuppetPin`, detallados a continuación; un miembro omitido conserva su valor por defecto.<br />Estructura de PuppetPin[] y ejemplo : [`PuppetPin`](#type-puppetpin) |

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

## Tipos

Los valores estructurados de los ajustes, detallados como clases: cada miembro con su tipo y, después, un ejemplo.

**Ejemplo de PuppetPin[]**

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

*Objeto*. Alfiler: el punto de la imagen que sujeta y, después, adónde lo lleva, de 0 a 1 dentro de la imagen.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `x0` | `number` | Inicio, horizontal: de 0 (izquierda) a 1 (derecha). De 0 a 1. |
| `y0` | `number` | Inicio, vertical: de 0 (arriba) a 1 (abajo). De 0 a 1. |
| `x1` | `number` | Destino, horizontal. De 0 a 1. |
| `y1` | `number` | Destino, vertical. Un alfiler cuyo destino es su inicio mantiene la imagen en su sitio. De 0 a 1. |

**Ejemplo**

```json
{
  "x0": 0.5,
  "y0": 0.3,
  "x1": 0.58,
  "y1": 0.22
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

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

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
