# Python and Go SDKs

The official clients: file uploads, result downloads, typed errors and safe retries.

Two official clients wrap the API: they upload files, download results and turn every refusal into a typed error. They read the key from `PIXLUB_API_KEY` and the API address from `PIXLUB_BASE_URL`.

```bash
export PIXLUB_API_KEY="pix.xxxxxxxx.xxxxxxxxxxxxxxxx"
export PIXLUB_BASE_URL="https://api.pixlub.com"
```

## Installing

**Python**

```bash
pip install pixlub
```

**Go**

```bash
go get github.com/pixlub/pixlub-go
```

Python 3.9 or later (one dependency: httpx); Go 1.23 or later (standard library only). Both SDKs are open source, under the MIT license.

## Running a module

**Python**

```python
import pixlub

client = pixlub.Client()
result = client.tools.run("removeBgApi", image="photo.jpg")
result.save(f"photo-nobg{result.extension}")
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
err = result.Save("photo-nobg"+result.Extension(), false)
```

The SDK downloads the produced files itself. The extension follows the produced file: `.webp` for `removeBgApi`, `.png` for most modules. `save` refuses to overwrite an existing file unless you ask it to.

## Settings and multiple inputs

**Python**

```python
client.tools.run("flip", image="photo.jpg", params={"axis": "v"})
client.tools.run("mask", inputs={"image": "photo.png", "mask": "mask.png"})
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
        "mask":  pixlub.FromPath("mask.png"),
    },
})
```

`client.tools.list()` and `client.tools.schema(id)` (Python) read the module list and their settings schema. In Python, `pixlub.AsyncClient` offers the same methods asynchronously.

## Errors

Every API refusal becomes a dedicated error:

| HTTP | Python | Case |
| --- | --- | --- |
| `400` | `InvalidRequestError` | Invalid settings; details in `details`. |
| `401` | `AuthenticationError` | Unknown or revoked key. |
| `402` | `InsufficientCreditsError` | Not enough credits. |
| `403` | `PermissionDeniedError` | Free plan (`code == "plan_required"`), expired link. |
| `429` | `RateLimitError` | Too many requests: 30 runs a minute, bursts of 10. Never charged. |
| `5xx` | `ServerError` | Error on our side. |

Local errors (missing key, file too large, unknown input) are raised **before anything is sent**: they cost nothing.

## Retries

The SDK **never** retries a call that may have been charged. It only retries what certainly did not run: `429` responses, connections refused before anything was sent, reads (`list`, `schema`) and result downloads. After a timeout or a `5xx` error on a call, check your balance before trying again.

> [!NOTE]
> **Security**
>
> The SDKs only send the key in the `X-API-Key` header, refuse plain HTTP except on `localhost`, never follow redirects and never attach the key to downloads.
