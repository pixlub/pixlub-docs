# Niveles: referencia de la API

Ajusta los puntos negro y blanco, la gamma y el rango de salida, por canal

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/levels` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen cuyos niveles se ajustan. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `space` | `string` | `"rgb"` | `rgb` RGB<br />`gray` Gris<br />`cmyk` CMYK<br />`lab` LAB | **Espacio**<br />Espacio de color en el que se ajustan los canales |

### Espacio RGB

> Estos ajustes solo cuentan cuando `space` = `rgb` (RGB).

#### Maestro

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackRgbMaster` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteRgbMaster` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaRgbMaster` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackRgbMaster` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteRgbMaster` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Rojo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackRgbR` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteRgbR` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaRgbR` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackRgbR` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteRgbR` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Verde

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackRgbG` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteRgbG` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaRgbG` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackRgbG` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteRgbG` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Azul

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackRgbB` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteRgbB` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaRgbB` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackRgbB` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteRgbB` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackRgbAlpha` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteRgbAlpha` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaRgbAlpha` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackRgbAlpha` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteRgbAlpha` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

### Espacio Gris

> Estos ajustes solo cuentan cuando `space` = `gray` (Gris).

#### Maestro

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackGrayMaster` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteGrayMaster` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaGrayMaster` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackGrayMaster` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteGrayMaster` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Intensidad

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackGrayI` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteGrayI` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaGrayI` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackGrayI` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteGrayI` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackGrayAlpha` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteGrayAlpha` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaGrayAlpha` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackGrayAlpha` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteGrayAlpha` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

### Espacio CMYK

> Estos ajustes solo cuentan cuando `space` = `cmyk` (CMYK).

#### Maestro

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackCmykMaster` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteCmykMaster` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaCmykMaster` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackCmykMaster` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteCmykMaster` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Cian

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackCmykC` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteCmykC` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaCmykC` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackCmykC` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteCmykC` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Magenta

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackCmykM` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteCmykM` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaCmykM` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackCmykM` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteCmykM` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Amarillo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackCmykY` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteCmykY` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaCmykY` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackCmykY` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteCmykY` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Negro

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackCmykK` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteCmykK` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaCmykK` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackCmykK` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteCmykK` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackCmykAlpha` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteCmykAlpha` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaCmykAlpha` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackCmykAlpha` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteCmykAlpha` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

### Espacio LAB

> Estos ajustes solo cuentan cuando `space` = `lab` (LAB).

#### Maestro

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackLabMaster` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteLabMaster` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaLabMaster` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackLabMaster` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteLabMaster` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Luminosidad

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackLabL` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteLabL` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaLabL` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackLabL` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteLabL` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Crominancia A

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackLabA` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteLabA` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaLabA` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackLabA` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteLabA` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Crominancia B

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackLabB` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteLabB` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaLabB` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackLabB` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteLabB` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

#### Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blackLabAlpha` | `number` | `0` | mín. 0 · máx. 254 · paso de 1 | **Nivel de negro**<br />Todo lo que sea más oscuro se vuelve negro. Subir este punto intensifica las sombras y empasta el detalle que contienen. |
| `whiteLabAlpha` | `number` | `255` | mín. 1 · máx. 255 · paso de 1 | **Nivel de blanco**<br />Todo lo que sea más claro se vuelve blanco. Bajar este punto aclara la imagen y quema las altas luces. |
| `gammaLabAlpha` | `number` | `1` | mín. 0.1 · máx. 4 · paso de 0.05 | **Gamma**<br />Curva los tonos medios sin tocar los dos extremos. Por debajo de 1 el canal se oscurece; por encima, se aclara. |
| `outBlackLabAlpha` | `number` | `0` | mín. 0 · máx. 255 · paso de 1 | **Nivel de negro de salida**<br />Valor que toma el negro en la salida. Subirlo desvanece las sombras. |
| `outWhiteLabAlpha` | `number` | `255` | mín. 0 · máx. 255 · paso de 1 | **Nivel de blanco de salida**<br />Valor que toma el blanco en la salida. Bajarlo apaga las altas luces. |

### Fusión

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Modo de fusión* | `"normal"` | `normal` Normal : La capa cubre lo que está debajo.<br />`multiply` Multiplicar : Oscurece: el blanco desaparece.<br />`screen` Trama : Aclara: el negro desaparece.<br />`overlay` Superponer : Refuerza el contraste de lo que está debajo.<br />`darken` Oscurecer : Conserva el más oscuro de los dos.<br />`color-burn` Subexponer color : Oscurece saturando los colores.<br />`lighten` Aclarar : Conserva el más claro de los dos.<br />`color-dodge` Sobreexponer color : Aclara hasta el destello.<br />`soft-light` Luz suave : Contraste suave, como una luz difusa.<br />`hard-light` Luz fuerte : Contraste marcado, como un foco.<br />`difference` Diferencia : Invierte donde la capa es clara.<br />`exclusion` Exclusión : Como Diferencia, pero más suave.<br />`hue` Tono : Toma solo el tono de la capa.<br />`saturation` Saturación : Toma solo la saturación de la capa.<br />`color` Color : Toma el tono y la saturación, conserva la luminosidad.<br />`luminosity` Luminosidad : Toma solo la luminosidad de la capa. | **Modo de fusión**<br />Cómo se aplica el ajuste sobre la imagen original. |
| `blendOpacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad**<br />Dosis del ajuste. |

### Tamaño

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `frameMethod` | `string` | `"module"` | `module` Módulo : El módulo amplía o reduce la imagen según lo que genera.<br />`source` Origen : El resultado conserva el tamaño de la imagen recibida.<br />`custom` Libre : El resultado toma el ancho y el alto elegidos. | **Método**<br />De dónde procede el tamaño del resultado. |
| `frameWidth` | `number` |  | mín. 1 px · máx. 16384 px | **Ancho**<br />Ancho del resultado, en píxeles.<br />*Se aplica cuando `frameMethod` = `custom` (Libre).* |
| `frameHeight` | `number` |  | mín. 1 px · máx. 16384 px | **Alto**<br />Alto del resultado, en píxeles.<br />*Se aplica cuando `frameMethod` = `custom` (Libre).* |
| `frameFit` | `string` | `"none"` | `none` Ninguno (recorta) : El resultado conserva su escala y se recorta.<br />`contain` Contener : Todo el resultado cabe en el tamaño.<br />`cover` Cubrir : El resultado llena el tamaño, aunque sobresalga.<br />`stretch` Estirar : El resultado se estira hasta el tamaño, sin conservar sus proporciones. | **Ajuste**<br />Cómo se coloca el resultado en el tamaño impuesto.<br />*Se aplica cuando `frameMethod` = `source` (Origen) o `custom` (Libre).* |
| `frameAnchor` | `string`<br />*Anclaje* | `"center"` | [cuadrícula de abajo](#anchor-frameanchor) | **Anclaje**<br />Lado al que se ancla el resultado.<br />*Se aplica cuando `frameMethod` = `source` (Origen) o `custom` (Libre) y `frameFit` = `none` (Ninguno (recorta)) o `contain` (Contener) o `cover` (Cubrir).*<br />*Anclaje* : Punto de una cuadrícula de 3 × 3, desde la esquina superior izquierda hasta la esquina inferior derecha. |

<a name="anchor-frameanchor"></a>

**Posiciones de `frameAnchor`**

| | Izquierda | Centro | Derecha |
| --- | --- | --- | --- |
| **Arriba** | `top-left`<br />Arriba a la izquierda | `top`<br />Arriba | `top-right`<br />Arriba a la derecha |
| **Medio** | `left`<br />A la izquierda | **`center`**<br />**En el centro** | `right`<br />A la derecha |
| **Abajo** | `bottom-left`<br />Abajo a la izquierda | `bottom`<br />Abajo | `bottom-right`<br />Abajo a la derecha |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/levels \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"space":"rgb","blackRgbMaster":0,"whiteRgbMaster":255}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"space":"rgb","blackRgbMaster":0,"whiteRgbMaster":255}))

const res = await fetch('https://api.pixlub.com/v1/modules/levels', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/levels",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("levels", image="photo.png", params={"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255})
result.save(f"levels{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "levels", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("levels"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

### 1 archivo

> **1 archivo** : Una sola imagen en `in`.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo.<br />Una sola imagen enviada: el archivo conserva la clave `out`. |

### Varios archivos

> **Varios archivos** : Varias imágenes en `in`, hasta 64: su número se deduce de los archivos enviados, usted no lo envía.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo.<br />Varias imágenes enviadas en `in`: un archivo por imagen, con las claves `out#0`, `out#1`…, en el orden de envío. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "levels",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 1,
    "balance": 190
  }
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/levels/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "space": {
      "title": "Space",
      "default": "rgb",
      "type": "string",
      "enum": [
        "rgb",
        "gray",
        "cmyk",
        "lab"
      ]
    },
    "blackRgbMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbR": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbR": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbR": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbR": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbR": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbG": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbG": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbG": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbG": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbG": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbB": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbB": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbB": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbB": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbB": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayI": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayI": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayI": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayI": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayI": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykC": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykC": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykC": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykC": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykC": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykM": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykM": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykM": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykM": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykM": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykY": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykY": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykY": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykY": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykY": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykK": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykK": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykK": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykK": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykK": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabL": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabL": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabL": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabL": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabL": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabA": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabA": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabA": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabA": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabA": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabB": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabB": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabB": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabB": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabB": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blendMode": {
      "title": "Blend mode",
      "default": "normal",
      "type": "string",
      "enum": [
        "normal",
        "multiply",
        "screen",
        "overlay",
        "darken",
        "color-burn",
        "lighten",
        "color-dodge",
        "soft-light",
        "hard-light",
        "difference",
        "exclusion",
        "hue",
        "saturation",
        "color",
        "luminosity"
      ]
    },
    "blendOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "frameMethod": {
      "title": "Method",
      "default": "module",
      "type": "string",
      "enum": [
        "module",
        "source",
        "custom"
      ]
    },
    "frameWidth": {
      "title": "Width",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameHeight": {
      "title": "Height",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameFit": {
      "title": "Fit",
      "default": "none",
      "type": "string",
      "enum": [
        "none",
        "contain",
        "cover",
        "stretch"
      ]
    },
    "frameAnchor": {
      "title": "Anchor",
      "default": "center",
      "type": "string",
      "enum": [
        "top-left",
        "top",
        "top-right",
        "left",
        "center",
        "right",
        "bottom-left",
        "bottom",
        "bottom-right"
      ]
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
