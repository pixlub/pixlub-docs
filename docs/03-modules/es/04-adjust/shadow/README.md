# Sombra

Proyectar una sombra, exterior o interior, a partir de la silueta de una imagen.

**Categoría** : Ajuste · **Identificador** : `shadow` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/shadow)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyo alfa proyecta la sombra. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Intensidad, desenfoque, desplazamiento y luego sombra interior.](../../../../assets/modules/shadow/demo.en.webp)](../../../../assets/modules/shadow/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/shadow/demo.en.mp4) : Intensidad, desenfoque, desplazamiento y luego sombra interior.

1. `0:00` Import a cut-out image
2. `0:02` Intensity and blur
3. `0:08` Offset the shadow
4. `0:13` Inner shadow
5. `0:15` Export the result

## Uso

1. **Importar**

   Suelte una imagen con transparencia.

2. **Ajustar la sombra**

   Intensidad, dilatación y desenfoque, y luego el desplazamiento en X y en Y.

3. **Elegir el lado**

   **Exterior**: proyectada detrás del objeto. **Interior**: hundida dentro.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Lado** | Exterior o interior. |
| **Color** | Color de la sombra. |
| **Intensidad** | 0 a 100 %. |
| **Dilatación** / **Desenfoque** | 0 a 200 px: ensancha la sombra y suaviza su borde. |
| **Desplazamiento X** / **Y** | −50 a 50 % de la imagen. Positivo: hacia la derecha, hacia abajo. |

## Consejos

- Un desenfoque amplio y un desplazamiento pequeño dan una sombra suave y realista.
- Una sombra de color sin desenfoque crea un efecto de relieve gráfico.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
