# Convertisseur d'image

Changer le format d'une ou plusieurs images : formats disponibles, réglages, traitement local ou serveur.

Le [convertisseur d'image](https://pixlub.com/fr/image/convert) change le format de vos fichiers sans rien installer. Chaque format de sortie a aussi sa page dédiée, par exemple [convertir en WebP](https://pixlub.com/fr/image/convert/webp), qui ouvre l'outil avec ce format déjà choisi.

## Convertir

1. **Déposer vos fichiers**

   Glissez une ou plusieurs images dans la zone de dépôt, ou cliquez sur **Choisir**. JPG, PNG, WebP, HEIC, GIF… et même des vidéos, dont l'image est extraite.

2. **Choisir le format**

   Les formats vont du plus courant au plus spécialisé. Les réglages s'adaptent au format : **qualité** pour les formats compressés, **échelle**, et **fond** pour les formats sans transparence.

3. **Télécharger**

   Récupérez les fichiers un par un, ou tout le lot dans une archive ZIP.

## Local ou serveur

| Format | Traitement |
| --- | --- |
| PNG, JPG, WebP | Encodés par votre navigateur : vos images ne quittent pas votre appareil. |
| AVIF, JPEG XL, HEIC, TIFF, ICO, PDF… | Encodés par notre API : la pastille passe sur **Envoyé au serveur** dès que le format est choisi. |

La page de chaque format indique où il est encodé (« Dans votre navigateur » ou « Par notre API »), s'il conserve la transparence et si sa compression se règle.

> [!TIP]
> **Transparence**
>
> Un format sans canal alpha (JPG, BMP…) aplatit l'image sur la couleur de **fond** choisie. Gardez PNG, WebP ou AVIF pour conserver la transparence.

## Par l'API

Le même convertisseur est le module [`convert`](../../../03-modules/fr/12-conversion/convert/api.md) de l'API : un fichier dans le champ `in`, le format dans `params`.
