# Bloom

Hacer que las zonas luminosas de una imagen se difundan en un halo.

**Categoría** : Filtros · **Identificador** : `bloom` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/bloom)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyas zonas luminosas difunden un halo. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Umbral, difusión e intensidad.](../../../../assets/modules/bloom/demo.en.webp)](../../../../assets/modules/bloom/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/bloom/demo.en.mp4) : Umbral, difusión e intensidad.

1. `0:00` Import an image
2. `0:02` Threshold of bright areas
3. `0:06` Diffusion and intensity
4. `0:12` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir el umbral**

   Solo irradian las zonas más claras.

3. **Dosificar el halo**

   **Difusión** para su tamaño e **intensidad** para su fuerza.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Umbral** | 0 a 100 % de luminosidad. |
| **Difusión** | 0 a 300 px. |
| **Intensidad** | 0 a 400 %. |

## Consejos

- Ideal sobre neones o luces nocturnas; sobre un cielo claro, suba el umbral.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
