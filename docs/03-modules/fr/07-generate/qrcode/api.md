# QR code : référence API

Génère un QR code lisible par tout lecteur (lien, Wi-Fi, contact…), stylé, avec logo, ou fondu dans une image

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/qrcode` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `logo` (Image seule) | non | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Logo**<br />Image facultative posée au centre du QR code ; la correction monte à H en automatique. |
| `image` (Image seule) | non | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image facultative convertie en motif de QR code, dans laquelle le QR code se fond (mode « Dans une image ») ; sa transparence donne la silhouette. |

## Réglages

### Contenu

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `contentType` | `string` | `"url"` | `url` Lien : Adresse web ; `https://` est ajouté s'il manque.<br />`text` Texte : Texte libre.<br />`wifi` Wi-Fi : Connexion à un réseau Wi-Fi en un scan.<br />`email` E-mail : Prépare un e-mail : destinataire, objet, message.<br />`tel` Téléphone : Appelle un numéro.<br />`sms` SMS : Prépare un SMS.<br />`vcard` Contact (vCard) : Fiche de contact à enregistrer.<br />`geo` Position : Ouvre un point sur la carte. | **Type**<br />Ce que le QR code contient ; chaque type suit le format lu par les lecteurs courants. |
| `url` | `string` | `"https://pixlub.com"` |  | **Lien**<br />Adresse ouverte au scan.<br />*Pris en compte quand `contentType` = `url` (Lien).* |
| `text` | `string` | *chaîne vide* |  | **Texte**<br />Texte porté tel quel.<br />*Pris en compte quand `contentType` = `text` (Texte).* |
| `wifiSsid` | `string` | *chaîne vide* |  | **Nom du réseau (SSID)**<br />Nom du réseau Wi-Fi.<br />*Pris en compte quand `contentType` = `wifi` (Wi-Fi).* |
| `wifiSecurity` | `string` | `"WPA"` | `WPA` WPA/WPA2/WPA3<br />`WEP` WEP<br />`none` Aucune | **Sécurité**<br />Chiffrement du réseau.<br />*Pris en compte quand `contentType` = `wifi` (Wi-Fi).* |
| `wifiPassword` | `string` | *chaîne vide* |  | **Mot de passe**<br />Mot de passe du réseau, écrit en clair dans le QR code.<br />*Pris en compte quand `contentType` = `wifi` (Wi-Fi) et `wifiSecurity` = `WPA` (WPA/WPA2/WPA3) ou `WEP` (WEP).* |
| `wifiHidden` | `boolean` | `false` |  | **Réseau masqué**<br />Le réseau ne diffuse pas son nom.<br />*Pris en compte quand `contentType` = `wifi` (Wi-Fi).* |
| `vcardFirstName` | `string` | *chaîne vide* |  | **Prénom**<br />Prénom du contact.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `vcardLastName` | `string` | *chaîne vide* |  | **Nom**<br />Nom du contact.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `vcardOrg` | `string` | *chaîne vide* |  | **Organisation**<br />Société ou organisation.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `vcardTitle` | `string` | *chaîne vide* |  | **Fonction**<br />Poste occupé.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `emailTo` | `string` | *chaîne vide* |  | **E-mail**<br />Adresse e-mail.<br />*Pris en compte quand `contentType` = `email` (E-mail) ou `vcard` (Contact (vCard)).* |
| `phone` | `string` | *chaîne vide* |  | **Téléphone**<br />Numéro, au format international de préférence (+33…).<br />*Pris en compte quand `contentType` = `tel` (Téléphone) ou `sms` (SMS) ou `vcard` (Contact (vCard)).* |
| `emailSubject` | `string` | *chaîne vide* |  | **Objet**<br />Objet de l'e-mail.<br />*Pris en compte quand `contentType` = `email` (E-mail).* |
| `emailBody` | `string` | *chaîne vide* |  | **Message**<br />Corps de l'e-mail.<br />*Pris en compte quand `contentType` = `email` (E-mail).* |
| `smsMessage` | `string` | *chaîne vide* |  | **Message**<br />Texte du SMS.<br />*Pris en compte quand `contentType` = `sms` (SMS).* |
| `vcardUrl` | `string` | *chaîne vide* |  | **Site web**<br />Site du contact.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `vcardStreet` | `string` | *chaîne vide* |  | **Adresse**<br />Rue et numéro.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `vcardZip` | `string` | *chaîne vide* |  | **Code postal**<br />Code postal.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `vcardCity` | `string` | *chaîne vide* |  | **Ville**<br />Ville.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `vcardCountry` | `string` | *chaîne vide* |  | **Pays**<br />Pays.<br />*Pris en compte quand `contentType` = `vcard` (Contact (vCard)).* |
| `geoLat` | `number` | `48.8584` | min -90 ° · max 90 ° | **Latitude**<br />Latitude en degrés décimaux.<br />*Pris en compte quand `contentType` = `geo` (Position).* |
| `geoLng` | `number` | `2.2945` | min -180 ° · max 180 ° | **Longitude**<br />Longitude en degrés décimaux.<br />*Pris en compte quand `contentType` = `geo` (Position).* |

### Intégration

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `mode` | `string` | `"standard"` | `standard` Standard : QR code seul, sur son fond.<br />`shape` Dans une forme : Le QR code remplit une silhouette (cloche, cœur… ou celle de l'image reliée), prolongé par des modules du même dessin et cerné d'un contour.<br />`image` Dans une image : L'image reliée devient un motif de modules, ses tons et ses couleurs compris, et le QR code s'y fond. | **Mode**<br />Dans une forme : silhouette blanche cernée, remplie de modules comme le QR code. Dans une image : reliez une image à l'entrée Image, ses tons deviennent le motif. |

### Silhouette

> Ces réglages ne comptent que quand `mode` = `shape` (Dans une forme).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"cloche"` | `cloche` Cloche<br />`circle` Cercle<br />`roundedSquare` Carré arrondi<br />`heart` Cœur<br />`star` Étoile<br />`diamond` Losange<br />`hexagon` Hexagone<br />`shield` Écusson<br />`house` Maison<br />`cloud` Nuage<br />`bubble` Bulle<br />`pin` Repère<br />`drop` Goutte<br />`leaf` Feuille<br />`cup` Tasse<br />`tshirt` T-shirt<br />`gift` Cadeau<br />`bag` Sac<br />`cat` Chat<br />`paw` Patte<br />`image` Depuis l'image : Silhouette de l'image reliée à l'entrée Image. | **Forme**<br />Silhouette remplie par le QR code. « Depuis l'image » prend celle de l'image reliée : sa transparence, ou son contour pour un dessin au trait. |
| `outlineWidth` | `number` | `0.8` | min 0 · max 6 · pas de 0.1 | **Épaisseur du contour**<br />Épaisseur de la bordure autour de la silhouette, en modules ; 0 la retire. |
| `outlineCustom` | `boolean` | `false` |  | **Couleur propre du contour**<br />Sinon le contour prend la couleur (ou le dégradé) des modules. |
| `outlineColor` | `Color`<br />*Couleur unie* | `"#1c2535"` |  | **Couleur du contour**<br />Couleur du contour.<br />*Pris en compte quand `outlineCustom` = `true`.*<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |
| `patternDensity` | `number` | `50` | min 20 % · max 80 % · pas de 1 | **Densité du motif**<br />Part de modules sombres autour du QR code ; 50 % imite les données d'un QR code. |

### Placement

> Ces réglages ne comptent que quand `mode` = `image` (Dans une image) ou `shape` (Dans une forme).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `qrSize` | `number` | `85` | min 20 % · max 150 % · pas de 1 | **Taille du QR code**<br />Part du plus grand carré tenu dans la forme ; les modules du motif suivent.<br />*Pris en compte quand `mode` = `shape` (Dans une forme).* |
| `cellSize` | `number` | `12` | min 3 px · max 64 px · pas de 1 | **Taille des modules**<br />Côté d'un module en pixels de l'image : fixe la finesse du motif et la taille du QR code.<br />*Pris en compte quand `mode` = `image` (Dans une image).* |
| `qrX` | `number` | `50` | min 0 % · max 100 % · pas de 0.1 | **Position X**<br />Dans une image : centre du QR code, en part de la largeur. Dans une forme : décalage depuis sa place automatique (50 % = au milieu de la forme). Il s'aligne toujours sur la grille. |
| `qrY` | `number` | `50` | min 0 % · max 100 % · pas de 0.1 | **Position Y**<br />Comme la position X, sur la hauteur. |
| `halo` | `number` | `0` | min 0 · max 6 · pas de 1 | **Halo**<br />Modules clairs autour du QR code. À 0, le QR code se fond dans le motif sans bord. |
| `seed` | `number` | `1` | min 0 · max 9999 | **Variante**<br />Change le tirage du motif.<br />*Pris en compte quand `mode` = `shape` (Dans une forme), ou `mode` = `image` (Dans une image) et `convert` = `qr` (Motif QR).* |
| `finderGuard` | `boolean` | `true` |  | **Dégager les yeux**<br />Un liseré clair d'un module autour des trois yeux, côté image : c'est ce dont les lecteurs ont besoin pour trouver le code, le reste du bord reste fondu. |

### Conversion

> Ces réglages ne comptent que quand `mode` = `image` (Dans une image).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `convert` | `string` | `"qr"` | `qr` Motif QR : Texture aléatoire comme les données d'un QR code, plus dense dans les tons sombres : le QR code se fond dedans.<br />`threshold` Seuil : Aplats nets : logos, silhouettes.<br />`dither` Diffusion : Rend les dégradés et les photos.<br />`ordered` Trame : Trame régulière (Bayer). | **Méthode**<br />Comment les tons de l'image deviennent des modules sombres ou clairs. |
| `tone` | `number` | `70` | min 0 % · max 100 % · pas de 1 | **Relief des tons**<br />À 0, densité égale partout (silhouette seule, allure QR pure) ; plus haut, les tons de l'image se lisent dans la densité.<br />*Pris en compte quand `convert` = `qr` (Motif QR).* |
| `threshold` | `number` | `50` | min 0 % · max 100 % · pas de 1 | **Seuil**<br />Plus haut, plus de modules sombres. |
| `contrast` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Contraste**<br />Contraste de l'image avant conversion. |
| `invertImage` | `boolean` | `false` |  | **Inverser**<br />Les zones claires deviennent sombres. |
| `silhouette` | `boolean` | `true` |  | **Suivre la silhouette**<br />Hors des zones opaques de l'image, rien n'est dessiné. |
| `outline` | `boolean` | `true` |  | **Contour**<br />Le bord de la silhouette est tracé d'un trait de modules.<br />*Pris en compte quand `silhouette` = `true`.* |
| `colorSource` | `string` | `"qr"` | `qr` Du QR code<br />`image` De l'image | **Couleur des modules**<br />Couleur de tous les modules, motif et QR code compris : celle du QR code, ou celle de l'image sous chaque module, assombrie pour rester lisible. |

### Fusion

> Ces réglages ne comptent que quand `mode` = `image` (Dans une image).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `halftone` | `boolean` | `false` |  | **Image à travers le QR**<br />Chaque module est découpé en 3 × 3 : le centre porte la donnée, le reste montre l'image ; tout le motif passe à ce grain. |
| `halftoneStrength` | `number` | `50` | min 0 % · max 100 % · pas de 1 | **Force du QR**<br />Part de chaque module rendue au QR code autour de son centre : plus haut, plus lisible.<br />*Pris en compte quand `halftone` = `true`.* |
| `qrSolidBg` | `boolean` | `true` |  | **Fond plein sous le QR**<br />Le QR code et son halo gardent un fond opaque, même si le reste est transparent. |
| `backdropOpacity` | `number` | `0` | min 0 % · max 100 % · pas de 1 | **Image d'origine**<br />Montre l'image d'origine sous le motif ; baissez alors l'opacité du fond. |

### Modules

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `moduleShape` | `string` | `"square"` | `square` Carrés<br />`rounded` Fluide<br />`dots` Points<br />`squircle` Carrés arrondis<br />`diamond` Losanges<br />`star` Étoiles<br />`cross` Croix<br />`heart` Cœurs<br />`leaf` Feuilles<br />`vbars` Barres verticales<br />`hbars` Barres horizontales<br />`random` Confettis | **Forme**<br />Forme de chaque module (et des modules de l'image en mode intégré). |
| `moduleScale` | `number` | `100` | min 40 % · max 100 % · pas de 1 | **Taille**<br />Taille du module dans sa case ; sous 70 %, la lecture devient plus fragile.<br />*Pris en compte quand `moduleShape` = `square` (Carrés) ou `dots` (Points) ou `squircle` (Carrés arrondis) ou `diamond` (Losanges) ou `star` (Étoiles) ou `cross` (Croix) ou `heart` (Cœurs) ou `leaf` (Feuilles) ou `vbars` (Barres verticales) ou `hbars` (Barres horizontales) ou `random` (Confettis).* |
| `roundness` | `number` | `50` | min 0 % · max 100 % · pas de 1 | **Arrondi**<br />Rondeur des coins.<br />*Pris en compte quand `moduleShape` = `rounded` (Fluide) ou `squircle` (Carrés arrondis) ou `leaf` (Feuilles) ou `vbars` (Barres verticales) ou `hbars` (Barres horizontales).* |

### Yeux

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `eyeFrame` | `string` | `"square"` | `square` Carré<br />`rounded` Arrondi<br />`circle` Cercle<br />`leaf` Feuille<br />`shape` Comme les modules | **Cadre**<br />Forme du cadre des trois yeux de repérage et des petits motifs d'alignement. « Comme les modules » avec des formes détachées (points…) gêne les lecteurs. |
| `eyeBall` | `string` | `"square"` | `square` Carré<br />`rounded` Arrondi<br />`circle` Rond<br />`diamond` Losange<br />`leaf` Feuille<br />`star` Étoile<br />`shape` Comme les modules | **Centre**<br />Forme du centre des yeux. Pour la lecture la plus sûre, gardez la même famille que le cadre : carré ou arrondi avec un cadre carré ou arrondi, rond ou losange avec un cadre rond. |
| `eyeCustom` | `boolean` | `false` |  | **Couleurs propres**<br />Donne aux yeux leurs propres couleurs. |
| `eyeFrameColor` | `Color`<br />*Couleur unie* | `"#1c2535"` |  | **Couleur du cadre**<br />Couleur du cadre des yeux.<br />*Pris en compte quand `eyeCustom` = `true`.*<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |
| `eyeBallColor` | `Color`<br />*Couleur unie* | `"#1c2535"` |  | **Couleur du centre**<br />Couleur du centre des yeux.<br />*Pris en compte quand `eyeCustom` = `true`.*<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |

### Couleurs

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Couleur ou dégradé* | `"#000000"` |  | **Modules**<br />Couleur ou dégradé des modules ; gardez-la nettement plus sombre que le fond.<br />*Couleur ou dégradé* : Une couleur CSS (`"#ff8800"`) pour un aplat, ou un objet `ColorGradient` pour un dégradé.<br />Structure de Color \| ColorGradient et exemple : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `fgOpacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité des modules**<br />Transparence des modules. |
| `background` | `Color`<br />*Couleur unie* | `"#ffffff"` |  | **Fond**<br />Couleur du fond (cases claires).<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |
| `bgOpacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité du fond**<br />À 0 %, le fond est transparent. |
| `bgRadius` | `number` | `0` | min 0 % · max 50 % · pas de 1 | **Coins du fond**<br />Arrondi des coins du fond.<br />*Pris en compte quand `mode` = `standard` (Standard).* |

### Dimensions

> Ces réglages ne comptent que quand `mode` = `standard` (Standard) ou `shape` (Dans une forme).

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `size` | `number` | `1024` | min 64 px · max 4096 px · pas de 1 | **Taille**<br />Côté de l'image, marge comprise. |
| `margin` | `number` | `4` | min 0 · max 20 · pas de 1 | **Marge (modules)**<br />Zone claire autour du code ; la norme en demande 4 modules.<br />*Pris en compte quand `mode` = `standard` (Standard).* |

### Logo

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `logoSize` | `number` | `22` | min 5 % · max 40 % · pas de 1 | **Taille**<br />Côté du logo, en part du QR code. Avec « Taille sûre », il est ramené à la plus grande taille que la correction d'erreur sait réparer. |
| `logoSafe` | `boolean` | `true` |  | **Taille sûre**<br />Compte les mots de code cachés par le logo, bloc par bloc, et réduit le logo tant qu'il en cache trop : le lien reste lisible. Montez la correction à H pour un logo plus grand. |
| `logoShape` | `string` | `"rounded"` | `none` Aucune<br />`square` Carrée<br />`rounded` Arrondie<br />`circle` Ronde | **Plaque**<br />Forme posée sous le logo ; le logo y est découpé. |
| `logoBg` | `Color`<br />*Couleur unie* | `"#ffffff"` |  | **Couleur de la plaque**<br />Couleur de la plaque sous le logo.<br />*Pris en compte quand `logoShape` = `square` (Carrée) ou `rounded` (Arrondie) ou `circle` (Ronde).*<br />*Couleur unie* : Couleur CSS : `#rrggbb`, `#rrggbbaa`, `rgb()` ou `hsl()`. |
| `logoPadding` | `number` | `1` | min 0 · max 4 · pas de 0.5 | **Marge**<br />Espace autour du logo, en modules. |
| `logoClear` | `boolean` | `true` |  | **Dégager les modules**<br />Retire les modules cachés par le logo, pour un bord net. |
| `logoOpacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité**<br />Transparence du logo. |

### Encodage

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `ecl` | `string` | `"auto"` | `auto` Auto : M, ou H dès qu'un logo ou la demi-teinte cache des modules.<br />`L` L · 7 % : Code le plus petit, le moins robuste.<br />`M` M · 15 % : Usage courant.<br />`Q` Q · 25 % : Résiste aux salissures et petits logos.<br />`H` H · 30 % : Le plus robuste : logo, style marqué, intégration. | **Correction d'erreur**<br />Part du code qui peut manquer sans gêner la lecture ; plus haute, le code est plus dense. Elle monte d'elle-même tant que la taille ne change pas. |
| `minVersion` | `number` | `1` | min 1 · max 40 · pas de 1 | **Version minimale**<br />Taille minimale de la grille (1 = 21 × 21 modules, +4 par version) ; utile pour un motif plus fin ou une grille fixe. |
| `mask` | `string` | `"auto"` | `auto` Auto<br />`0` 0<br />`1` 1<br />`2` 2<br />`3` 3<br />`4` 4<br />`5` 5<br />`6` 6<br />`7` 7 | **Masque**<br />Motif qui brouille les données ; Auto retient le plus lisible, un numéro fixe change l'allure du code. |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/qrcode \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F logo=@logo.png \
  -F 'params={"contentType":"url","url":"https://pixlub.com","mode":"standard"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('logo', await openAsBlob('logo.png'), 'logo.png')
form.append('params', JSON.stringify({"contentType":"url","url":"https://pixlub.com","mode":"standard"}))

const res = await fetch('https://api.pixlub.com/v1/modules/qrcode', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/qrcode",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("logo", open("logo.png", "rb"))],
    data={"params": json.dumps({"contentType": "url", "url": "https://pixlub.com", "mode": "standard"})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("qrcode", inputs={"logo": "logo.png"}, params={"contentType": "url", "url": "https://pixlub.com", "mode": "standard"})
result.save(f"qrcode{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "qrcode", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "logo": pixlub.FromPath("logo.png"),
    },
    Params: map[string]any{"contentType": "url", "url": "https://pixlub.com", "mode": "standard"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("qrcode"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produite par le module. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "qrcode",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 1,
    "balance": 190
  }
}
```

## Types

Les valeurs structurées des réglages, détaillées comme des classes : chaque membre avec son type, puis un exemple.

<a name="type-colorgradient"></a>

### ColorGradient

*Objet*. Dégradé de couleurs : des arrêts placés le long d'un axe, et la façon de les étaler.

| Membre | Type | Description |
| --- | --- | --- |
| `stops` | `GradientStop[]` | Arrêts de couleur, au moins deux, dans n'importe quel ordre. |
| `type` | `"linear" \| "radial"` | *facultatif* · Linéaire le long de `angle`, ou en cercles depuis le centre. `linear` par défaut ; sans effet quand seul l'ordre des couleurs compte (Mappe dégradé). |
| `angle` | `number` | *facultatif* · Direction d'un dégradé linéaire, en degrés : 0 vers le haut, 90 vers la droite. `90` par défaut. |

**Exemple**

```json
{
  "type": "linear",
  "angle": 90,
  "stops": [
    {
      "color": "#140a2e",
      "at": 0
    },
    {
      "color": "#c264c2",
      "at": 55
    },
    {
      "color": "#ffffff",
      "at": 100
    }
  ]
}
```

<a name="type-gradientstop"></a>

### GradientStop

*Objet*. Arrêt d'un dégradé.

| Membre | Type | Description |
| --- | --- | --- |
| `color` | `Color` | Couleur CSS de l'arrêt ; l'alpha (`#rrggbbaa`) est gardé. |
| `at` | `number` | Position de l'arrêt, de 0 (début) à 100 (fin), en %. |

**Exemple**

```json
{
  "color": "#c264c2",
  "at": 55
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/qrcode/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "contentType": {
      "title": "Type",
      "default": "url",
      "type": "string",
      "enum": [
        "url",
        "text",
        "wifi",
        "email",
        "tel",
        "sms",
        "vcard",
        "geo"
      ]
    },
    "url": {
      "title": "Link",
      "default": "https://pixlub.com",
      "type": "string"
    },
    "wifiSsid": {
      "title": "Network name (SSID)",
      "default": "",
      "type": "string"
    },
    "wifiSecurity": {
      "title": "Security",
      "default": "WPA",
      "type": "string",
      "enum": [
        "WPA",
        "WEP",
        "none"
      ]
    },
    "wifiPassword": {
      "title": "Password",
      "default": "",
      "type": "string"
    },
    "wifiHidden": {
      "title": "Hidden network",
      "default": false,
      "type": "boolean"
    },
    "vcardFirstName": {
      "title": "First name",
      "default": "",
      "type": "string"
    },
    "vcardLastName": {
      "title": "Last name",
      "default": "",
      "type": "string"
    },
    "vcardOrg": {
      "title": "Organization",
      "default": "",
      "type": "string"
    },
    "vcardTitle": {
      "title": "Job title",
      "default": "",
      "type": "string"
    },
    "emailTo": {
      "title": "Email",
      "default": "",
      "type": "string"
    },
    "phone": {
      "title": "Phone",
      "default": "",
      "type": "string"
    },
    "emailSubject": {
      "title": "Subject",
      "default": "",
      "type": "string"
    },
    "vcardUrl": {
      "title": "Website",
      "default": "",
      "type": "string"
    },
    "vcardStreet": {
      "title": "Street",
      "default": "",
      "type": "string"
    },
    "vcardZip": {
      "title": "Postal code",
      "default": "",
      "type": "string"
    },
    "vcardCity": {
      "title": "City",
      "default": "",
      "type": "string"
    },
    "vcardCountry": {
      "title": "Country",
      "default": "",
      "type": "string"
    },
    "geoLat": {
      "title": "Latitude",
      "default": 48.8584,
      "type": "number",
      "minimum": -90,
      "maximum": 90
    },
    "geoLng": {
      "title": "Longitude",
      "default": 2.2945,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "mode": {
      "title": "Mode",
      "default": "standard",
      "type": "string",
      "enum": [
        "standard",
        "shape",
        "image"
      ]
    },
    "outlineWidth": {
      "title": "Outline thickness",
      "default": 0.8,
      "type": "number",
      "minimum": 0,
      "maximum": 6,
      "multipleOf": 0.1
    },
    "outlineCustom": {
      "title": "Own outline color",
      "default": false,
      "type": "boolean"
    },
    "outlineColor": {
      "title": "Outline color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "patternDensity": {
      "title": "Pattern density",
      "default": 50,
      "type": "number",
      "minimum": 20,
      "maximum": 80,
      "multipleOf": 1
    },
    "qrSize": {
      "title": "QR code size",
      "default": 85,
      "type": "number",
      "minimum": 20,
      "maximum": 150,
      "multipleOf": 1
    },
    "cellSize": {
      "title": "Module size",
      "default": 12,
      "type": "number",
      "minimum": 3,
      "maximum": 64,
      "multipleOf": 1
    },
    "qrX": {
      "title": "Position X",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "qrY": {
      "title": "Position Y",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "halo": {
      "title": "Halo",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 6,
      "multipleOf": 1
    },
    "seed": {
      "title": "Variant",
      "default": 1,
      "type": "number",
      "minimum": 0,
      "maximum": 9999
    },
    "finderGuard": {
      "title": "Clear the eyes",
      "default": true,
      "type": "boolean"
    },
    "convert": {
      "title": "Method",
      "default": "qr",
      "type": "string",
      "enum": [
        "qr",
        "threshold",
        "dither",
        "ordered"
      ]
    },
    "tone": {
      "title": "Tone depth",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "threshold": {
      "title": "Threshold",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "contrast": {
      "title": "Contrast",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "invertImage": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "silhouette": {
      "title": "Follow the silhouette",
      "default": true,
      "type": "boolean"
    },
    "outline": {
      "title": "Outline",
      "default": true,
      "type": "boolean"
    },
    "colorSource": {
      "title": "Module color",
      "default": "qr",
      "type": "string",
      "enum": [
        "qr",
        "image"
      ]
    },
    "halftone": {
      "title": "Image through the QR",
      "default": false,
      "type": "boolean"
    },
    "halftoneStrength": {
      "title": "QR strength",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "qrSolidBg": {
      "title": "Solid background under the QR",
      "default": true,
      "type": "boolean"
    },
    "backdropOpacity": {
      "title": "Original image",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "moduleScale": {
      "title": "Size",
      "default": 100,
      "type": "number",
      "minimum": 40,
      "maximum": 100,
      "multipleOf": 1
    },
    "roundness": {
      "title": "Roundness",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "eyeCustom": {
      "title": "Own colors",
      "default": false,
      "type": "boolean"
    },
    "eyeFrameColor": {
      "title": "Frame color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "eyeBallColor": {
      "title": "Center color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "color": {
      "title": "Modules",
      "default": "#000000",
      "anyOf": [
        {
          "type": "string",
          "minLength": 1
        },
        {
          "type": "object",
          "required": [
            "stops"
          ],
          "properties": {
            "stops": {
              "type": "array",
              "items": {
                "type": "object",
                "required": [
                  "color",
                  "at"
                ],
                "properties": {
                  "color": {
                    "type": "string",
                    "minLength": 1
                  },
                  "at": {
                    "type": "number",
                    "minimum": 0,
                    "maximum": 100
                  }
                }
              },
              "minItems": 2
            },
            "type": {
              "type": "string",
              "enum": [
                "linear",
                "radial"
              ]
            },
            "angle": {
              "type": "number"
            }
          }
        }
      ]
    },
    "fgOpacity": {
      "title": "Module opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "background": {
      "title": "Background",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    },
    "bgOpacity": {
      "title": "Background opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "bgRadius": {
      "title": "Background corners",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 50,
      "multipleOf": 1
    },
    "size": {
      "title": "Size",
      "default": 1024,
      "type": "number",
      "minimum": 64,
      "maximum": 4096,
      "multipleOf": 1
    },
    "margin": {
      "title": "Margin (modules)",
      "default": 4,
      "type": "number",
      "minimum": 0,
      "maximum": 20,
      "multipleOf": 1
    },
    "logoSize": {
      "title": "Size",
      "default": 22,
      "type": "number",
      "minimum": 5,
      "maximum": 40,
      "multipleOf": 1
    },
    "logoSafe": {
      "title": "Safe size",
      "default": true,
      "type": "boolean"
    },
    "logoShape": {
      "title": "Plate",
      "default": "rounded",
      "type": "string",
      "enum": [
        "none",
        "square",
        "rounded",
        "circle"
      ]
    },
    "logoBg": {
      "title": "Plate color",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    },
    "logoPadding": {
      "title": "Padding",
      "default": 1,
      "type": "number",
      "minimum": 0,
      "maximum": 4,
      "multipleOf": 0.5
    },
    "logoClear": {
      "title": "Clear the modules",
      "default": true,
      "type": "boolean"
    },
    "logoOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "ecl": {
      "title": "Error correction",
      "default": "auto",
      "type": "string",
      "enum": [
        "auto",
        "L",
        "M",
        "Q",
        "H"
      ]
    },
    "minVersion": {
      "title": "Minimum version",
      "default": 1,
      "type": "number",
      "minimum": 1,
      "maximum": 40,
      "multipleOf": 1
    },
    "mask": {
      "title": "Mask",
      "default": "auto",
      "type": "string",
      "enum": [
        "auto",
        "0",
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7"
      ]
    },
    "text": {
      "type": "string",
      "default": ""
    },
    "emailBody": {
      "type": "string",
      "default": ""
    },
    "smsMessage": {
      "type": "string",
      "default": ""
    },
    "moduleShape": {
      "type": "string",
      "default": "square"
    },
    "eyeFrame": {
      "type": "string",
      "default": "square"
    },
    "eyeBall": {
      "type": "string",
      "default": "square"
    },
    "shape": {
      "type": "string",
      "default": "cloche"
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
