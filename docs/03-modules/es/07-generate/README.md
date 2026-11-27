# Generación

| Módulo | Descripción | API |
| --- | --- | --- |
| [Ruido](./noise/README.md) | Genera un ruido procedural (Perlin, simplex, aleatorio, Voronoi, puntos, cubista, esquirlas) con posprocesamiento y fusión | [API](./noise/api.md) |
| [Dibujar una máscara](./drawShape/README.md) | Dibuja formas precisas (curvas) combinadas por suma o resta, con salida en máscara | — |
| [Sólido](./solid/README.md) | Genera una forma rellena de un color sólido o de un degradado | [API](./solid/api.md) |
| [Paleta](./palette/README.md) | Define una paleta de colores para reutilizar en el grafo | — |
| [Paleta a partir de un degradado](./paletteFromGradient/README.md) | Muestrea un degradado en un número fijo de colores | — |
| [Paleta a partir de una imagen](./paletteFromImage/README.md) | Extrae los colores dominantes de una imagen (median cut) | [API](./paletteFromImage/api.md) |
| [Modelo 3D](./model3d/README.md) | Importa un modelo 3D (GLB, GLTF, OBJ, FBX, STL): cámara, materiales y animación. Para fusionarlo sobre una imagen, use «Fusión de modelo 3D». | — |
| [Material](./material/README.md) | Compone un material 3D: tipo de render (Estándar, sin iluminación, dibujo animado, matcap, teselación), superficie, una textura por mapa y efectos. El mismo material que en el editor 3D; para enlazar con un material del módulo «Modelo 3D». | — |
| [Motivo](./checker/README.md) | Genera un motivo repetido: tablero de ajedrez, cuadrícula, puntos, rayas, ladrillos, panal | — |
| [Degradado](./gradient/README.md) | Genera un degradado lineal, circular, radial o en rombo | — |
| [Código QR](./qrcode/README.md) | Genera un código QR legible por cualquier lector (enlace, wifi, contacto…), con estilo, con logotipo o fundido en una imagen | [API](./qrcode/api.md) |
| [Destello de lente](./flare/README.md) | Destello óptico: núcleo, ramas en estrella, halo cromático y reflejos fantasma | — |
| [Resplandor radial](./glow/README.md) | Genera un resplandor radial (núcleo, resplandor, aura) con control de la atenuación | — |
| [Rayo](./lightning/README.md) | Genera un rayo procedural ramificado entre dos puntos | — |
| [Trazado](./pathStroke/README.md) | Dibuja trazados vectoriales: pluma, lápiz, formas, trazos afilados y rellenos | — |
| [Partículas](./particles/README.md) | Dispersa una imagen de origen (o una mezcla de imágenes de un lote) en partículas (forma de emisión, estelas, atenuación), controladas por una semilla | [API](./particles/api.md) |
