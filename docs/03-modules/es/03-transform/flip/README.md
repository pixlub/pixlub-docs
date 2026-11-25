# Espejo

Voltear una imagen horizontalmente, verticalmente o en ambos sentidos.

**Categoría** : Transformación · **Identificador** : `flip` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/flip)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen que se va a voltear. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Espejo horizontal, vertical y luego ambos.](../../../../assets/modules/flip/demo.en.webp)](../../../../assets/modules/flip/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/flip/demo.en.mp4) : Espejo horizontal, vertical y luego ambos.

1. `0:00` Import an image
2. `0:03` Horizontal mirror
3. `0:07` Vertical, or both
4. `0:12` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir el eje**

   **Horizontal** invierte la izquierda y la derecha; **Vertical**, arriba y abajo.

## Ajustes

| Eje | Efecto |
| --- | --- |
| **Horizontal** | Reflejo de izquierda a derecha (por defecto). |
| **Vertical** | Reflejo de arriba abajo. |
| **Ambos** | Equivale a media vuelta (180°). |

## Consejos

- Un selfi invertido por la cámara se corrige con un espejo horizontal.
- Un texto presente en la imagen se leerá al revés: compruébelo antes de exportar.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
