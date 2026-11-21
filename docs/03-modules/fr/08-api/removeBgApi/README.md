# Retirer un fond

Détourer le sujet d'une photo par IA, quel que soit le fond.

**Catégorie** : Services API · **Identifiant** : `removeBgApi` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/removeBgApi)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image envoyée au serveur, dont le sujet est détecté et le fond rendu transparent. | `PNG`, `JPEG`, `WebP`, `GIF` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Utilisation

1. **Se connecter**

   Le détourage passe par nos serveurs : un compte est demandé.

2. **Importer**

   Personne, objet, animal, produit : le sujet est détecté quel que soit le fond.

3. **Lancer**

   Le prix en crédits s'affiche avant le lancement ; l'image revient avec un fond transparent.

Aucun réglage : relancer le même fichier donne le même résultat, et coûte de nouveau.

## Retoucher à la gomme

- Le bouton **Gomme** de l'aperçu l'allume : ses options flottent sur l'image.
- Peignez pour retirer ce qui reste ; **Restaurer** (ou **Alt**) remet ce que le détourage a emporté.
- La retouche se fait dans votre navigateur : elle ne relance pas l'appel et ne coûte rien.
- **Zones gommées en rouge** montre tout ce qui a été retiré.

## Astuces

- Exportez en PNG, WebP ou AVIF pour garder la transparence.
- Pour un fond d'une seule couleur, [Retirer un fond uni](../../05-filter/removeBg/README.md) le fait dans votre navigateur, sans crédit.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
