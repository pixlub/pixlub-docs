# Módulos

Todos los módulos de Pixlub, por categoría. Cada ficha tiene dos vistas: el uso en el sitio y la referencia de la API.

Cada módulo tiene su ficha, con dos vistas:

- **Aplicación**: dónde encontrar el módulo en el sitio y cómo usarlo, con una guía escrita a mano cuando existe.
- **API**: el endpoint, los archivos esperados, cada ajuste con su tipo, sus límites y su valor por defecto, y ejemplos de solicitud en cURL, JavaScript, Python y con los SDK. Esta vista se **genera** a partir del registro de módulos: sigue cada nueva versión sin actualización manual.

Los módulos marcados **API** se llaman mediante la [API](../../02-api/es/01-getting-started.md); los demás (video, documentos, bloques del grafo) se usan en el sitio.

## Módulos básicos

| Módulo | Descripción | API |
| --- | --- | --- |
| [Imagen de origen](./01-base/source/README.md) | Carga una imagen desde un archivo y la proporciona al grafo. | — |
| [Vista previa](./01-base/preview/README.md) | Muestra la imagen y la transmite sin cambios. El nodo se agranda al alejar el zoom para ofrecer una mejor vista de conjunto. | — |

## Salida

| Módulo | Descripción | API |
| --- | --- | --- |
| [Exportación](./02-output/output/README.md) | Muestra una vista previa de la imagen resultante y la exporta. | — |
| [Exportar un lote](./02-output/exportBatch/README.md) | Descarga todas las imágenes de un lote: un archivo comprimido, archivos separados o una animación. | — |

## Transformación

| Módulo | Descripción | API |
| --- | --- | --- |
| [Redimensionar](./03-transform/resize/README.md) | Modifica las dimensiones de la imagen | [API](./03-transform/resize/api.md) |
| [Redimensionar (factor)](./03-transform/resizeFactor/README.md) | Escala la imagen por un factor multiplicador | [API](./03-transform/resizeFactor/api.md) |
| [Ampliar](./03-transform/extend/README.md) | Amplía la zona de la imagen sin deformar el contenido | [API](./03-transform/extend/api.md) |
| [Recortar](./03-transform/crop/README.md) | Recorta una zona de la imagen | [API](./03-transform/crop/api.md) |
| [Recorte automático](./03-transform/trim/README.md) | Recorta automáticamente los bordes transparentes | [API](./03-transform/trim/api.md) |
| [Rotación](./03-transform/rotate/README.md) | Gira la imagen | [API](./03-transform/rotate/api.md) |
| [Espejo](./03-transform/flip/README.md) | Voltea la imagen horizontal y/o verticalmente | [API](./03-transform/flip/api.md) |
| [Inclinación](./03-transform/skew/README.md) | Inclina la imagen (cizallamiento horizontal y vertical) | [API](./03-transform/skew/api.md) |
| [Perspectiva](./03-transform/cornerPin/README.md) | Mueve libremente las cuatro esquinas de la imagen para ponerla en perspectiva | [API](./03-transform/cornerPin/api.md) |
| [Sticker](./03-transform/sticker/README.md) | Despega la imagen como un sticker, enrollándola en la dirección elegida | [API](./03-transform/sticker/api.md) |
| [Desplazamiento](./03-transform/translate/README.md) | Desplaza la textura en X y en Y, en % de la imagen | [API](./03-transform/translate/api.md) |
| [Transformación](./03-transform/transform/README.md) | Mueve, gira, escala, voltea y desvanece la imagen de una vez | [API](./03-transform/transform/api.md) |
| [Marioneta](./03-transform/puppet/README.md) | Deforma la imagen moviendo alfileres sobre una malla (puppet warp) | [API](./03-transform/puppet/api.md) |
| [Polar](./03-transform/polar/README.md) | Convierte entre coordenadas rectangulares y polares (anillos, rayos, halos) | [API](./03-transform/polar/api.md) |
| [Ondulación](./03-transform/ripple/README.md) | Distorsión en anillos concéntricos alrededor de un centro | [API](./03-transform/ripple/api.md) |
| [Desplazamiento](./03-transform/displace/README.md) | Deforma la imagen según un mapa de desplazamiento (ruido, degradado…) | [API](./03-transform/displace/api.md) |
| [Remapeo de textura](./03-transform/remap/README.md) | Vuelve a dibujar la imagen leyendo, para cada píxel, la posición indicada por un mapa (degradado, ruido…) | [API](./03-transform/remap/api.md) |
| [Caleidoscopio](./03-transform/kaleidoscope/README.md) | Repite un sector en simetría radial | [API](./03-transform/kaleidoscope/api.md) |
| [Remolino](./03-transform/twirl/README.md) | Retuerce la imagen en espiral alrededor de un centro | [API](./03-transform/twirl/api.md) |
| [Onda](./03-transform/wave/README.md) | Desplazamiento sinusoidal horizontal / vertical | [API](./03-transform/wave/api.md) |
| [Distorsión de lente](./03-transform/fisheye/README.md) | Abomba (ojo de pez) o hunde (cojín) la imagen alrededor de un centro | [API](./03-transform/fisheye/api.md) |
| [Desplazamiento de unión](./03-transform/tile/README.md) | Desplaza la imagen con envoltura: comprobar y crear texturas repetibles | [API](./03-transform/tile/api.md) |
| [Curvar sobre un camino](./03-transform/warpPath/README.md) | Deforma una imagen a lo largo de un camino (cinta / estela curvada) | [API](./03-transform/warpPath/api.md) |
| [Seguir un camino](./03-transform/followPath/README.md) | Desplaza una imagen a lo largo de un camino, del 0 % al 100 % de su longitud; el camino puede salir del encuadre | [API](./03-transform/followPath/api.md) |
| [Recorte](./03-transform/trimVideo/README.md) | Recorta una parte del video en un momento dado. | — |
| [Velocidad](./03-transform/speedVideo/README.md) | Acelera o ralentiza el video. La velocidad de fotogramas de salida sigue siendo la misma: lo que cambia son los fotogramas que se piden al original. | — |
| [Velocidad de fotogramas](./03-transform/frameRateVideo/README.md) | Reescribe la velocidad de fotogramas del video. Bajarla aligera el archivo; subirla por encima de la del original duplica fotogramas. | — |

## Ajuste

| Módulo | Descripción | API |
| --- | --- | --- |
| [Ajuste básico](./04-adjust/baseAdjust/README.md) | Los ajustes esenciales de una foto, reunidos: luz, tonos, balance de blancos y colores | [API](./04-adjust/baseAdjust/api.md) |
| [Niveles](./04-adjust/levels/README.md) | Ajusta los puntos negro y blanco, la gamma y el rango de salida, por canal | [API](./04-adjust/levels/api.md) |
| [Balance de blancos](./04-adjust/whiteBalance/README.md) | Calienta o enfría la imagen y corrige su dominante verde o magenta | [API](./04-adjust/whiteBalance/api.md) |
| [Recolorear](./04-adjust/recolor/README.md) | Tiñe toda la imagen de un solo color, conservando sus sombras y sus luces | [API](./04-adjust/recolor/api.md) |
| [HSL](./04-adjust/hsl/README.md) | Desplaza el tono, la saturación y la luminosidad de un rango de colores | [API](./04-adjust/hsl/api.md) |
| [Blanco y negro](./04-adjust/blackWhite/README.md) | Pasa la imagen a gris dosificando la luminosidad de cada color | [API](./04-adjust/blackWhite/api.md) |
| [Brillo y contraste](./04-adjust/brightness/README.md) | Ajusta el brillo y el contraste | [API](./04-adjust/brightness/api.md) |
| [Posterizar](./04-adjust/posterize/README.md) | Reduce el número de niveles por canal (tonos planos estilizados, cel shading) | [API](./04-adjust/posterize/api.md) |
| [Exposición](./04-adjust/exposure/README.md) | Sube o baja la luz de la imagen, paso a paso como una cámara fotográfica | [API](./04-adjust/exposure/api.md) |
| [Curvas](./04-adjust/curves/README.md) | Ajusta la tonalidad con una curva editable, por canal o global | [API](./04-adjust/curves/api.md) |
| [Curvas de saturación / tono](./04-adjust/hueSatCurves/README.md) | Ajusta la saturación o el tono según la luminancia, la saturación o el tono de cada color | [API](./04-adjust/hueSatCurves/api.md) |
| [Mezclador de canales](./04-adjust/channelMixer/README.md) | Recompone cada canal a partir de los demás, en el espacio elegido | [API](./04-adjust/channelMixer/api.md) |
| [Invertir](./04-adjust/invert/README.md) | Pasa la imagen a negativo | [API](./04-adjust/invert/api.md) |
| [Equilibrio de color](./04-adjust/colorBalance/README.md) | Ajusta los tonos por rango tonal (claros, medios, oscuros), con máscara opcional | [API](./04-adjust/colorBalance/api.md) |
| [Filtro de accesibilidad](./04-adjust/colorAccessibility/README.md) | Corrige los colores para que sigan siendo legibles con una visión daltónica | [API](./04-adjust/colorAccessibility/api.md) |
| [Paleta: recolorear](./04-adjust/paletteRemap/README.md) | Genera una variante recoloreada de la imagen por cada color de la paleta (lote) | [API](./04-adjust/paletteRemap/api.md) |
| [Umbral](./04-adjust/threshold/README.md) | Binariza la luminancia según un umbral (con transición suave) | [API](./04-adjust/threshold/api.md) |
| [Reemplazar colores](./04-adjust/replaceColors/README.md) | Reemplaza una lista de colores de origen por colores de destino | [API](./04-adjust/replaceColors/api.md) |
| [Opacidad](./04-adjust/opacity/README.md) | Modifica la opacidad de la imagen | [API](./04-adjust/opacity/api.md) |
| [Contorno](./04-adjust/outline/README.md) | Añade un contorno a la imagen | [API](./04-adjust/outline/api.md) |
| [Sombra](./04-adjust/shadow/README.md) | Proyecta una sombra (exterior o interior) a partir del alfa de la imagen | [API](./04-adjust/shadow/api.md) |
| [Mapa de degradado](./04-adjust/gradientMap/README.md) | Colorea la imagen asignando su luminancia a un degradado | [API](./04-adjust/gradientMap/api.md) |

## Filtros

| Módulo | Descripción | API |
| --- | --- | --- |
| [Desenfoque](./05-filter/blur/README.md) | Desenfoque gaussiano, de movimiento, de rotación o de zoom (centro interactivo) | [API](./05-filter/blur/api.md) |
| [Desenfoque de movimiento](./05-filter/motionBlur/README.md) | Desenfoque direccional, de zoom o de rotación (velocidad, estelas, impactos) | [API](./05-filter/motionBlur/api.md) |
| [Nitidez](./05-filter/sharpen/README.md) | Refuerza los detalles y los contornos (máscara de enfoque) | [API](./05-filter/sharpen/api.md) |
| [Reducción de ruido](./05-filter/denoise/README.md) | Reduce el ruido conservando los contornos (filtro de mediana) | [API](./05-filter/denoise/api.md) |
| [Detección de contornos](./05-filter/edgeDetect/README.md) | Extrae los contornos (Sobel) con doble umbral, colores y desenfoque previo | [API](./05-filter/edgeDetect/api.md) |
| [Aberración cromática](./05-filter/chromatic/README.md) | Desplaza los canales rojo y azul (efecto de lente, glitch, impacto) | [API](./05-filter/chromatic/api.md) |
| [Dilatar / Erosionar](./05-filter/morphology/README.md) | Engrosa o contrae las zonas opacas (máscaras, contornos, siluetas) | [API](./05-filter/morphology/api.md) |
| [Mapa de normales](./05-filter/normalMap/README.md) | Genera un mapa de normales a partir de un mapa de alturas (relieve para motores 3D / VFX) | [API](./05-filter/normalMap/api.md) |
| [Pixelar](./05-filter/pixelate/README.md) | Reduce la imagen a píxeles grandes (efecto pixel art) | [API](./05-filter/pixelate/api.md) |
| [Semitono](./05-filter/halftone/README.md) | Trama de puntos, tramado ordenado (Bayer) o difusión de error (retro / impresión) | [API](./05-filter/halftone/api.md) |
| [Pintura](./05-filter/kuwahara/README.md) | Manchas pictóricas que conservan los contornos (filtro de Kuwahara, efecto óleo) | [API](./05-filter/kuwahara/api.md) |
| [Ordenación de píxeles](./05-filter/pixelSort/README.md) | Ordena los píxeles por luminancia en las zonas claras u oscuras (glitch art) | [API](./05-filter/pixelSort/api.md) |
| [Líneas CRT](./05-filter/scanlines/README.md) | Líneas de barrido y máscara RGB al estilo de una pantalla de tubo | [API](./05-filter/scanlines/api.md) |
| [Rayos de luz](./05-filter/rays/README.md) | Rayos volumétricos emitidos por las zonas claras desde un centro (god rays) | [API](./05-filter/rays/api.md) |
| [Borde difuminado](./05-filter/feather/README.md) | Suaviza los bordes de la transparencia (fundido de la máscara alfa) | [API](./05-filter/feather/api.md) |
| [Viñeta](./05-filter/vignette/README.md) | Oscurece progresivamente los bordes de la imagen | [API](./05-filter/vignette/api.md) |
| [Bloom](./05-filter/bloom/README.md) | Difunde las zonas luminosas en un halo aditivo (glow) | [API](./05-filter/bloom/api.md) |
| [Quitar un fondo liso](./05-filter/removeBg/README.md) | Vuelve transparente un fondo de un solo color (pantalla verde, estudio…), detectado o elegido. | [API](./05-filter/removeBg/api.md) |
| [Separar RGB](./05-filter/splitRgb/README.md) | Separa la imagen en sus canales rojo, verde y azul | [API](./05-filter/splitRgb/api.md) |
| [Separar transparencia](./05-filter/splitAlpha/README.md) | Separa la imagen en su canal de color (RGB opaco) y su canal alfa (escala de grises) | [API](./05-filter/splitAlpha/api.md) |
| [Purpurina](./05-filter/glitter/README.md) | Cubre la imagen de purpurina centelleante: escamas irisadas, destellos de estrella y un reflejo que barre, en bucle. | [API](./05-filter/glitter/api.md) |

## Composición

| Módulo | Descripción | API |
| --- | --- | --- |
| [Separar los canales](./06-compose/channelSplit/README.md) | Extrae los canales R, G, B y alfa como canales (escala de grises) | [API](./06-compose/channelSplit/api.md) |
| [Combinar los canales](./06-compose/channelMerge/README.md) | Recompone una imagen a partir de canales R, G, B y/o alfa | [API](./06-compose/channelMerge/api.md) |
| [Imagen a máscara](./06-compose/imageToMask/README.md) | Convierte una imagen en un canal de máscara (alfa, canal o luminancia) | [API](./06-compose/imageToMask/api.md) |
| [Fusión](./06-compose/merge/README.md) | Superpone una o varias imágenes (capas) sobre otra | [API](./06-compose/merge/api.md) |
| [Combinar transparencia](./06-compose/mergeAlpha/README.md) | Recombina un canal de color (RGB) y un canal alfa en una imagen transparente | [API](./06-compose/mergeAlpha/api.md) |
| [Hoja de sprites](./06-compose/spriteSheet/README.md) | Reúne varias imágenes en una cuadrícula (flipbook, atlas de VFX) | [API](./06-compose/spriteSheet/api.md) |
| [Disposición](./06-compose/arrange/README.md) | Alinea varias imágenes una al lado de otra o apiladas (banners, comparativas) | [API](./06-compose/arrange/api.md) |
| [Reunir un lote](./06-compose/arrayBatch/README.md) | Agrupa imágenes y lotes en un solo lote | — |
| [Separar un lote](./06-compose/arraySplitBatch/README.md) | Divide un lote en imágenes individuales | — |
| [Máscara](./06-compose/mask/README.md) | Modula la opacidad de una imagen mediante la luminancia (o el alfa) de una máscara | [API](./06-compose/mask/api.md) |
| [Borrador](./06-compose/eraser/README.md) | Borra a mano partes de la imagen, con una paleta de puntas ajustables | [API](./06-compose/eraser/api.md) |
| [Fusión de modelo 3D](./06-compose/model3dMerge/README.md) | Renderiza un modelo 3D y lo superpone sobre una imagen: posición, rotación, escala. | — |

## Generación

| Módulo | Descripción | API |
| --- | --- | --- |
| [Ruido](./07-generate/noise/README.md) | Genera un ruido procedural (Perlin, simplex, aleatorio, Voronoi, puntos, cubista, esquirlas) con posprocesamiento y fusión | [API](./07-generate/noise/api.md) |
| [Dibujar una máscara](./07-generate/drawShape/README.md) | Dibuja formas precisas (curvas) combinadas por suma o resta, con salida en máscara | — |
| [Sólido](./07-generate/solid/README.md) | Genera una forma rellena de un color sólido o de un degradado | [API](./07-generate/solid/api.md) |
| [Paleta](./07-generate/palette/README.md) | Define una paleta de colores para reutilizar en el grafo | — |
| [Paleta a partir de un degradado](./07-generate/paletteFromGradient/README.md) | Muestrea un degradado en un número fijo de colores | — |
| [Paleta a partir de una imagen](./07-generate/paletteFromImage/README.md) | Extrae los colores dominantes de una imagen (median cut) | [API](./07-generate/paletteFromImage/api.md) |
| [Modelo 3D](./07-generate/model3d/README.md) | Importa un modelo 3D (GLB, GLTF, OBJ, FBX, STL): cámara, materiales y animación. Para fusionarlo sobre una imagen, use «Fusión de modelo 3D». | — |
| [Material](./07-generate/material/README.md) | Compone un material 3D: tipo de render (Estándar, sin iluminación, dibujo animado, matcap, teselación), superficie, una textura por mapa y efectos. El mismo material que en el editor 3D; para enlazar con un material del módulo «Modelo 3D». | — |
| [Motivo](./07-generate/checker/README.md) | Genera un motivo repetido: tablero de ajedrez, cuadrícula, puntos, rayas, ladrillos, panal | — |
| [Degradado](./07-generate/gradient/README.md) | Genera un degradado lineal, circular, radial o en rombo | — |
| [Código QR](./07-generate/qrcode/README.md) | Genera un código QR legible por cualquier lector (enlace, wifi, contacto…), con estilo, con logotipo o fundido en una imagen | [API](./07-generate/qrcode/api.md) |
| [Destello de lente](./07-generate/flare/README.md) | Destello óptico: núcleo, ramas en estrella, halo cromático y reflejos fantasma | — |
| [Resplandor radial](./07-generate/glow/README.md) | Genera un resplandor radial (núcleo, resplandor, aura) con control de la atenuación | — |
| [Rayo](./07-generate/lightning/README.md) | Genera un rayo procedural ramificado entre dos puntos | — |
| [Trazado](./07-generate/pathStroke/README.md) | Dibuja trazados vectoriales: pluma, lápiz, formas, trazos afilados y rellenos | — |
| [Partículas](./07-generate/particles/README.md) | Dispersa una imagen de origen (o una mezcla de imágenes de un lote) en partículas (forma de emisión, estelas, atenuación), controladas por una semilla | [API](./07-generate/particles/api.md) |

## Servicios de API

| Módulo | Descripción | API |
| --- | --- | --- |
| [Quitar el fondo](./08-api/removeBgApi/README.md) | Detecta el sujeto mediante IA (con nuestros servicios) y vuelve transparente todo lo demás, sea cual sea el fondo. | [API](./08-api/removeBgApi/api.md) |
| [Difuminado de rostros](./08-api/faceBlurApi/README.md) | Difumina zonas dibujadas a mano o detecta los rostros mediante IA (nuestros servicios). Las zonas se pueden editar en la vista previa: crear, mover, redimensionar, eliminar. | [API](./08-api/faceBlurApi/api.md) |
| [Calcomanía](./08-api/decalApi/README.md) | Reconstruye mediante IA (nuestros servicios) el relieve 3D del objeto y luego drapea sobre él la imagen que usted coloca libremente encima. Solo se envía la foto, una sola vez; la imagen colocada se queda en su equipo. | [API](./08-api/decalApi/api.md) |
| [Difuminado de rostros (video)](./08-api/faceBlurVideoApi/README.md) | Difumina zonas dibujadas a mano o detecta los rostros de cada fotograma mediante nuestra API. Cada zona se sigue en el tiempo y se ajusta en la vista previa, fotograma a fotograma. En modo automático, la detección se envía al servidor una sola vez; el difuminado siempre se calcula en el navegador. | — |
| [Subtítulos (video)](./08-api/transcribeVideoApi/README.md) | Transcribe el habla de un video mediante nuestra API, palabra por palabra y con marcas de tiempo, y luego incrusta los subtítulos en la imagen. La transcripción se envía al servidor una sola vez; el formato se sigue calculando en el navegador. | — |

## Valores

| Módulo | Descripción | API |
| --- | --- | --- |
| [Valor](./09-operation/value/README.md) | Emite un valor numérico constante. | — |
| [Suma](./09-operation/add/README.md) | Suma de dos entradas (A + B). | — |
| [Resta](./09-operation/subtract/README.md) | Diferencia de dos entradas (A - B). | — |
| [Multiplicación](./09-operation/multiply/README.md) | Producto de dos entradas (A × B). | — |
| [División](./09-operation/divide/README.md) | Cociente de dos entradas (A ÷ B); 0 si B = 0. | — |
| [Tamaño de imagen](./09-operation/size/README.md) | Ancho y alto de la imagen de entrada. | — |

## Texto

| Módulo | Descripción | API |
| --- | --- | --- |
| [Texto](./10-text/text/README.md) | Compone un texto: tipografía, color sólido o degradado, pila de estilos y animación. | — |
| [Texto a imagen](./10-text/textRender/README.md) | Renderiza un texto en un marco elegido: tamaño, anclaje, fondo. | — |

## Colores

| Módulo | Descripción | API |
| --- | --- | --- |
| [Color](./11-color/color/README.md) | Emite un color (sólido o degradado). | — |

## Conversión

| Módulo | Descripción | API |
| --- | --- | --- |
| [Extracción de audio](./12-conversion/extractAudioVideo/README.md) | Extrae la pista de sonido de un video a un archivo de audio: MP3, AAC, Opus, FLAC, WAV… o la pista original tal cual, sin pérdida. | — |
| [Conversión de audio](./12-conversion/convertAudio/README.md) | Convierte un archivo de sonido a otro formato (MP3, AAC, Opus, Vorbis, FLAC, WAV o AIFF), con su tasa de bits, su frecuencia y sus canales, y conserva la parte que quiera. | — |
| [Conversión](./12-conversion/convert/README.md) | Convierte imágenes, animaciones, videos y audios a cualquier formato de exportación: PNG, JPG, WebP, GIF, MP4, WebM, MP3, FLAC, WAV, PDF… | [API](./12-conversion/convert/api.md) |

## Documentos

| Módulo | Descripción | API |
| --- | --- | --- |
| [Unir PDF](./13-document/docMerge/README.md) | Reúne varios PDF en un solo archivo, en el orden que elija. | — |
| [Dividir un PDF](./13-document/docSplit/README.md) | Separa un PDF en varios archivos: página por página, por bloques, en las marcas colocadas en la vista previa o según sus rangos. Se exporta en PDF o en imágenes. | — |
| [Organizar las páginas](./13-document/docPages/README.md) | Conserva, elimina, reordena, duplica o gira las páginas de un PDF. | — |
| [Recortar un PDF](./13-document/docCrop/README.md) | Quita un margen alrededor de las páginas, sin tocar su contenido: el mismo en todas o uno propio para algunas páginas. | — |
| [Numerar las páginas](./13-document/docPageNumbers/README.md) | Añade un número en cada página, en el lugar y con el formato que elija. | — |
| [Marca de agua](./13-document/docWatermark/README.md) | Coloca un texto o una imagen translúcidos sobre las páginas, una vez o en mosaico. | — |
| [Metadatos](./13-document/docMetadata/README.md) | Lee y modifica el título, el autor, el asunto y las palabras clave de un PDF, o los borra. | — |
| [Firmar un PDF](./13-document/docSign/README.md) | Coloca su firma, dibujada o importada, en las páginas que elija. | — |
| [Imágenes a PDF](./13-document/docImagesToPdf/README.md) | Reúne imágenes en un PDF: componga sus páginas, con una o varias imágenes cada una, colocadas donde quiera. | — |
| [PDF a imágenes](./13-document/docPdfToImages/README.md) | Exporta cada página en PNG, JPEG o WebP, a la resolución elegida. | — |
| [PDF a Word](./13-document/docPdfToWord/README.md) | Lleva los títulos, los párrafos y las tablas de un PDF a un documento de Word editable. | — |
| [PDF a Excel](./13-document/docPdfToExcel/README.md) | Ordena el contenido de un PDF en un libro de cálculo: las columnas alineadas se convierten en columnas y los números, en números. | — |
| [Office a PDF](./13-document/docOfficeToPdf/README.md) | Convierte un documento de Word, Excel, PowerPoint u OpenDocument en PDF. | — |
| [HTML a PDF](./13-document/docHtmlToPdf/README.md) | Maqueta un archivo HTML y lo convierte en PDF, con texto seleccionable. | — |
| [Comprimir un PDF](./13-document/docCompress/README.md) | Reduce el peso de un PDF recodificando sus imágenes; el texto sigue nítido y seleccionable. | — |
| [Reparar un PDF](./13-document/docRepair/README.md) | Reconstruye un PDF dañado o que se abre mal: tabla de objetos, catálogo y árbol de páginas. | — |
| [Proteger un PDF](./13-document/docProtect/README.md) | Cifra un PDF en AES-256 con una contraseña y limita lo que se puede hacer con él. | — |
| [Desbloquear un PDF](./13-document/docUnlock/README.md) | Quita la contraseña y las restricciones de un PDF protegido, si conoce su contraseña. | — |
| [Censurar un PDF](./13-document/docRedact/README.md) | Tapa en negro las palabras o los patrones elegidos: el texto desaparece realmente de la página. | — |
| [Extraer el texto (OCR)](./13-document/docOcrText/README.md) | Lee el texto de un PDF, de un escaneo o de una foto de documento y lo exporta como texto sin formato o como PDF con búsqueda. | — |
| [Comparar dos PDF](./13-document/docCompare/README.md) | Enumera las líneas añadidas y eliminadas página por página, y señala las páginas cuyo aspecto ha cambiado. | — |
