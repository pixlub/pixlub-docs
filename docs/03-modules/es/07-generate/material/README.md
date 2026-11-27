# Material

Compone un material 3D: tipo de render (Estándar, sin iluminación, dibujo animado, matcap, teselación), superficie, una textura por mapa y efectos. El mismo material que en el editor 3D; para enlazar con un material del módulo «Modelo 3D».

**Categoría** : Generación · **Identificador** : `material`

## Dónde usarlo

- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Color** (opcional)<br />Color de la superficie; su transparencia recorta el material. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Normales** (opcional)<br />Mapa de normales: relieve fino sin cambiar la forma. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Rugosidad** (opcional)<br />Gris: claro = mate, oscuro = brillante. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Metal** (opcional)<br />Gris: blanco = metal, negro = no metálico. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Emisión** (opcional)<br />Lo que brilla por sí mismo, teñido por el color de emisión. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Oclusión** (opcional)<br />Sombras de contacto en los huecos. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Opacidad** (opcional)<br />Gris: blanco = opaco, negro = transparente. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Relieve** (opcional)<br />Alturas en gris: lo claro sobresale. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |

> [!NOTE]
> **Guía en preparación**
>
> Este módulo todavía no tiene una guía detallada. Sus ajustes muestran su descripción en la aplicación; la vista API enumera cada uno de ellos con sus límites.
