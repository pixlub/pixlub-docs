# Éditeur vidéo

Monter des vidéos, des sons, des images et des textes dans le navigateur : timeline, effets, transitions, sous-titres et export.

L'[éditeur vidéo](https://pixlub.com/fr/video/editor) est un logiciel de montage complet qui tourne dans votre navigateur. Le décodage, l'aperçu et l'encodage se font sur votre appareil ; seuls les **sous-titres automatiques** envoient le son du montage à nos serveurs.

## L'interface

| Zone | Rôle |
| --- | --- |
| Médias | Vos fichiers importés (vidéos, sons, images), les textes, les solides, les transitions, les compositions et les enregistrements. |
| Aperçu | La lecture du montage, en vue **Projet** ou **Plan** (le plan sélectionné seul). |
| Panneau | Les réglages du plan sélectionné, ou ceux du projet (dimensions, cadence, fond). |
| Timeline | Les pistes vidéo et son, les plans, la tête de lecture et les courbes d'animation. |

## Monter

1. **Importer**

   Déposez des vidéos, des sons ou des images dans **Médias**, ou directement sur la timeline.

2. **Poser sur la timeline**

   Glissez un média sur une piste. Le déposer au-dessus des pistes existantes crée une nouvelle ligne au premier plan.

3. **Couper et arranger**

   Déplacez les plans, tirez leurs bords pour les raccourcir. Les **repères magnétiques** alignent les plans entre eux ; <kbd>Ctrl</kbd> pendant le déplacement les suspend.

4. **Exporter**

   **Exporter** ouvre la fenêtre d'export : format (MP4, WebM, MOV…), dimensions, qualité. L'encodage se fait dans le navigateur.

## Raccourcis

| Action | Raccourci |
| --- | --- |
| Couper à la tête de lecture | <kbd>S</kbd> |
| Dupliquer le plan | <kbd>Ctrl</kbd> + <kbd>D</kbd> |
| Supprimer le plan | <kbd>Suppr</kbd> |
| Annuler / Rétablir | <kbd>Ctrl</kbd> + <kbd>Z</kbd> / <kbd>Ctrl</kbd> + <kbd>Y</kbd> |

Le menu contextuel d'un plan propose aussi **Copier**, **Couper**, **Coller**, **Diviser** et **Détacher le son**.

## Pistes

Chaque piste peut être **masquée**, **coupée** (son), **verrouillée** ou réordonnée par glisser-déposer. Une piste vidéo a son **mode de fusion** avec ce qui se trouve derrière elle.

## Effets et animation

Les modules vidéo et image se posent en **effet** sur un plan. Leurs réglages sont **animables** : dépliez l'effet dans la timeline pour poser des images clés, puis affinez-les dans la vue **Courbes** ou la **Feuille**.

## Textes, solides et transitions

- **Textes** : déposez un texte sur une piste, puis réglez police, styles et animations dans le panneau du plan. Une composition de texte posée se modifie d'un double-clic.
- **Solides** : des aplats et formes à poser comme un plan.
- **Transitions** : à déposer sur un raccord entre deux plans qui se touchent, ou au début et à la fin d'une piste. Deux plans qui se chevauchent sur la même piste deviennent un fondu.

## Compositions

Une **composition** est un montage dans le montage. Sélectionnez des plans et **Précomposez**-les pour les regrouper ; ouvrez la composition pour la modifier, puis revenez au niveau supérieur par le fil des compositions ouvertes.

## Sous-titres

Le panneau **Sous-titres** propose trois départs :

- **Sous-titres automatiques** : le son du montage est transcrit par notre service. Choisissez la langue d'origine (ou la détection automatique) ; les sous-titres sont écrits dans la langue parlée. Le coût estimé, facturé à la minute entamée, s'affiche avant l'envoi.
- **Importer un fichier SRT / VTT**.
- **Écrire les sous-titres** à la main.

Les répliques se modifient ensuite une à une : couper au curseur, fusionner, attribuer un locuteur, ajuster le temps de chaque mot. **Exporter en .srt** enregistre le fichier de sous-titres.

> [!WARNING]
> **Envoyé au serveur**
>
> Dès que le panneau des sous-titres automatiques est ouvert, la pastille de confidentialité passe sur **Envoyé au serveur** : c'est le seul cas où l'éditeur vidéo transmet un contenu. Voir [Traitement local et serveur](../06-privacy.md).

## Enregistrer

L'onglet **Enregistrement** capture l'écran, la caméra et le micro, ensemble ou séparément, avec incrustation de la caméra dans un coin. Tout est capturé dans le navigateur ; les prises rejoignent les médias, prêtes à glisser sur le montage.
