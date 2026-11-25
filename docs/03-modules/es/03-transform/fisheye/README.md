# Distorsión de lente

Abombar una imagen como un ojo de pez, o hundirla en cojín.

**Categoría** : Transformación · **Identificador** : `fisheye` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/fisheye)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen abombada o hundida alrededor del centro. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Abombar, hundir, colocar el centro.](../../../../assets/modules/fisheye/demo.en.webp)](../../../../assets/modules/fisheye/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/fisheye/demo.en.mp4) : Abombar, hundir, colocar el centro.

1. `0:00` Import an image
2. `0:02` Bulge the image
3. `0:07` Pinch it
4. `0:11` Place the center
5. `0:13` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Dosificar la intensidad**

   Positiva, la imagen se abomba; negativa, se hunde.

3. **Colocar el centro**

   Haga clic en la vista previa.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Intensidad** | −100 a 100 %. Positiva: abombado (ojo de pez). Negativa: hundido (cojín). |
| **Centro X** / **Y** | Posición del centro, en %. |

## Consejos

- Un valor negativo pequeño corrige el abombado de un objetivo gran angular.
- Un valor positivo alto, centrado en una cara, da un divertido efecto de lupa.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
