# Reducción de ruido

Reducir el ruido de una imagen conservando sus contornos.

**Categoría** : Filtros · **Identificador** : `denoise` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/denoise)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyo ruido se reduce. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Radio del filtro y luego mezcla con el original.](../../../../assets/modules/denoise/demo.en.webp)](../../../../assets/modules/denoise/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/denoise/demo.en.mp4) : Radio del filtro y luego mezcla con el original.

1. `0:00` Import an image
2. `0:04` Filter radius
3. `0:08` Mix with the original
4. `0:12` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes. Haga zoom para ver el grano.

2. **Ajustar**

   El **radio** fija la fuerza del suavizado y la **intensidad**, la mezcla con el original.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Radio** | 1 a 3 px. |
| **Intensidad** | 0 a 100 %: proporción de la imagen sin ruido. |

## Consejos

- Un radio alto también borra los detalles finos: baje la intensidad para conservar un aspecto natural.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
