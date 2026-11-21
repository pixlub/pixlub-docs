# Authentication

Create, use, protect and revoke an API key.

Every module call authenticates with an **API key**, sent in the `X-API-Key` header. Read endpoints (`GET /v1/modules`, a module's schema) and signed result links do not need one.

```http
POST /v1/modules/blur HTTP/1.1
Host: api.pixlub.com
X-API-Key: pix.AbCdEf12.xxxxxxxxxxxxxxxxxxxxxxxx
Content-Type: multipart/form-data; boundary=…
```

## Creating a key

1. **Open the Developer section**

   [Settings → Workspace → Developer](https://pixlub.com/en/settings/workspace#developer). The section is reserved for **Basic** and **Pro** plans.

2. **Create the key**

   **Create a key**, then give it a name that says where it is used ("production server", "nightly script").

3. **Copy it right away**

   The full key is only shown once. Pixlub only keeps a fingerprint: it cannot be read again.

A key looks like `pix.<prefix>.<secret>`. The prefix, visible in the key list, identifies it; only the secret must stay hidden. The list also shows each key's creation date and last use. An account can have up to 20 active keys.

## Revoking a key

**Revoke** cuts the key off immediately: following calls receive `401`. Revoke a leaked key right away, then create a new one.

## Good practices

- **One key per use** (a server, a script, an environment): you can revoke one without cutting the others.
- **Never in source code** or a repository: use an environment variable or a secrets manager.
- **Never in a browser or a mobile app**: anyone could read it there. Call the API from your server.
- **HTTPS only**, and never in the URL: the key travels in the `X-API-Key` header.

> [!WARNING]
> **Plan and keys**
>
> If your account goes back to the free plan, your keys stay saved but calls are refused with `403` and the `plan_required` code.
