# Décalcomanie

Draper une image sur un objet photographié, en suivant son relief.

**Catégorie** : Services API · **Identifiant** : `decalApi` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/decalApi)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Surface** (obligatoire)<br />Photo de l'objet dont le relief 3D est reconstruit. C'est la seule image envoyée au serveur. | `PNG`, `JPEG`, `WebP`, `GIF` | Un fichier |
| **Motif** (obligatoire)<br />Image posée et drapée sur l'objet. | `PNG`, `JPEG`, `WebP`, `GIF` | Un fichier |

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Utilisation

1. **Se connecter**

   Le relief est reconstruit par nos serveurs : un compte est demandé.

2. **Importer**

   La **photo de l'objet**, puis l'**image à poser** (un logo, un motif).

3. **Lancer, puis placer**

   Seule la photo part, une fois. Ensuite, placez et réglez l'image librement, sans nouvel envoi.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Placement** | Position, taille, rotation et profondeur du relief. |
| **Lumière** | Reflets et ombres, plis. |
| **Calque** | Opacité, mode de fusion, rester sur l'objet. |

## Astuces

- Déplacer ou redimensionner l'image posée ne coûte rien : seul un changement de photo relance le serveur.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
