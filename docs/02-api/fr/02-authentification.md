# Authentification

Créer, utiliser, protéger et révoquer une clé d'API.

Chaque appel à un module s'authentifie par une **clé d'API**, envoyée dans l'en-tête `X-API-Key`. Les points d'accès de lecture (`GET /v1/modules`, le schéma d'un module) et les liens de résultat signés n'en ont pas besoin.

```http
POST /v1/modules/blur HTTP/1.1
Host: api.pixlub.com
X-API-Key: pix.AbCdEf12.xxxxxxxxxxxxxxxxxxxxxxxx
Content-Type: multipart/form-data; boundary=…
```

## Créer une clé

1. **Ouvrir la section Développeur**

   [Paramètres → Espace de travail → Développeur](https://pixlub.com/fr/settings/workspace#developer). La section est réservée aux offres **Basique** et **Pro**.

2. **Créer la clé**

   **Créer une clé**, puis donnez-lui un nom qui dit où elle sert (« serveur de production », « script de nuit »).

3. **La copier tout de suite**

   La clé complète ne s'affiche qu'une fois. Pixlub n'en garde qu'une empreinte : elle ne pourra plus être relue.

Une clé a la forme `pix.<préfixe>.<secret>`. Le préfixe, visible dans la liste des clés, sert à la reconnaître ; seul le secret doit rester caché. La liste indique aussi la date de création et le dernier usage de chaque clé. Un compte peut avoir jusqu'à 20 clés actives.

## Révoquer une clé

**Révoquer** coupe la clé immédiatement : les appels suivants reçoivent `401`. Révoquez sans attendre une clé qui a fuité, puis créez-en une nouvelle.

## Bonnes pratiques

- **Une clé par usage** (un serveur, un script, un environnement) : on révoque l'une sans couper les autres.
- **Jamais dans le code source** ni dans un dépôt : variable d'environnement ou gestionnaire de secrets.
- **Jamais dans un navigateur ou une application mobile** : la clé y serait lisible par n'importe qui. Appelez l'API depuis votre serveur.
- **HTTPS uniquement**, et pas dans l'adresse : la clé voyage dans l'en-tête `X-API-Key`.

> [!WARNING]
> **Offre et clés**
>
> Si votre compte repasse sur l'offre gratuite, vos clés restent enregistrées mais les appels sont refusés avec `403` et le code `plan_required`.
