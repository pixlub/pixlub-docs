# Mapa de degradado

Recolorear una imagen sustituyendo su luminosidad por los colores de un degradado.

**Categoría** : Ajuste · **Identificador** : `gradientMap` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/gradientMap)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuya luminancia se colorea con el degradado. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Elegir un degradado, mezclarlo, invertirlo.](../../../../assets/modules/gradientMap/demo.en.webp)](../../../../assets/modules/gradientMap/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/gradientMap/demo.en.mp4) : Elegir un degradado, mezclarlo, invertirlo.

1. `0:00` Import an image
2. `0:03` Pick a gradient
3. `0:09` Blend and invert
4. `0:16` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir el degradado**

   Abra el campo **Degradado**: tome uno de la colección o modifique sus puntos.

3. **Dosificar**

   La **mezcla** conserva una parte de la imagen original.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Degradado** | Los negros toman el color de la izquierda y los blancos, el de la derecha. |
| **Mezcla** | 0 a 100 % del efecto. |
| **Invertir la luminancia** | Los claros toman el inicio del degradado. |
| **Aplicar el alfa del degradado** | Un punto transparente del degradado vuelve transparentes los tonos correspondientes. |

## Consejos

- Un degradado de dos colores vivos da un efecto duotono.
- Para un solo color, [Recolorear](../recolor/README.md) es más sencillo.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
