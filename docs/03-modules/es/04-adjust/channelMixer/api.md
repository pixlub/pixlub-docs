# Mezclador de canales: referencia de la API

Recompone cada canal a partir de los demás, en el espacio elegido

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/channelMixer` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen cuyos canales se recomponen. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `space` | `string` | `"rgb"` | `rgb` RGB<br />`gray` Gris<br />`cmyk` CMYK<br />`lab` LAB | **Espacio**<br />Espacio de color en el que se ajustan los canales |

### Espacio RGB

> Estos ajustes solo cuentan cuando `space` = `rgb` (RGB).

#### Salida Rojo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `rgbRFromRgbR` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Rojo**<br />Parte del canal Rojo trasladada al canal de salida Rojo. 100 % lo copia; un valor negativo lo resta. |
| `rgbRFromRgbG` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Verde**<br />Parte del canal Verde trasladada al canal de salida Rojo. 100 % lo copia; un valor negativo lo resta. |
| `rgbRFromRgbB` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Azul**<br />Parte del canal Azul trasladada al canal de salida Rojo. 100 % lo copia; un valor negativo lo resta. |
| `rgbRFromRgbAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Rojo. 100 % lo copia; un valor negativo lo resta. |
| `offsetRgbR` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Rojo, sea cual sea la imagen. |

#### Salida Verde

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `rgbGFromRgbR` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Rojo**<br />Parte del canal Rojo trasladada al canal de salida Verde. 100 % lo copia; un valor negativo lo resta. |
| `rgbGFromRgbG` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Verde**<br />Parte del canal Verde trasladada al canal de salida Verde. 100 % lo copia; un valor negativo lo resta. |
| `rgbGFromRgbB` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Azul**<br />Parte del canal Azul trasladada al canal de salida Verde. 100 % lo copia; un valor negativo lo resta. |
| `rgbGFromRgbAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Verde. 100 % lo copia; un valor negativo lo resta. |
| `offsetRgbG` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Verde, sea cual sea la imagen. |

#### Salida Azul

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `rgbBFromRgbR` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Rojo**<br />Parte del canal Rojo trasladada al canal de salida Azul. 100 % lo copia; un valor negativo lo resta. |
| `rgbBFromRgbG` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Verde**<br />Parte del canal Verde trasladada al canal de salida Azul. 100 % lo copia; un valor negativo lo resta. |
| `rgbBFromRgbB` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Azul**<br />Parte del canal Azul trasladada al canal de salida Azul. 100 % lo copia; un valor negativo lo resta. |
| `rgbBFromRgbAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Azul. 100 % lo copia; un valor negativo lo resta. |
| `offsetRgbB` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Azul, sea cual sea la imagen. |

#### Salida Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `rgbAlphaFromRgbR` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Rojo**<br />Parte del canal Rojo trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `rgbAlphaFromRgbG` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Verde**<br />Parte del canal Verde trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `rgbAlphaFromRgbB` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Azul**<br />Parte del canal Azul trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `rgbAlphaFromRgbAlpha` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `offsetRgbAlpha` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Alfa, sea cual sea la imagen. |

### Espacio Gris

> Estos ajustes solo cuentan cuando `space` = `gray` (Gris).

#### Salida Intensidad

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `grayIFromGrayI` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Intensidad**<br />Parte del canal Intensidad trasladada al canal de salida Intensidad. 100 % lo copia; un valor negativo lo resta. |
| `grayIFromGrayAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Intensidad. 100 % lo copia; un valor negativo lo resta. |
| `offsetGrayI` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Intensidad, sea cual sea la imagen. |

#### Salida Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `grayAlphaFromGrayI` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Intensidad**<br />Parte del canal Intensidad trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `grayAlphaFromGrayAlpha` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `offsetGrayAlpha` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Alfa, sea cual sea la imagen. |

### Espacio CMYK

> Estos ajustes solo cuentan cuando `space` = `cmyk` (CMYK).

#### Salida Cian

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `cmykCFromCmykC` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Cian**<br />Parte del canal Cian trasladada al canal de salida Cian. 100 % lo copia; un valor negativo lo resta. |
| `cmykCFromCmykM` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Magenta**<br />Parte del canal Magenta trasladada al canal de salida Cian. 100 % lo copia; un valor negativo lo resta. |
| `cmykCFromCmykY` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Amarillo**<br />Parte del canal Amarillo trasladada al canal de salida Cian. 100 % lo copia; un valor negativo lo resta. |
| `cmykCFromCmykK` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Negro**<br />Parte del canal Negro trasladada al canal de salida Cian. 100 % lo copia; un valor negativo lo resta. |
| `cmykCFromCmykAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Cian. 100 % lo copia; un valor negativo lo resta. |
| `offsetCmykC` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Cian, sea cual sea la imagen. |

#### Salida Magenta

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `cmykMFromCmykC` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Cian**<br />Parte del canal Cian trasladada al canal de salida Magenta. 100 % lo copia; un valor negativo lo resta. |
| `cmykMFromCmykM` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Magenta**<br />Parte del canal Magenta trasladada al canal de salida Magenta. 100 % lo copia; un valor negativo lo resta. |
| `cmykMFromCmykY` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Amarillo**<br />Parte del canal Amarillo trasladada al canal de salida Magenta. 100 % lo copia; un valor negativo lo resta. |
| `cmykMFromCmykK` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Negro**<br />Parte del canal Negro trasladada al canal de salida Magenta. 100 % lo copia; un valor negativo lo resta. |
| `cmykMFromCmykAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Magenta. 100 % lo copia; un valor negativo lo resta. |
| `offsetCmykM` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Magenta, sea cual sea la imagen. |

#### Salida Amarillo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `cmykYFromCmykC` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Cian**<br />Parte del canal Cian trasladada al canal de salida Amarillo. 100 % lo copia; un valor negativo lo resta. |
| `cmykYFromCmykM` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Magenta**<br />Parte del canal Magenta trasladada al canal de salida Amarillo. 100 % lo copia; un valor negativo lo resta. |
| `cmykYFromCmykY` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Amarillo**<br />Parte del canal Amarillo trasladada al canal de salida Amarillo. 100 % lo copia; un valor negativo lo resta. |
| `cmykYFromCmykK` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Negro**<br />Parte del canal Negro trasladada al canal de salida Amarillo. 100 % lo copia; un valor negativo lo resta. |
| `cmykYFromCmykAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Amarillo. 100 % lo copia; un valor negativo lo resta. |
| `offsetCmykY` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Amarillo, sea cual sea la imagen. |

#### Salida Negro

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `cmykKFromCmykC` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Cian**<br />Parte del canal Cian trasladada al canal de salida Negro. 100 % lo copia; un valor negativo lo resta. |
| `cmykKFromCmykM` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Magenta**<br />Parte del canal Magenta trasladada al canal de salida Negro. 100 % lo copia; un valor negativo lo resta. |
| `cmykKFromCmykY` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Amarillo**<br />Parte del canal Amarillo trasladada al canal de salida Negro. 100 % lo copia; un valor negativo lo resta. |
| `cmykKFromCmykK` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Negro**<br />Parte del canal Negro trasladada al canal de salida Negro. 100 % lo copia; un valor negativo lo resta. |
| `cmykKFromCmykAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Negro. 100 % lo copia; un valor negativo lo resta. |
| `offsetCmykK` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Negro, sea cual sea la imagen. |

#### Salida Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `cmykAlphaFromCmykC` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Cian**<br />Parte del canal Cian trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `cmykAlphaFromCmykM` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Magenta**<br />Parte del canal Magenta trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `cmykAlphaFromCmykY` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Amarillo**<br />Parte del canal Amarillo trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `cmykAlphaFromCmykK` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Negro**<br />Parte del canal Negro trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `cmykAlphaFromCmykAlpha` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `offsetCmykAlpha` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Alfa, sea cual sea la imagen. |

### Espacio LAB

> Estos ajustes solo cuentan cuando `space` = `lab` (LAB).

#### Salida Luminosidad

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `labLFromLabL` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Luminosidad**<br />Parte del canal Luminosidad trasladada al canal de salida Luminosidad. 100 % lo copia; un valor negativo lo resta. |
| `labLFromLabA` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia A**<br />Parte del canal Crominancia A trasladada al canal de salida Luminosidad. 100 % lo copia; un valor negativo lo resta. |
| `labLFromLabB` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia B**<br />Parte del canal Crominancia B trasladada al canal de salida Luminosidad. 100 % lo copia; un valor negativo lo resta. |
| `labLFromLabAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Luminosidad. 100 % lo copia; un valor negativo lo resta. |
| `offsetLabL` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Luminosidad, sea cual sea la imagen. |

#### Salida Crominancia A

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `labAFromLabL` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Luminosidad**<br />Parte del canal Luminosidad trasladada al canal de salida Crominancia A. 100 % lo copia; un valor negativo lo resta. |
| `labAFromLabA` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia A**<br />Parte del canal Crominancia A trasladada al canal de salida Crominancia A. 100 % lo copia; un valor negativo lo resta. |
| `labAFromLabB` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia B**<br />Parte del canal Crominancia B trasladada al canal de salida Crominancia A. 100 % lo copia; un valor negativo lo resta. |
| `labAFromLabAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Crominancia A. 100 % lo copia; un valor negativo lo resta. |
| `offsetLabA` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Crominancia A, sea cual sea la imagen. |

#### Salida Crominancia B

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `labBFromLabL` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Luminosidad**<br />Parte del canal Luminosidad trasladada al canal de salida Crominancia B. 100 % lo copia; un valor negativo lo resta. |
| `labBFromLabA` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia A**<br />Parte del canal Crominancia A trasladada al canal de salida Crominancia B. 100 % lo copia; un valor negativo lo resta. |
| `labBFromLabB` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia B**<br />Parte del canal Crominancia B trasladada al canal de salida Crominancia B. 100 % lo copia; un valor negativo lo resta. |
| `labBFromLabAlpha` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Crominancia B. 100 % lo copia; un valor negativo lo resta. |
| `offsetLabB` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Crominancia B, sea cual sea la imagen. |

#### Salida Alfa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `labAlphaFromLabL` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Luminosidad**<br />Parte del canal Luminosidad trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `labAlphaFromLabA` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia A**<br />Parte del canal Crominancia A trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `labAlphaFromLabB` | `number` | `0` | mín. -200 % · máx. 200 % · paso de 1 | **Crominancia B**<br />Parte del canal Crominancia B trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `labAlphaFromLabAlpha` | `number` | `100` | mín. -200 % · máx. 200 % · paso de 1 | **Alfa**<br />Parte del canal Alfa trasladada al canal de salida Alfa. 100 % lo copia; un valor negativo lo resta. |
| `offsetLabAlpha` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento**<br />Valor añadido al canal de salida Alfa, sea cual sea la imagen. |

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
curl -X POST https://api.pixlub.com/v1/modules/channelMixer \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"space":"rgb","rgbRFromRgbR":100,"rgbRFromRgbG":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"space":"rgb","rgbRFromRgbR":100,"rgbRFromRgbG":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/channelMixer', {
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
    "https://api.pixlub.com/v1/modules/channelMixer",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0})},
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
result = client.tools.run("channelMixer", image="photo.png", params={"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0})
result.save(f"channelMixer{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "channelMixer", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("channelMixer"+result.Extension(), false)
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
  "module": "channelMixer",
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

`GET /v1/modules/channelMixer/schema`

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
    "rgbRFromRgbR": {
      "title": "Red",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbR": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbGFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbG": {
      "title": "Green",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbG": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbBFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbB": {
      "title": "Blue",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbB": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "grayIFromGrayI": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "grayIFromGrayAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetGrayI": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "grayAlphaFromGrayI": {
      "title": "Intensity",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "grayAlphaFromGrayAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetGrayAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykCFromCmykC": {
      "title": "Cyan",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykC": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykMFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykM": {
      "title": "Magenta",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykM": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykYFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykY": {
      "title": "Yellow",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykY": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykKFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykK": {
      "title": "Black",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykK": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labLFromLabL": {
      "title": "Lightness",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabL": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labAFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabA": {
      "title": "Chroma A",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabA": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labBFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabB": {
      "title": "Chroma B",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabB": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labAlphaFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
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
