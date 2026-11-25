# Ordenación de píxeles

Ordenar los píxeles por luminosidad en las zonas claras u oscuras, efecto glitch art.

**Categoría** : Filtros · **Identificador** : `pixelSort` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/pixelSort)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyos píxeles se ordenan por luminancia. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Umbral, dirección y zonas ordenadas.](../../../../assets/modules/pixelSort/demo.en.webp)](../../../../assets/modules/pixelSort/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/pixelSort/demo.en.mp4) : Umbral, dirección y zonas ordenadas.

1. `0:00` Import an image
2. `0:02` Threshold of sorted areas
3. `0:05` Direction and areas
4. `0:09` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Ajustar el umbral**

   Decide qué zonas se ordenan.

3. **Elegir dirección y zonas**

   Horizontal o vertical, zonas claras u oscuras.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Dirección** | Horizontal o vertical. |
| **Zonas ordenadas** | Claras u oscuras. |
| **Umbral** | 0 a 100 % de luminancia. |
| **Invertir el sentido de la ordenación** | De claro a oscuro, o al revés. |

## Consejos

- Ordenación vertical de las zonas claras sobre un cielo: chorreones de luz.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
