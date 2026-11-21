# Traitement local et serveur

Ce qui reste sur votre appareil, ce qui part sur nos serveurs, et comment la pastille de confidentialité vous le dit.

Pixlub traite vos fichiers **dans votre navigateur**. C'est une promesse : tant qu'aucune opération distante n'entre en jeu, vos images, vidéos et documents ne quittent pas votre appareil.

## La pastille

Les pages d'édition (page module, graphe d'image, éditeur vidéo, éditeur de réglages) affichent une pastille en bas de l'écran :

| Pastille | Signification |
| --- | --- |
| **Traitement local** | Rien ne part : tout se calcule sur votre appareil. |
| **Envoyé au serveur** | Une opération de la page envoie un fichier à nos serveurs. Ouvrez la pastille pour voir laquelle. |

La pastille annonce ce que la page **s'apprête** à envoyer, pas seulement ce qui est déjà parti : elle bascule dès que vous posez un module d'IA, choisissez un format encodé par le serveur ou ouvrez les sous-titres automatiques. Elle garde aussi l'historique de ce qui a déjà été envoyé pendant la session. Vous pouvez la déplacer ; elle se range du côté le plus proche.

## Ce qui part sur nos serveurs

| Opération | Ce qui est envoyé |
| --- | --- |
| Module d'IA (détourage, floutage auto, décalcomanie…) | L'image d'entrée du module, et seulement les réglages dont le service a besoin. |
| Format d'export encodé par l'API (AVIF, HEIC, TIFF, PDF…) | L'image à convertir. |
| Sous-titres automatiques | Le son du montage. |
| Conversion Office ou HTML vers PDF | Le fichier à convertir. |

Les autres réglages d'un module d'IA restent sur votre appareil : les modifier ne relance pas d'envoi et ne rend pas le résultat obsolète.

## Ce que deviennent les fichiers envoyés

Le résultat est disponible par un lien signé, valable une heure ; les fichiers sont effacés de nos serveurs au bout de 24 heures. Les statistiques d'usage ne retiennent que le nom des modules utilisés, la taille et la nature des fichiers importés, jamais leur nom ni leur contenu.

Pour le détail des mesures de sécurité, voir la page [Sécurité](https://pixlub.com/fr/security).
