# Mezclador de canales

Recomponer cada canal de una imagen a partir de los demás.

**Categoría** : Ajuste · **Identificador** : `channelMixer` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/channelMixer)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyos canales se recomponen. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Recomponer el rojo y luego el azul.](../../../../assets/modules/channelMixer/demo.en.webp)](../../../../assets/modules/channelMixer/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/channelMixer/demo.en.mp4) : Recomponer el rojo y luego el azul.

1. `0:00` Import an image
2. `0:02` Rebuild the red
3. `0:11` Then the blue
4. `0:20` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir el canal**

   El menú **Canal** elige el que se recompone.

3. **Dosificar sus fuentes**

   Cada control deslizante indica qué parte de otro canal toma.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Espacio** | RGB, Gris, CMYK o LAB. |
| **Canal** | Canal recompuesto; todos se aplican a la vez. |
| **Fuentes** | Parte de cada canal de origen, en %. |
| **Desplazamiento** | Aclara u oscurece el canal en bloque. |
| **Fusión** | Modo de fusión y opacidad: cómo se aplica el ajuste sobre la imagen original. |

## Consejos

- Rojo tomado del azul y azul tomado del rojo: los colores se intercambian, efecto infrarrojo.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
