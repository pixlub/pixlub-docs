# Exposición

Subir o bajar la luz de una imagen, paso a paso como una cámara de fotos.

**Categoría** : Ajuste · **Identificador** : `exposure` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/exposure)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuya exposición se corrige. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Sobreexponer y luego subexponer.](../../../../assets/modules/exposure/demo.en.webp)](../../../../assets/modules/exposure/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/exposure/demo.en.mp4) : Sobreexponer y luego subexponer.

1. `0:00` Import an image
2. `0:02` Overexpose
3. `0:06` Underexpose
4. `0:10` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Ajustar la exposición**

   Hacia la derecha la imagen se ilumina y hacia la izquierda se oscurece.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Exposición** | −10 a 10 pasos. +1 duplica la luz y −1 la reduce a la mitad. |
| **Fusión** | Modo de fusión y opacidad: cómo se aplica el ajuste sobre la imagen original. |

## Consejos

- Por encima de +2 pasos, las zonas claras se queman: baje después las altas luces en [Ajuste básico](../baseAdjust/README.md).

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
