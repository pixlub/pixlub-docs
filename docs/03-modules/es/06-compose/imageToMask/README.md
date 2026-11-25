# Imagen a máscara

Convertir una imagen en una máscara en blanco y negro, a partir de su transparencia, de un canal o de su luminosidad.

**Categoría** : Composición · **Identificador** : `imageToMask` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/imageToMask)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen convertida en máscara (mediante su alfa, un canal o su luminancia). | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Origen de la máscara, umbral, borde difuminado, inversión.](../../../../assets/modules/imageToMask/demo.en.webp)](../../../../assets/modules/imageToMask/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/imageToMask/demo.en.mp4) : Origen de la máscara, umbral, borde difuminado, inversión.

1. `0:00` Import a cut-out image
2. `0:03` Pick the mask source
3. `0:06` Threshold and feather
4. `0:12` Invert
5. `0:14` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir el origen**

   **Alfa**, **luminancia** o un canal **rojo**, **verde** o **azul**.

3. **Afinar**

   Un **umbral** para una máscara nítida, un **borde difuminado** para un borde suave.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Origen** | Alfa, luminancia, rojo, verde o azul. |
| **Umbral** | 0 a 100 %. A 0, la máscara se queda en degradado. |
| **Borde difuminado** | 0 a 100 px. |
| **Invertir** | Blanco ↔ negro. |

## Consejos

- La máscara obtenida se aplica después con [Máscara](../mask/README.md), sobre otra imagen.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
