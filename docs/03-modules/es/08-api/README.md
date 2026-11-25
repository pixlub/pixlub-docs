# Servicios de API

| Módulo | Descripción | API |
| --- | --- | --- |
| [Quitar el fondo](./removeBgApi/README.md) | Detecta el sujeto mediante IA (con nuestros servicios) y vuelve transparente todo lo demás, sea cual sea el fondo. | [API](./removeBgApi/api.md) |
| [Difuminado de rostros](./faceBlurApi/README.md) | Difumina zonas dibujadas a mano o detecta los rostros mediante IA (nuestros servicios). Las zonas se pueden editar en la vista previa: crear, mover, redimensionar, eliminar. | [API](./faceBlurApi/api.md) |
| [Calcomanía](./decalApi/README.md) | Reconstruye mediante IA (nuestros servicios) el relieve 3D del objeto y luego drapea sobre él la imagen que usted coloca libremente encima. Solo se envía la foto, una sola vez; la imagen colocada se queda en su equipo. | [API](./decalApi/api.md) |
| [Difuminado de rostros (video)](./faceBlurVideoApi/README.md) | Difumina zonas dibujadas a mano o detecta los rostros de cada fotograma mediante nuestra API. Cada zona se sigue en el tiempo y se ajusta en la vista previa, fotograma a fotograma. En modo automático, la detección se envía al servidor una sola vez; el difuminado siempre se calcula en el navegador. | — |
| [Subtítulos (video)](./transcribeVideoApi/README.md) | Transcribe el habla de un video mediante nuestra API, palabra por palabra y con marcas de tiempo, y luego incrusta los subtítulos en la imagen. La transcripción se envía al servidor una sola vez; el formato se sigue calculando en el navegador. | — |
