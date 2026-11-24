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
| Lire / Pause | <kbd>Espace</kbd> |
| Image précédente / suivante | <kbd>←</kbd> / <kbd>→</kbd> |
| Reculer / avancer de 10 images | <kbd>Maj</kbd> + <kbd>←</kbd> / <kbd>Maj</kbd> + <kbd>→</kbd> |
| Raccord précédent / suivant | <kbd>Ctrl</kbd> + <kbd>←</kbd> / <kbd>Ctrl</kbd> + <kbd>→</kbd> |
| Début / fin du montage | <kbd>Début</kbd> / <kbd>Fin</kbd> |
| Lecture en boucle | <kbd>L</kbd> |
| Couper le son | <kbd>M</kbd> |
| Diviser à la tête de lecture | <kbd>S</kbd> |
| Rogner le début / la fin jusqu'à la tête de lecture | <kbd>Q</kbd> / <kbd>W</kbd> |
| Couper / Copier / Coller | <kbd>Ctrl</kbd> + <kbd>X</kbd> / <kbd>Ctrl</kbd> + <kbd>C</kbd> / <kbd>Ctrl</kbd> + <kbd>V</kbd> |
| Dupliquer le plan | <kbd>Ctrl</kbd> + <kbd>D</kbd> |
| Tout sélectionner | <kbd>Ctrl</kbd> + <kbd>A</kbd> |
| Supprimer le plan | <kbd>Suppr</kbd> |
| Détacher le son | <kbd>Ctrl</kbd> + <kbd>Maj</kbd> + <kbd>D</kbd> |
| Précomposer | <kbd>Ctrl</kbd> + <kbd>Maj</kbd> + <kbd>C</kbd> |
| Annuler / Rétablir | <kbd>Ctrl</kbd> + <kbd>Z</kbd> / <kbd>Ctrl</kbd> + <kbd>Maj</kbd> + <kbd>Z</kbd> |
| Zoom de la timeline | <kbd>Ctrl</kbd> + <kbd>+</kbd> / <kbd>Ctrl</kbd> + <kbd>-</kbd> |
| Ajuster la timeline | <kbd>Maj</kbd> + <kbd>1</kbd> |
| Vue du plan seul | <kbd>Alt</kbd> + <kbd>V</kbd> |
| Repères magnétiques | <kbd>Alt</kbd> + <kbd>G</kbd> |
| Moniteur en plein cadre | <kbd>F</kbd> |
| Nouveau projet | <kbd>Alt</kbd> + <kbd>N</kbd> |
| Ouvrir un fichier / depuis le stockage | <kbd>Ctrl</kbd> + <kbd>O</kbd> / <kbd>Ctrl</kbd> + <kbd>Maj</kbd> + <kbd>O</kbd> |
| Enregistrer | <kbd>Ctrl</kbd> + <kbd>S</kbd> |
| Exporter | <kbd>Ctrl</kbd> + <kbd>E</kbd> |

Toutes ces commandes se retrouvent, avec leur raccourci, dans les menus **Fichier**, **Édition**, **Plan**, **Lecture** et **Affichage** de la barre du haut. Le menu **MCP** montre l'état de la liaison avec une IA connectée et ouvre ses options.

Le menu contextuel d'un plan propose aussi **Copier**, **Couper**, **Coller**, **Diviser** et **Détacher le son**.

## Pistes

Chaque piste peut être **masquée**, **coupée** (son), **verrouillée** ou réordonnée par glisser-déposer. Une piste vidéo a son **mode de fusion** avec ce qui se trouve derrière elle.

## Effets et animation

Les modules vidéo et image se posent en **effet** sur un plan. Leurs réglages sont **animables** : dépliez l'effet dans la timeline pour poser des images clés, puis affinez-les dans la vue **Courbes** ou la **Feuille**.

## Textes, solides et transitions

- **Textes** : déposez un texte sur une piste, puis réglez police, styles et animations dans le panneau du plan. Une composition de texte posée se modifie d'un double-clic.
- **Solides** : des aplats et formes à poser comme un plan.
- **Effets** : des effets visuels prêts à poser par-dessus un plan — ondes de clic, glissés, lumières, éclats, repères, ambiances. Chacun est une composition de formes, de particules et d'images clés : un double-clic l'ouvre pour en changer les couleurs, les formes ou le rythme.
- **Sons** : près de deux cents bruitages rangés par thème — clics, interface, alertes, souffles, impacts, montées, magie, jeu rétro, science-fiction, cartoon, ambiances. Un clic écoute le son, un glissé le pose sur une piste. Chaque bruitage est synthétisé dans votre navigateur : aucun fichier n'est téléchargé, aucune musique n'est fournie.
- **Transitions** : à déposer sur un raccord entre deux plans qui se touchent, ou au début et à la fin d'une piste. Deux plans qui se chevauchent sur la même piste deviennent un fondu.

## Compositions

Une **composition** est un montage dans le montage. Sélectionnez des plans et **Précomposez**-les pour les regrouper ; ouvrez la composition pour la modifier, puis revenez au niveau supérieur par le fil des compositions ouvertes.

## Suivi de mouvement

Le **suivi de mouvement** accroche un texte, une image ou une forme à un élément qui bouge dans une vidéo ou une image animée. L'analyse se fait dans le navigateur : rien n'est envoyé.

1. **Ouvrir l'outil**

   Clic droit sur la vidéo, dans la timeline ou l'aperçu, puis **Outils → Suivi de mouvement**. La même entrée se trouve dans le menu **Édition**, et en icône en haut de l'aperçu quand le plan sélectionné s'y prête. Le panneau de droite montre alors l'outil ; **Réglages du plan**, en haut, en ressort.

2. **Choisir quoi suivre**

   **Point** pour un élément qui se déplace seulement, **Objet** pour un élément qui tourne, s'approche ou s'éloigne, **Surface** pour une surface plane vue de biais (écran, affiche, mur) dont vous placez les quatre coins.

3. **Placer le cadre bleu**

   Un cadre est déjà posé sur l'aperçu. Glissez-le sur l'élément et tirez ses coins pour l'entourer : une zone contrastée se suit mieux qu'un aplat.

4. **Lancer le suivi**

   **Lancer le suivi** analyse tout le plan depuis l'image affichée. La barre montre ce qui est suivi ; cliquez-la pour aller à une image.

5. **Attacher un élément**

   Les plans posés au-dessus de la vidéo sont listés : un interrupteur attache chacun au cadre. L'élément garde la place qu'il a sur l'image affichée, puis suit ; vous pouvez toujours le déplacer, l'agrandir ou le tourner. **Orienter selon la trajectoire** le fait tourner avec la direction du déplacement, comme une flèche sur son chemin.

Le cadre se dessine et se saisit aussi autour de l'image : pour cadrer un élément qui sort du champ, dézoomez l'aperçu et tirez ses coins au-delà du bord. En mode **Objet**, le cadre pivote en le saisissant juste à l'extérieur d'un coin. Sur la timeline, une icône de cible marque le plan suivi, et une cible pleine le plan attaché.

**Si le cadre perd l'élément** (il passe derrière un obstacle, sort de l'image), le suivi s'arrête et le cadre devient rouge. Avancez jusqu'à l'image où l'élément réapparaît et replacez le cadre dessus : le suivi reprend tout seul, et le passage caché est comblé. Pour corriger un suivi qui a glissé, replacez le cadre sur une image puis choisissez **Corriger la suite** ou **Corriger avant**.

### Ajuster un passage à la main

Le suivi trace une **ligne** : le chemin que parcourt le centre du cadre. Quand il glisse, **Ajuster à la main** permet de retoucher cette ligne sans relancer l'analyse. Une palette d'outils descend alors en haut de l'aperçu ; le cadre, lui, ne se déplace plus à la main — il reste réservé au suivi automatique.

Le plus rapide est de rendre **tout un passage** éditable d'un seul geste : glissez sur la barre du suivi dans le panneau (de 1 s à 3 s, par exemple), ou le long de la ligne avec l'outil **Tronçon**. Le passage devient une seule courbe orange, tenue par quelques points placés là où la trajectoire change ; sa forme ne bouge pas tant que vous n'y touchez pas.

- **Sélection** : tirez un point pour le déplacer — l'aperçu se cale sur son image, pour le placer en voyant ce qu'il doit suivre. Un point choisi montre ses deux **poignées** : tirez-les pour régler la courbure. <kbd>Maj</kbd> + clic ou un cadre tracé dans le vide choisit plusieurs points, qui se déplacent ensemble.
- **Point** : cliquez la ligne pour y ajouter un point. Dans un passage, la courbe est coupée en deux sans changer de forme.
- **Point en courbe** garde les deux poignées alignées ; **Point en angle** les rend indépendantes (<kbd>Alt</kbd> en tirant une poignée fait de même).
- **Lisser** redonne aux points choisis les poignées d'une courbe régulière ; **Supprimer** les retire, et là où plus rien ne la couvre, la ligne redevient celle de l'analyse.

Si le premier ou le dernier point d'un passage s'écarte du suivi, les images voisines le rejoignent en douceur : pas de saut à la jonction. Le passage retouché apparaît en orange sur la ligne et dans la barre. **Reprendre le suivi automatique d'ici** relance l'analyse depuis l'image affichée en gardant vos points ; en parcourant la timeline, la tête de lecture s'accroche aux points tout proches.

### Attacher à un plan

Pour un élément animé par des clés (un texte, une forme, une image qui se déplace sur la timeline), rien n'est à analyser : **Outils → Attacher à un plan** fait reprendre à un plan le mouvement d'un autre. Choisissez le plan porteur, puis ce qui est repris — **la position** seule, ou **tout le mouvement** (position, échelle, rotation). Le plan attaché garde la place qu'il a sur la première image où les deux se voient ; il reste déplaçable et animable, et peut s'orienter selon la trajectoire.

### Lier deux plans sur la timeline

Chaque plan porte, en bas de son bloc, les icônes de ses outils. Tirez l'icône **maillon** d'un plan vers un autre pour l'y attacher ; tirez l'icône **cible** d'un plan suivi vers un autre plan pour attacher celui-ci à l'élément suivi (si le plan en suit plusieurs, un petit menu demande lequel). Pendant le geste, seuls les plans qui croisent celui de départ restent en couleur ; relâcher ailleurs ne change rien. Un simple clic sur l'icône ouvre l'outil. Dans les panneaux, cliquer le nom d'un plan le retrouve dans la timeline, où il brille un instant.

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
