# Código QR: referencia de la API

Genera un código QR legible por cualquier lector (enlace, wifi, contacto…), con estilo, con logotipo o fundido en una imagen

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/qrcode` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `logo` (Una sola imagen) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Logotipo**<br />Imagen opcional colocada en el centro del código QR; en automático, la corrección sube a H. |
| `image` (Una sola imagen) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen**<br />Imagen opcional convertida en motivo de código QR, en la que se funde el código QR (modo «En una imagen»); su transparencia da la silueta. |

## Ajustes

### Contenido

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `contentType` | `string` | `"url"` | `url` Enlace : Dirección web; si falta, se añade `https://`.<br />`text` Texto : Texto libre.<br />`wifi` Wi-Fi : Conexión a una red wifi con un escaneo.<br />`email` Correo electrónico : Prepara un correo electrónico: destinatario, asunto, mensaje.<br />`tel` Teléfono : Llama a un número.<br />`sms` SMS : Prepara un SMS.<br />`vcard` Contacto (vCard) : Ficha de contacto para guardar.<br />`geo` Ubicación : Abre un punto en el mapa. | **Tipo**<br />Lo que contiene el código QR; cada tipo sigue el formato que leen los lectores habituales. |
| `url` | `string` | `"https://pixlub.com"` |  | **Enlace**<br />Dirección que se abre al escanear.<br />*Se aplica cuando `contentType` = `url` (Enlace).* |
| `text` | `string` | *cadena vacía* |  | **Texto**<br />Texto incluido tal cual.<br />*Se aplica cuando `contentType` = `text` (Texto).* |
| `wifiSsid` | `string` | *cadena vacía* |  | **Nombre de la red (SSID)**<br />Nombre de la red wifi.<br />*Se aplica cuando `contentType` = `wifi` (Wi-Fi).* |
| `wifiSecurity` | `string` | `"WPA"` | `WPA` WPA/WPA2/WPA3<br />`WEP` WEP<br />`none` Ninguno | **Seguridad**<br />Cifrado de la red.<br />*Se aplica cuando `contentType` = `wifi` (Wi-Fi).* |
| `wifiPassword` | `string` | *cadena vacía* |  | **Contraseña**<br />Contraseña de la red, escrita sin cifrar en el código QR.<br />*Se aplica cuando `contentType` = `wifi` (Wi-Fi) y `wifiSecurity` = `WPA` (WPA/WPA2/WPA3) o `WEP` (WEP).* |
| `wifiHidden` | `boolean` | `false` |  | **Red oculta**<br />La red no difunde su nombre.<br />*Se aplica cuando `contentType` = `wifi` (Wi-Fi).* |
| `vcardFirstName` | `string` | *cadena vacía* |  | **Nombre**<br />Nombre del contacto.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `vcardLastName` | `string` | *cadena vacía* |  | **Apellidos**<br />Apellidos del contacto.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `vcardOrg` | `string` | *cadena vacía* |  | **Organización**<br />Empresa u organización.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `vcardTitle` | `string` | *cadena vacía* |  | **Cargo**<br />Puesto que ocupa.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `emailTo` | `string` | *cadena vacía* |  | **Correo electrónico**<br />Dirección de correo electrónico.<br />*Se aplica cuando `contentType` = `email` (Correo electrónico) o `vcard` (Contacto (vCard)).* |
| `phone` | `string` | *cadena vacía* |  | **Teléfono**<br />Número, preferiblemente en formato internacional (+…).<br />*Se aplica cuando `contentType` = `tel` (Teléfono) o `sms` (SMS) o `vcard` (Contacto (vCard)).* |
| `emailSubject` | `string` | *cadena vacía* |  | **Asunto**<br />Asunto del correo electrónico.<br />*Se aplica cuando `contentType` = `email` (Correo electrónico).* |
| `emailBody` | `string` | *cadena vacía* |  | **Mensaje**<br />Cuerpo del correo electrónico.<br />*Se aplica cuando `contentType` = `email` (Correo electrónico).* |
| `smsMessage` | `string` | *cadena vacía* |  | **Mensaje**<br />Texto del SMS.<br />*Se aplica cuando `contentType` = `sms` (SMS).* |
| `vcardUrl` | `string` | *cadena vacía* |  | **Sitio web**<br />Sitio web del contacto.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `vcardStreet` | `string` | *cadena vacía* |  | **Dirección**<br />Calle y número.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `vcardZip` | `string` | *cadena vacía* |  | **Código postal**<br />Código postal.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `vcardCity` | `string` | *cadena vacía* |  | **Ciudad**<br />Ciudad.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `vcardCountry` | `string` | *cadena vacía* |  | **País**<br />País.<br />*Se aplica cuando `contentType` = `vcard` (Contacto (vCard)).* |
| `geoLat` | `number` | `48.8584` | mín. -90 ° · máx. 90 ° | **Latitud**<br />Latitud en grados decimales.<br />*Se aplica cuando `contentType` = `geo` (Ubicación).* |
| `geoLng` | `number` | `2.2945` | mín. -180 ° · máx. 180 ° | **Longitud**<br />Longitud en grados decimales.<br />*Se aplica cuando `contentType` = `geo` (Ubicación).* |

### Integración

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `mode` | `string` | `"standard"` | `standard` Estándar : Código QR solo, sobre su fondo.<br />`shape` En una forma : El código QR rellena una silueta (campana, corazón… o la de la imagen conectada), prolongado por módulos del mismo diseño y rodeado por un contorno.<br />`image` En una imagen : La imagen conectada se convierte en un motivo de módulos, con sus tonos y sus colores, y el código QR se funde en ella. | **Modo**<br />En una forma: silueta blanca contorneada, rellena de módulos como el código QR. En una imagen: conecte una imagen a la entrada Imagen; sus tonos se convierten en el motivo. |

### Silueta

> Estos ajustes solo cuentan cuando `mode` = `shape` (En una forma).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"cloche"` | `cloche` Campana<br />`circle` Círculo<br />`roundedSquare` Cuadrado redondeado<br />`heart` Corazón<br />`star` Estrella<br />`diamond` Rombo<br />`hexagon` Hexágono<br />`shield` Escudo<br />`house` Casa<br />`cloud` Nube<br />`bubble` Bocadillo<br />`pin` Marcador<br />`drop` Gota<br />`leaf` Hoja<br />`cup` Taza<br />`tshirt` Camiseta<br />`gift` Regalo<br />`bag` Bolsa<br />`cat` Gato<br />`paw` Pata<br />`image` Desde la imagen : Silueta de la imagen conectada a la entrada Imagen. | **Forma**<br />Silueta que rellena el código QR. «Desde la imagen» toma la de la imagen conectada: su transparencia o su contorno, si es un dibujo de líneas. |
| `outlineWidth` | `number` | `0.8` | mín. 0 · máx. 6 · paso de 0.1 | **Grosor del contorno**<br />Grosor del borde alrededor de la silueta, en módulos; 0 lo quita. |
| `outlineCustom` | `boolean` | `false` |  | **Color propio del contorno**<br />Si no, el contorno toma el color (o el degradado) de los módulos. |
| `outlineColor` | `Color`<br />*Color sólido* | `"#1c2535"` |  | **Color del contorno**<br />Color del contorno.<br />*Se aplica cuando `outlineCustom` = `true`.*<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |
| `patternDensity` | `number` | `50` | mín. 20 % · máx. 80 % · paso de 1 | **Densidad del motivo**<br />Proporción de módulos oscuros alrededor del código QR; 50 % imita los datos de un código QR. |

### Colocación

> Estos ajustes solo cuentan cuando `mode` = `image` (En una imagen) o `shape` (En una forma).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `qrSize` | `number` | `85` | mín. 20 % · máx. 150 % · paso de 1 | **Tamaño del código QR**<br />Proporción del mayor cuadrado que cabe en la forma; los módulos del motivo la siguen.<br />*Se aplica cuando `mode` = `shape` (En una forma).* |
| `cellSize` | `number` | `12` | mín. 3 px · máx. 64 px · paso de 1 | **Tamaño de los módulos**<br />Lado de un módulo en píxeles de la imagen: fija la finura del motivo y el tamaño del código QR.<br />*Se aplica cuando `mode` = `image` (En una imagen).* |
| `qrX` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 0.1 | **Posición X**<br />En una imagen: centro del código QR, como proporción del ancho. En una forma: desplazamiento desde su posición automática (50 % = en el centro de la forma). Siempre se ajusta a la cuadrícula. |
| `qrY` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 0.1 | **Posición Y**<br />Como la posición X, a lo alto. |
| `halo` | `number` | `0` | mín. 0 · máx. 6 · paso de 1 | **Halo**<br />Módulos claros alrededor del código QR. A 0, el código QR se funde en el motivo sin borde. |
| `seed` | `number` | `1` | mín. 0 · máx. 9999 | **Variante**<br />Cambia la tirada del motivo.<br />*Se aplica cuando `mode` = `shape` (En una forma), o `mode` = `image` (En una imagen) y `convert` = `qr` (Motivo QR).* |
| `finderGuard` | `boolean` | `true` |  | **Despejar los ojos**<br />Un ribete claro de un módulo alrededor de los tres ojos, del lado de la imagen: es lo que necesitan los lectores para encontrar el código; el resto del borde sigue fundido. |

### Conversión

> Estos ajustes solo cuentan cuando `mode` = `image` (En una imagen).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `convert` | `string` | `"qr"` | `qr` Motivo QR : Textura aleatoria como los datos de un código QR, más densa en los tonos oscuros: el código QR se funde en ella.<br />`threshold` Umbral : Tonos planos nítidos: logotipos, siluetas.<br />`dither` Difusión : Reproduce los degradados y las fotos.<br />`ordered` Trama : Trama regular (Bayer). | **Método**<br />Cómo se convierten los tonos de la imagen en módulos oscuros o claros. |
| `tone` | `number` | `70` | mín. 0 % · máx. 100 % · paso de 1 | **Relieve de los tonos**<br />A 0, densidad igual en todas partes (solo la silueta, aspecto QR puro); más alto, los tonos de la imagen se aprecian en la densidad.<br />*Se aplica cuando `convert` = `qr` (Motivo QR).* |
| `threshold` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 1 | **Umbral**<br />Más alto, más módulos oscuros. |
| `contrast` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Contraste**<br />Contraste de la imagen antes de la conversión. |
| `invertImage` | `boolean` | `false` |  | **Invertir**<br />Las zonas claras se vuelven oscuras. |
| `silhouette` | `boolean` | `true` |  | **Seguir la silueta**<br />Fuera de las zonas opacas de la imagen, no se dibuja nada. |
| `outline` | `boolean` | `true` |  | **Contorno**<br />El borde de la silueta se traza con una línea de módulos.<br />*Se aplica cuando `silhouette` = `true`.* |
| `colorSource` | `string` | `"qr"` | `qr` Del código QR<br />`image` De la imagen | **Color de los módulos**<br />Color de todos los módulos, incluidos el motivo y el código QR: el del código QR o el de la imagen bajo cada módulo, oscurecido para seguir siendo legible. |

### Fusión

> Estos ajustes solo cuentan cuando `mode` = `image` (En una imagen).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `halftone` | `boolean` | `false` |  | **Imagen a través del QR**<br />Cada módulo se divide en 3 × 3: el centro lleva el dato y el resto muestra la imagen; todo el motivo pasa a este grano. |
| `halftoneStrength` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 1 | **Fuerza del QR**<br />Parte de cada módulo devuelta al código QR alrededor de su centro: cuanto más alta, más legible.<br />*Se aplica cuando `halftone` = `true`.* |
| `qrSolidBg` | `boolean` | `true` |  | **Fondo sólido bajo el QR**<br />El código QR y su halo conservan un fondo opaco, aunque el resto sea transparente. |
| `backdropOpacity` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 1 | **Imagen original**<br />Muestra la imagen original bajo el motivo; en ese caso, baje la opacidad del fondo. |

### Módulos

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `moduleShape` | `string` | `"square"` | `square` Cuadrados<br />`rounded` Fluido<br />`dots` Puntos<br />`squircle` Cuadrados redondeados<br />`diamond` Rombos<br />`star` Estrellas<br />`cross` Cruces<br />`heart` Corazones<br />`leaf` Hojas<br />`vbars` Barras verticales<br />`hbars` Barras horizontales<br />`random` Confeti | **Forma**<br />Forma de cada módulo (y de los módulos de la imagen en modo integrado). |
| `moduleScale` | `number` | `100` | mín. 40 % · máx. 100 % · paso de 1 | **Tamaño**<br />Tamaño del módulo en su celda; por debajo del 70 %, la lectura se vuelve más frágil.<br />*Se aplica cuando `moduleShape` = `square` (Cuadrados) o `dots` (Puntos) o `squircle` (Cuadrados redondeados) o `diamond` (Rombos) o `star` (Estrellas) o `cross` (Cruces) o `heart` (Corazones) o `leaf` (Hojas) o `vbars` (Barras verticales) o `hbars` (Barras horizontales) o `random` (Confeti).* |
| `roundness` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 1 | **Redondeo**<br />Redondez de las esquinas.<br />*Se aplica cuando `moduleShape` = `rounded` (Fluido) o `squircle` (Cuadrados redondeados) o `leaf` (Hojas) o `vbars` (Barras verticales) o `hbars` (Barras horizontales).* |

### Ojos

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `eyeFrame` | `string` | `"square"` | `square` Cuadrado<br />`rounded` Redondeado<br />`circle` Círculo<br />`leaf` Hoja<br />`shape` Como los módulos | **Marco**<br />Forma del marco de los tres ojos de localización y de los pequeños motivos de alineación. «Como los módulos» con formas sueltas (puntos…) dificulta la lectura. |
| `eyeBall` | `string` | `"square"` | `square` Cuadrado<br />`rounded` Redondeado<br />`circle` Redondo<br />`diamond` Rombo<br />`leaf` Hoja<br />`star` Estrella<br />`shape` Como los módulos | **Centro**<br />Forma del centro de los ojos. Para la lectura más segura, mantenga la misma familia que el marco: cuadrado o redondeado con un marco cuadrado o redondeado, redondo o rombo con un marco redondo. |
| `eyeCustom` | `boolean` | `false` |  | **Colores propios**<br />Da a los ojos sus propios colores. |
| `eyeFrameColor` | `Color`<br />*Color sólido* | `"#1c2535"` |  | **Color del marco**<br />Color del marco de los ojos.<br />*Se aplica cuando `eyeCustom` = `true`.*<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |
| `eyeBallColor` | `Color`<br />*Color sólido* | `"#1c2535"` |  | **Color del centro**<br />Color del centro de los ojos.<br />*Se aplica cuando `eyeCustom` = `true`.*<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |

### Colores

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Color o degradado* | `"#000000"` |  | **Módulos**<br />Color o degradado de los módulos; manténgalo claramente más oscuro que el fondo.<br />*Color o degradado* : Un color CSS (`"#ff8800"`) para un relleno plano, o un objeto `ColorGradient` para un degradado.<br />Estructura de Color \| ColorGradient y ejemplo : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `fgOpacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad de los módulos**<br />Transparencia de los módulos. |
| `background` | `Color`<br />*Color sólido* | `"#ffffff"` |  | **Fondo**<br />Color del fondo (celdas claras).<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |
| `bgOpacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad del fondo**<br />Al 0 %, el fondo es transparente. |
| `bgRadius` | `number` | `0` | mín. 0 % · máx. 50 % · paso de 1 | **Esquinas del fondo**<br />Redondeo de las esquinas del fondo.<br />*Se aplica cuando `mode` = `standard` (Estándar).* |

### Dimensiones

> Estos ajustes solo cuentan cuando `mode` = `standard` (Estándar) o `shape` (En una forma).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `size` | `number` | `1024` | mín. 64 px · máx. 4096 px · paso de 1 | **Tamaño**<br />Lado de la imagen, margen incluido. |
| `margin` | `number` | `4` | mín. 0 · máx. 20 · paso de 1 | **Margen (módulos)**<br />Zona clara alrededor del código; la norma exige 4 módulos.<br />*Se aplica cuando `mode` = `standard` (Estándar).* |

### Logotipo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `logoSize` | `number` | `22` | mín. 5 % · máx. 40 % · paso de 1 | **Tamaño**<br />Lado del logotipo, como proporción del código QR. Con «Tamaño seguro», se reduce al mayor tamaño que la corrección de errores puede reparar. |
| `logoSafe` | `boolean` | `true` |  | **Tamaño seguro**<br />Cuenta las palabras de código que tapa el logotipo, bloque por bloque, y reduce el logotipo mientras tape demasiadas: el enlace sigue siendo legible. Suba la corrección a H para un logotipo más grande. |
| `logoShape` | `string` | `"rounded"` | `none` Ninguno<br />`square` Cuadrada<br />`rounded` Redondeada<br />`circle` Redonda | **Placa**<br />Forma colocada bajo el logotipo; el logotipo se recorta con ella. |
| `logoBg` | `Color`<br />*Color sólido* | `"#ffffff"` |  | **Color de la placa**<br />Color de la placa bajo el logotipo.<br />*Se aplica cuando `logoShape` = `square` (Cuadrada) o `rounded` (Redondeada) o `circle` (Redonda).*<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |
| `logoPadding` | `number` | `1` | mín. 0 · máx. 4 · paso de 0.5 | **Margen**<br />Espacio alrededor del logotipo, en módulos. |
| `logoClear` | `boolean` | `true` |  | **Despejar los módulos**<br />Quita los módulos tapados por el logotipo, para un borde limpio. |
| `logoOpacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad**<br />Transparencia del logotipo. |

### Codificación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `ecl` | `string` | `"auto"` | `auto` Auto : M, o H en cuanto un logotipo o el semitono tapan módulos.<br />`L` L · 7 % : Código más pequeño y menos robusto.<br />`M` M · 15 % : Uso habitual.<br />`Q` Q · 25 % : Resiste la suciedad y los logotipos pequeños.<br />`H` H · 30 % : El más robusto: logotipo, estilo marcado, integración. | **Corrección de errores**<br />Parte del código que puede faltar sin impedir la lectura; cuanto más alta, más denso es el código. Sube sola mientras el tamaño no cambie. |
| `minVersion` | `number` | `1` | mín. 1 · máx. 40 · paso de 1 | **Versión mínima**<br />Tamaño mínimo de la cuadrícula (1 = 21 × 21 módulos, +4 por versión); útil para un motivo más fino o una cuadrícula fija. |
| `mask` | `string` | `"auto"` | `auto` Auto<br />`0` 0<br />`1` 1<br />`2` 2<br />`3` 3<br />`4` 4<br />`5` 5<br />`6` 6<br />`7` 7 | **Máscara**<br />Motivo que mezcla los datos; Auto elige el más legible y un número fijo cambia el aspecto del código. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/qrcode \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F logo=@logo.png \
  -F 'params={"contentType":"url","url":"https://pixlub.com","mode":"standard"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('logo', await openAsBlob('logo.png'), 'logo.png')
form.append('params', JSON.stringify({"contentType":"url","url":"https://pixlub.com","mode":"standard"}))

const res = await fetch('https://api.pixlub.com/v1/modules/qrcode', {
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
    "https://api.pixlub.com/v1/modules/qrcode",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("logo", open("logo.png", "rb"))],
    data={"params": json.dumps({"contentType": "url", "url": "https://pixlub.com", "mode": "standard"})},
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
result = client.tools.run("qrcode", inputs={"logo": "logo.png"}, params={"contentType": "url", "url": "https://pixlub.com", "mode": "standard"})
result.save(f"qrcode{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "qrcode", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "logo": pixlub.FromPath("logo.png"),
    },
    Params: map[string]any{"contentType": "url", "url": "https://pixlub.com", "mode": "standard"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("qrcode"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "qrcode",
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

## Tipos

Los valores estructurados de los ajustes, detallados como clases: cada miembro con su tipo y, después, un ejemplo.

<a name="type-colorgradient"></a>

### ColorGradient

*Objeto*. Degradado de colores: paradas colocadas a lo largo de un eje y la forma de repartirlas.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `stops` | `GradientStop[]` | Paradas de color, al menos dos, en cualquier orden. |
| `type` | `"linear" \| "radial"` | *opcional* · Lineal a lo largo de `angle`, o en círculos desde el centro. `linear` por defecto; sin efecto cuando solo cuenta el orden de los colores (Mapa de degradado). |
| `angle` | `number` | *opcional* · Dirección de un degradado lineal, en grados: 0 hacia arriba, 90 hacia la derecha. `90` por defecto. |

**Ejemplo**

```json
{
  "type": "linear",
  "angle": 90,
  "stops": [
    {
      "color": "#140a2e",
      "at": 0
    },
    {
      "color": "#c264c2",
      "at": 55
    },
    {
      "color": "#ffffff",
      "at": 100
    }
  ]
}
```

<a name="type-gradientstop"></a>

### GradientStop

*Objeto*. Parada de un degradado.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `color` | `Color` | Color CSS de la parada; se conserva el alfa (`#rrggbbaa`). |
| `at` | `number` | Posición de la parada, de 0 (inicio) a 100 (final), en %. |

**Ejemplo**

```json
{
  "color": "#c264c2",
  "at": 55
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/qrcode/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "contentType": {
      "title": "Type",
      "default": "url",
      "type": "string",
      "enum": [
        "url",
        "text",
        "wifi",
        "email",
        "tel",
        "sms",
        "vcard",
        "geo"
      ]
    },
    "url": {
      "title": "Link",
      "default": "https://pixlub.com",
      "type": "string"
    },
    "wifiSsid": {
      "title": "Network name (SSID)",
      "default": "",
      "type": "string"
    },
    "wifiSecurity": {
      "title": "Security",
      "default": "WPA",
      "type": "string",
      "enum": [
        "WPA",
        "WEP",
        "none"
      ]
    },
    "wifiPassword": {
      "title": "Password",
      "default": "",
      "type": "string"
    },
    "wifiHidden": {
      "title": "Hidden network",
      "default": false,
      "type": "boolean"
    },
    "vcardFirstName": {
      "title": "First name",
      "default": "",
      "type": "string"
    },
    "vcardLastName": {
      "title": "Last name",
      "default": "",
      "type": "string"
    },
    "vcardOrg": {
      "title": "Organization",
      "default": "",
      "type": "string"
    },
    "vcardTitle": {
      "title": "Job title",
      "default": "",
      "type": "string"
    },
    "emailTo": {
      "title": "Email",
      "default": "",
      "type": "string"
    },
    "phone": {
      "title": "Phone",
      "default": "",
      "type": "string"
    },
    "emailSubject": {
      "title": "Subject",
      "default": "",
      "type": "string"
    },
    "vcardUrl": {
      "title": "Website",
      "default": "",
      "type": "string"
    },
    "vcardStreet": {
      "title": "Street",
      "default": "",
      "type": "string"
    },
    "vcardZip": {
      "title": "Postal code",
      "default": "",
      "type": "string"
    },
    "vcardCity": {
      "title": "City",
      "default": "",
      "type": "string"
    },
    "vcardCountry": {
      "title": "Country",
      "default": "",
      "type": "string"
    },
    "geoLat": {
      "title": "Latitude",
      "default": 48.8584,
      "type": "number",
      "minimum": -90,
      "maximum": 90
    },
    "geoLng": {
      "title": "Longitude",
      "default": 2.2945,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "mode": {
      "title": "Mode",
      "default": "standard",
      "type": "string",
      "enum": [
        "standard",
        "shape",
        "image"
      ]
    },
    "outlineWidth": {
      "title": "Outline thickness",
      "default": 0.8,
      "type": "number",
      "minimum": 0,
      "maximum": 6,
      "multipleOf": 0.1
    },
    "outlineCustom": {
      "title": "Own outline color",
      "default": false,
      "type": "boolean"
    },
    "outlineColor": {
      "title": "Outline color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "patternDensity": {
      "title": "Pattern density",
      "default": 50,
      "type": "number",
      "minimum": 20,
      "maximum": 80,
      "multipleOf": 1
    },
    "qrSize": {
      "title": "QR code size",
      "default": 85,
      "type": "number",
      "minimum": 20,
      "maximum": 150,
      "multipleOf": 1
    },
    "cellSize": {
      "title": "Module size",
      "default": 12,
      "type": "number",
      "minimum": 3,
      "maximum": 64,
      "multipleOf": 1
    },
    "qrX": {
      "title": "Position X",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "qrY": {
      "title": "Position Y",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "halo": {
      "title": "Halo",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 6,
      "multipleOf": 1
    },
    "seed": {
      "title": "Variant",
      "default": 1,
      "type": "number",
      "minimum": 0,
      "maximum": 9999
    },
    "finderGuard": {
      "title": "Clear the eyes",
      "default": true,
      "type": "boolean"
    },
    "convert": {
      "title": "Method",
      "default": "qr",
      "type": "string",
      "enum": [
        "qr",
        "threshold",
        "dither",
        "ordered"
      ]
    },
    "tone": {
      "title": "Tone depth",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "threshold": {
      "title": "Threshold",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "contrast": {
      "title": "Contrast",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "invertImage": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "silhouette": {
      "title": "Follow the silhouette",
      "default": true,
      "type": "boolean"
    },
    "outline": {
      "title": "Outline",
      "default": true,
      "type": "boolean"
    },
    "colorSource": {
      "title": "Module color",
      "default": "qr",
      "type": "string",
      "enum": [
        "qr",
        "image"
      ]
    },
    "halftone": {
      "title": "Image through the QR",
      "default": false,
      "type": "boolean"
    },
    "halftoneStrength": {
      "title": "QR strength",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "qrSolidBg": {
      "title": "Solid background under the QR",
      "default": true,
      "type": "boolean"
    },
    "backdropOpacity": {
      "title": "Original image",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "moduleScale": {
      "title": "Size",
      "default": 100,
      "type": "number",
      "minimum": 40,
      "maximum": 100,
      "multipleOf": 1
    },
    "roundness": {
      "title": "Roundness",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "eyeCustom": {
      "title": "Own colors",
      "default": false,
      "type": "boolean"
    },
    "eyeFrameColor": {
      "title": "Frame color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "eyeBallColor": {
      "title": "Center color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "color": {
      "title": "Modules",
      "default": "#000000",
      "anyOf": [
        {
          "type": "string",
          "minLength": 1
        },
        {
          "type": "object",
          "required": [
            "stops"
          ],
          "properties": {
            "stops": {
              "type": "array",
              "items": {
                "type": "object",
                "required": [
                  "color",
                  "at"
                ],
                "properties": {
                  "color": {
                    "type": "string",
                    "minLength": 1
                  },
                  "at": {
                    "type": "number",
                    "minimum": 0,
                    "maximum": 100
                  }
                }
              },
              "minItems": 2
            },
            "type": {
              "type": "string",
              "enum": [
                "linear",
                "radial"
              ]
            },
            "angle": {
              "type": "number"
            }
          }
        }
      ]
    },
    "fgOpacity": {
      "title": "Module opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "background": {
      "title": "Background",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    },
    "bgOpacity": {
      "title": "Background opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "bgRadius": {
      "title": "Background corners",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 50,
      "multipleOf": 1
    },
    "size": {
      "title": "Size",
      "default": 1024,
      "type": "number",
      "minimum": 64,
      "maximum": 4096,
      "multipleOf": 1
    },
    "margin": {
      "title": "Margin (modules)",
      "default": 4,
      "type": "number",
      "minimum": 0,
      "maximum": 20,
      "multipleOf": 1
    },
    "logoSize": {
      "title": "Size",
      "default": 22,
      "type": "number",
      "minimum": 5,
      "maximum": 40,
      "multipleOf": 1
    },
    "logoSafe": {
      "title": "Safe size",
      "default": true,
      "type": "boolean"
    },
    "logoShape": {
      "title": "Plate",
      "default": "rounded",
      "type": "string",
      "enum": [
        "none",
        "square",
        "rounded",
        "circle"
      ]
    },
    "logoBg": {
      "title": "Plate color",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    },
    "logoPadding": {
      "title": "Padding",
      "default": 1,
      "type": "number",
      "minimum": 0,
      "maximum": 4,
      "multipleOf": 0.5
    },
    "logoClear": {
      "title": "Clear the modules",
      "default": true,
      "type": "boolean"
    },
    "logoOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "ecl": {
      "title": "Error correction",
      "default": "auto",
      "type": "string",
      "enum": [
        "auto",
        "L",
        "M",
        "Q",
        "H"
      ]
    },
    "minVersion": {
      "title": "Minimum version",
      "default": 1,
      "type": "number",
      "minimum": 1,
      "maximum": 40,
      "multipleOf": 1
    },
    "mask": {
      "title": "Mask",
      "default": "auto",
      "type": "string",
      "enum": [
        "auto",
        "0",
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7"
      ]
    },
    "text": {
      "type": "string",
      "default": ""
    },
    "emailBody": {
      "type": "string",
      "default": ""
    },
    "smsMessage": {
      "type": "string",
      "default": ""
    },
    "moduleShape": {
      "type": "string",
      "default": "square"
    },
    "eyeFrame": {
      "type": "string",
      "default": "square"
    },
    "eyeBall": {
      "type": "string",
      "default": "square"
    },
    "shape": {
      "type": "string",
      "default": "cloche"
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
