# Errors

API HTTP statuses, the error format, and what to do about each one.

An error answers with an HTTP status and a JSON body. `error` describes the problem in plain words; `code`, when present, is stable and meant for your program.

```json
{
  "error": "not enough credits for this module",
  "code": "insufficient_credits"
}
```

## Statuses

| Status | Cause | What to do |
| --- | --- | --- |
| `400` | Invalid settings, required file missing (`missing_file`) or over 25 MB, format refused by the input (`unsupported_format`), too many files (`too_many_files`), unreadable multipart request. | Fix the request. `details` lists each refused setting. |
| `401` | Missing, unknown or revoked key. | Check the `X-API-Key` header. |
| `402` | Not enough credits (`insufficient_credits`); `required` gives the cost of the call, all images included. | Top up, then run again. |
| `403` | Plan without API access (`plan_required`), more images than the plan processes per call (`batch_limit`, cap in `limit`), or an expired result link. | Move to a paid plan; spread the images over several calls; run the call again for a new link. |
| `404` | Unknown module or result; deposit unknown, already used or expired (`upload_not_found`); unknown job (`job_not_found`). | Check the identifier; open a new deposit. |
| `409` | File not sent to `upload_url` yet (`upload_incomplete`). | Finish the `PUT`, then run the call again. |
| `413` | File larger than your plan (`file_too_large`, ceiling in `max_bytes`), or too large for the request (`use_uploads`). | Shrink the file, or deposit it with [`POST /v1/uploads`](./035-large-files.md). |
| `422` | Unreadable source URL: `source_status`, `source_too_large`, `source_timeout`, `source_unreachable`. | Check the address and the file size. |
| `429` | Too many requests. | Wait a few seconds, then run again. |
| `500` | Error on our side. The charge is refunded. | Try again later. |
| `501` | Module the API cannot run (video, 3D…). | Use it on the site. |
| `503` | Service temporarily unavailable. | Try again later. |

## Refused settings

A `400` on settings details each error, in JSON Schema format:

```json
{
  "error": "Paramètres invalides",
  "details": [
    {
      "instancePath": "/radius",
      "keyword": "maximum",
      "params": { "comparison": "<=", "limit": 40 },
      "message": "must be <= 40"
    }
  ]
}
```

`instancePath` points at the faulty setting. Each setting's limits are in the **API** view of the [module page](../../03-modules/en/README.md).

## Retrying safely

- `400`, `401`, `402`, `403`, `404`: the request was neither run nor charged. Sending it again unchanged will fail again.
- `429`: nothing was computed or charged; run again after a short pause, spacing out attempts.
- `500`, `503`, timeout: the call may have been charged then refunded. Check your balance before running an expensive module again.
