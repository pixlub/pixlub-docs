# Large files and long jobs

Send a file over 25 MB, have a URL downloaded, and follow a job that takes several minutes.

A regular call sends the file in the request and waits for the result. Two cases fall outside that frame:

- a **large file** (over **25 MB**) does not fit in the request: deposit it first, or give its address;
- a **long job** answers `202` right away with an identifier, to follow until the result.

Modules run by our servers (`handler` = `remote` in `GET /v1/modules`) accept both. Modules computed by the API stay limited to 25 MB per file, in the request.

## Depositing a large file

**1. Open a deposit.** Name the module, the file name and its exact size:

```bash
curl -X POST https://api.pixlub.com/v1/uploads \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"module":"removeBgApi","filename":"photo.png","bytes":48213977}'
```

```json
{
  "upload_id": "8a6f1f3e-6a1c-4c55-9a43-2f0e5b8f0c11",
  "upload_url": "https://files.pixlub.com/u/8a6f1f3e-…?exp=…&max=48213977&sig=…",
  "method": "PUT",
  "expires_at": "2026-10-26T14:15:00Z"
}
```

A size beyond your plan is refused right away (`413`, `file_too_large`, ceiling in `max_bytes`), before any upload.

**2. Send the file** to `upload_url`, as one `PUT` whose body is the raw file. No API key needed: the signed URL is enough. It is valid for **15 minutes** to start the upload, and accepts no more bytes than the announced size.

```bash
curl -T photo.png "https://files.pixlub.com/u/8a6f1f3e-…?exp=…&max=48213977&sig=…"
```

Quote the URL and use it as is, without re-encoding it: the signature covers every character.

**3. Run the module** with the `upload_id` field instead of the file:

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F upload_id=8a6f1f3e-6a1c-4c55-9a43-2f0e5b8f0c11 \
  -F 'params={}'
```

The response is the same as a direct call. A deposit serves **only once**; uploaded but never used, it is deleted after 24 hours.

## Having a URL downloaded

If the file is already online (your own storage, a CDN), give its address in `source_url`: our servers download it themselves, with no upload on your side.

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F source_url=https://cdn.example.com/photos/photo.png \
  -F 'params={}'
```

- The address uses **`https`**, on port 443, with no credentials in the URL. A signed URL from your storage (S3, R2…) works.
- **Non-public** addresses (private network, loopback…) are refused, even behind a name or a redirect (`400`, `forbidden_address`).
- The allowed size is your plan's; the download lasts **15 minutes** at most.
- A failed download answers `422` with its code: `source_status` (a response other than `200`), `source_too_large`, `source_timeout`, `source_unreachable`.

## Following a long job

A call waits for the job to finish for **a little under a minute**. Beyond that, it answers `202`:

```json
{
  "job_id": "3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7",
  "module": "removeBgApi",
  "status": "running",
  "poll": "https://api.pixlub.com/v1/jobs/3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7"
}
```

The job goes on on our side, and its credits are already charged. Follow it with `GET /v1/jobs/:id`; the `Prefer: wait=25` header waits for its end up to 25 seconds, which saves calls:

```bash
curl https://api.pixlub.com/v1/jobs/3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7 \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -H "Prefer: wait=25"
```

| `status` | Response content |
| --- | --- |
| `queued`, `running` | Nothing else: follow again. |
| `succeeded` | The module's response (`outputs`, `expires_at`, `credits`…), as for a direct call. |
| `failed` | `error`, `code` and `http_status`: the error the direct call would have returned. A failure on our side is refunded. |

```js
let job = await (await fetch(poll, { headers: { 'X-API-Key': key, Prefer: 'wait=25' } })).json()
while (job.status === 'queued' || job.status === 'running') {
  job = await (await fetch(poll, { headers: { 'X-API-Key': key, Prefer: 'wait=25' } })).json()
}
if (job.status === 'failed') throw new Error(`${job.http_status} ${job.code}`)
const url = job.outputs[0].url
```

A job can be read for **24 hours**; its result links stay valid for one hour, like those of a direct call. Batch calls (several images in one request) always wait for their result.

## Downloading results

Files produced by our servers download from `https://files.pixlub.com`, without an API key, through their signed link. A cut download resumes where it stopped:

```bash
curl -C - -o output.png "https://files.pixlub.com/r/…_result.png?exp=…&sig=…"
```
