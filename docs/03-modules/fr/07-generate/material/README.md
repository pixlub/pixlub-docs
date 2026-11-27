# Matériau

Compose un matériau 3D : type de rendu (Standard, sans éclairage, dessin animé, matcap, tessellation), surface, une texture par carte et des effets. Le même matériau que dans l’éditeur 3D ; à relier à un matériau du module « Modèle 3D ».

**Catégorie** : Génération · **Identifiant** : `material`

## Où l'utiliser

- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Couleur** (facultative)<br />Couleur de la surface ; sa transparence découpe le matériau. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Normales** (facultative)<br />Carte de normales : le relief fin sans toucher à la forme. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Rugosité** (facultative)<br />Gris : clair = mat, sombre = brillant. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Métal** (facultative)<br />Gris : blanc = métal, noir = non métallique. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Émission** (facultative)<br />Ce qui brille de soi-même, teinté par la couleur d’émission. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Occlusion** (facultative)<br />Ombres de contact dans les creux. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Opacité** (facultative)<br />Gris : blanc = opaque, noir = transparent. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Relief** (facultative)<br />Hauteurs en gris : le clair ressort. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |

> [!NOTE]
> **Guide en préparation**
>
> Ce module n'a pas encore de guide détaillé. Ses réglages s'affichent avec leur description dans l'application ; la vue API liste chacun d'eux avec ses limites.
