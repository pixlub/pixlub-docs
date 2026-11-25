# Ampliar

Agrandar la zona de la imagen sin deformar su contenido: añadir espacio alrededor.

**Categoría** : Transformación · **Identificador** : `extend` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/extend)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuya zona se amplía, sin deformar su contenido. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Tirar de un borde, introducir la ampliación, elegir el origen.](../../../../assets/modules/extend/demo.en.webp)](../../../../assets/modules/extend/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/extend/demo.en.mp4) : Tirar de un borde, introducir la ampliación, elegir el origen.

1. `0:00` Import an image
2. `0:02` Pull an edge in the preview
3. `0:05` Type the extra size
4. `0:09` Pick the origin
5. `0:15` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Añadir espacio**

   Tire de un borde de la imagen en la vista previa, o introduzca **Ancho +** y **Alto +**.

3. **Elegir el origen**

   La cuadrícula **Origen** fija dónde se queda la imagen: en el centro, el espacio se reparte alrededor.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Ancho +** / **Alto +** | Espacio añadido, en píxeles o en %. |
| **Origen** | Posición de la imagen en la nueva zona. |

La zona añadida es **transparente**: exporte en PNG o WebP para conservarla.

## Consejos

- Para un fondo de color, coloque Ampliar en el [grafo de imagen](../../../../01-app/es/02-image/01-image-graph.md) y luego fusione sobre un fondo liso.
- Para alcanzar un formato preciso (cuadrado, 16:9), use mejor el [tamaño del resultado](../../../../01-app/es/01-module-independant.md#tamano-del-resultado) en **Libre** con **Contener**.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
