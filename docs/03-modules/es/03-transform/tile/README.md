# Desplazamiento de unión

Desplazar una imagen en bucle para comprobar y crear texturas repetibles.

**Categoría** : Transformación · **Identificador** : `tile` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/tile)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen que se va a desplazar. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Las uniones llevadas al centro y luego un desplazamiento ajustado.](../../../../assets/modules/tile/demo.en.webp)](../../../../assets/modules/tile/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/tile/demo.en.mp4) : Las uniones llevadas al centro y luego un desplazamiento ajustado.

1. `0:00` Import an image
2. `0:02` Seams in the middle
3. `0:07` Set the offset
4. `0:14` Export the result

## Uso

1. **Importar**

   Suelte la textura que comprobar.

2. **Mirar el centro**

   Al 50 %, los bordes de la imagen se juntan en el medio: una costura visible indica una textura que no se repite bien.

3. **Corregir**

   Retoque la costura en otro módulo y luego ajuste el desplazamiento para volver a la imagen original.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Desplazamiento X** | 0 a 100 % del ancho. Lo que sale por la derecha vuelve por la izquierda. |
| **Desplazamiento Y** | 0 a 100 % del alto. Lo que sale por abajo vuelve por arriba. |

## Consejos

- El 0 % o el 100 % devuelven la imagen original.
- Para un desplazamiento que no haga bucle, use [Desplazamiento](../translate/README.md).

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
