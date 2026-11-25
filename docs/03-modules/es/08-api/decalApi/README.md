# Calcomanía

Envolver un objeto fotografiado con una imagen, siguiendo su relieve.

**Categoría** : Servicios de API · **Identificador** : `decalApi` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/decalApi)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Superficie** (obligatoria)<br />Foto del objeto cuyo relieve 3D se reconstruye. Es la única imagen que se envía al servidor. | `PNG`, `JPEG`, `WebP`, `GIF` | Un archivo |
| **Motivo** (obligatoria)<br />Imagen colocada y drapeada sobre el objeto. | `PNG`, `JPEG`, `WebP`, `GIF` | Un archivo |

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Uso

1. **Iniciar sesión**

   Nuestros servidores reconstruyen el relieve: se pide una cuenta.

2. **Importar**

   La **foto del objeto** y luego la **imagen que colocar** (un logotipo, un motivo).

3. **Ejecutar y luego colocar**

   Solo se envía la foto, una vez. Después, coloque y ajuste la imagen libremente, sin nuevos envíos.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Colocación** | Posición, tamaño, rotación y profundidad del relieve. |
| **Iluminación** | Reflejos y sombras, pliegues. |
| **Capa** | Opacidad, modo de fusión, permanecer sobre el objeto. |

## Consejos

- Mover o redimensionar la imagen colocada no cuesta nada: solo un cambio de foto vuelve a llamar al servidor.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
