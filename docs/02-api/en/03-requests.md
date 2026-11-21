# Requests and responses

Endpoints, request format, multiple inputs, the settings schema and the response.

## Endpoints

| Method | Path | Key | Role |
| --- | --- | --- | --- |
| `GET` | `/v1/modules` | no | List of modules and their inputs. |
| `GET` | `/v1/modules/:id/schema` | no | JSON Schema of a module's settings. |
| `POST` | `/v1/modules/:id` | yes | Runs a module. |
| `POST` | `/v1/uploads` | yes | Opens a deposit for a large file ([Large files](./035-large-files.md)). |
| `GET` | `/v1/jobs/:id` | yes | Follows a long job ([Long jobs](./035-large-files.md)). |
| `GET` | `/v1/results/:name` | no (signed link) | Downloads a produced file. |
| `GET` | `/healthz` | no | Service health. |

Every path starts from `https://api.pixlub.com`.

## Listing modules

```json
[
  {
    "id": "mask",
    "name": "Mask",
    "description": "Applies a mask to an image.",
    "category": "compose",
    "executable": true,
    "handler": "local",
    "inputs": [
      { "id": "image", "label": "Image", "type": "image", "required": true, "multiple": false, "per_file": false, "max_files": 1, "accept": ["image/png", "image/jpeg", "image/webp", "image/gif", "image/avif", "image/bmp"] },
      { "id": "mask", "label": "Mask", "type": "image", "required": true, "multiple": false, "per_file": false, "max_files": 1, "accept": ["image/png", "image/jpeg", "image/webp", "image/gif", "image/avif", "image/bmp"] }
    ],
    "outputs": [
      { "key": "out", "label": "Image(s)", "kind": "image", "multiple": false, "content_types": ["image/png"] }
    ]
  }
]
```

`executable` says whether the API can run the module; `handler` is `local` (computed by the API) or `remote` (AI service). Each input states the formats it accepts (`accept`) and how many files it takes (`max_files`, with `per_file` when each file is processed on its own); each output, the key its file comes back under (`key`). Non-executable modules (video, 3D, graph building blocks) remain usable on the site.

## Sending a request

A call is a `multipart/form-data` request:

- **one field per input**, named after the input `id`, holding the file; a list input (`multiple`) **repeats its field**, once per file;
- **a `params` field**, a JSON string with the settings.

```bash
curl -X POST https://api.pixlub.com/v1/modules/mask \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@photo.png \
  -F mask=@mask.png \
  -F 'params={}'
```

Files are at most **25 MB** each in the request (beyond that, or for a file already online: [Large files](./035-large-files.md)); a request carries **8** batch files at most, or up to **64** images processed one by one (see below). What an input receives depends on its type:

| Input type | Files | What the module reads |
| --- | --- | --- |
| `image` | One, or several when `per_file` is `true` | The image; each image sent is processed on its own. |
| `channel` | One | Its grayscale value, like the `r`, `g`, `b`, `a` inputs of `channelMerge`. |
| `batch` | A list: the field repeats | The images in sending order, like the `overlay` input of `merge` (`-F overlay=@a.png -F overlay=@b.png`). |

### Accepted formats

Each input names its formats, listed in the **API** view of each [module page](../../03-modules/en/README.md) and in `accept` of `GET /v1/modules`:

- a module computed by the API reads **PNG, JPEG, WebP, GIF, AVIF and BMP**;
- an AI module (`handler` = `remote`) reads **PNG, JPEG, WebP and GIF**, sometimes fewer (photos only for face detection).

The format is read **from the file content**, never from its name or declared type. Any other format is refused (`400`, `unsupported_format`), as is a single field that receives several files (`too_many_files`).

### Several images in one call

Most modules with a single image input (`resize`, `blur`, `convert`…) accept **several images**: repeat the field, once per image. Each image is processed **on its own**, with the same settings, like the batch on the module page of the site. `GET /v1/modules` flags it with `per_file: true` on the input.

```bash
curl -X POST https://api.pixlub.com/v1/modules/resize \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@photo-1.png \
  -F in=@photo-2.jpg \
  -F 'params={"size":{"width":800}}'
```

- **Cost**: the module price **per image**, charged **at once** before the first render. If the balance does not cover the whole batch, nothing runs (`402`, `required` gives the total cost); a failure on our side refunds everything.
- **Count**: your plan sets how many images a call may carry (the same cap as batches on the site), **64** at most. Beyond your plan: `403`, `batch_limit`, with the cap in `limit`.
- **Response**: each output comes back numbered in upload order, `out#0`, `out#1`… (`r#0`, `g#0`, `b#0`, `r#1`… for `splitRgb`). A single image keeps its key (`out`).

## Settings

- A **missing** setting takes its default value. `params` may be omitted or be `{}`.
- An **unknown** setting is refused: the list is closed.
- **Types are strict**: `"12"` is not a number. A value out of range or outside the allowed list is refused.

The exact schema, with types, limits, steps and defaults, is available at `GET /v1/modules/:id/schema`, and in the **API** view of each [module page](../../03-modules/en/README.md). A refused request returns `400` with the details of each error: see [Errors](./05-errors.md).

## The response

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "faceBlurApi",
  "outputs": [
    { "key": "out", "name": "image", "url": "https://files.pixlub.com/r/…_result.png?exp=…&sig=…", "content_type": "image/png", "bytes": 172891 },
    { "key": "data", "name": "data", "url": "https://files.pixlub.com/r/…_result.json?exp=…&sig=…", "content_type": "application/json", "bytes": 82 }
  ],
  "expires_at": "2026-10-17T13:00:00Z",
  "credits": { "cost": 10, "balance": 190 }
}
```

| Field | Content |
| --- | --- |
| `id` | Result identifier (that of the first file). |
| `module` | The module that ran. |
| `outputs` | Produced files: `key`, `name`, `url`, `content_type`, `bytes`. |
| `expires_at` | When the links expire. |
| `credits` | Cost of the call and remaining balance. |
| `message` | Optional: a note from the module. |

### Finding a file by its key

A module can return several files: `splitRgb` returns its three channels. Each item of `outputs` carries the **key** of the output that produced it (`key`): `r`, `g`, `b` for `splitRgb`, `out` for most modules, `data` for the data of an AI module. A list output, or a call that sends several images, returns one file per image, under `out#0`, `out#1`… The keys of each module are listed in the **Outputs** section of its page.

```js
const result = await res.json()
const red = result.outputs.find((o) => o.key === 'r')
```

An output's `name` says what it holds:

| `name` | Content |
| --- | --- |
| `image` | The produced image. |
| `data` | A JSON file: detected faces, a rebuilt relief… |
| `file` | Another format, such as a PDF. |

## Result links

- A link is **signed** and valid for **one hour**: it downloads without an API key, as many times as needed, with no new charge.
- Files produced by our servers download from `https://files.pixlub.com`, which resumes a cut download (`Range`): follow the `url` as is, whatever its domain.
- Files are **deleted after 24 hours**.
- Treat a link as a secret until it expires: anyone holding it can download the file.
