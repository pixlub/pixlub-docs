# SDK Python et Go

Les clients officiels : envoi des fichiers, téléchargement des résultats, erreurs typées et relances sûres.

Deux clients officiels enveloppent l'API : ils envoient les fichiers, téléchargent les résultats et transforment chaque refus en erreur typée. Ils lisent la clé dans `PIXLUB_API_KEY` et l'adresse de l'API dans `PIXLUB_BASE_URL`.

```bash
export PIXLUB_API_KEY="pix.xxxxxxxx.xxxxxxxxxxxxxxxx"
export PIXLUB_BASE_URL="https://api.pixlub.com"
```

## Installer

**Python**

```bash
pip install pixlub
```

**Go**

```bash
go get github.com/pixlub/pixlub-go
```

Python 3.9 ou plus récent (une seule dépendance : httpx) ; Go 1.23 ou plus récent (bibliothèque standard uniquement). Les deux SDK sont libres, sous licence MIT.

## Lancer un module

**Python**

```python
import pixlub

client = pixlub.Client()
result = client.tools.run("removeBgApi", image="photo.jpg")
result.save(f"photo-sans-fond{result.extension}")
print(result.cost, result.credits_balance)
```

**Go**

```go
client, err := pixlub.NewClient()
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "removeBgApi", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.jpg"),
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("photo-sans-fond"+result.Extension(), false)
```

Le SDK télécharge lui-même les fichiers produits. L'extension suit le fichier produit : `.webp` pour `removeBgApi`, `.png` pour la plupart des modules. `save` refuse d'écraser un fichier existant, sauf si vous le demandez.

## Réglages et entrées multiples

**Python**

```python
client.tools.run("flip", image="photo.jpg", params={"axis": "v"})
client.tools.run("mask", inputs={"image": "photo.png", "mask": "masque.png"})
```

**Go**

```go
client.Tools.Run(ctx, "flip", pixlub.RunRequest{
    Image:  pixlub.FromPath("photo.jpg"),
    Params: map[string]any{"axis": "v"},
})
client.Tools.Run(ctx, "mask", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("photo.png"),
        "mask":  pixlub.FromPath("masque.png"),
    },
})
```

`client.tools.list()` et `client.tools.schema(id)` (Python) lisent la liste des modules et le schéma de leurs réglages. En Python, `pixlub.AsyncClient` offre les mêmes méthodes en asynchrone.

## Erreurs

Chaque refus de l'API devient une erreur dédiée :

| HTTP | Python | Cas |
| --- | --- | --- |
| `400` | `InvalidRequestError` | Réglages invalides ; détail dans `details`. |
| `401` | `AuthenticationError` | Clé inconnue ou révoquée. |
| `402` | `InsufficientCreditsError` | Crédits insuffisants. |
| `403` | `PermissionDeniedError` | Offre gratuite (`code == "plan_required"`), lien expiré. |
| `429` | `RateLimitError` | Trop de requêtes : 30 lancements par minute, par rafales de 10. Jamais débité. |
| `5xx` | `ServerError` | Erreur de notre côté. |

Les erreurs locales (clé absente, fichier trop gros, entrée inconnue) sont levées **avant tout envoi** : elles ne coûtent rien.

## Relances

Le SDK ne relance **jamais** un appel qui a pu être débité. Il ne relance que ce qui n'a certainement pas tourné : les réponses `429`, les connexions refusées avant tout envoi, les lectures (`list`, `schema`) et les téléchargements de résultat. Après un délai dépassé ou une erreur `5xx` sur un appel, vérifiez votre solde avant de recommencer.

> [!NOTE]
> **Sécurité**
>
> Les SDK n'envoient la clé que dans l'en-tête `X-API-Key`, refusent le HTTP en clair hors `localhost`, ne suivent aucune redirection et ne joignent jamais la clé aux téléchargements.
