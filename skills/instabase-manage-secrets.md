---
name: Manage AI Hub secrets
description: Store, list, update, and delete secrets used by AI Hub apps and integrations.
api: openapi/instabase-aihub-openapi.yaml
operations: [listSecrets, createSecret, updateSecret, deleteSecret]
---

# Manage AI Hub secrets

Securely store credentials that automation apps and integrations reference.

## Auth
- `Authorization: Bearer ${API_TOKEN}` + `IB-Context` (organization ID) on every request.
- Base URL: `https://aihub.instabase.com/api`.

## Steps
1. **List** — `listSecrets` (`GET /v2/aihub/secrets`).
2. **Create** — `createSecret` (`POST /v2/aihub/secrets`) with a name and value. Secret key names may contain hyphens (release 26.24).
3. **Update** — `updateSecret` (`PATCH /v2/aihub/secrets`) to rotate a value.
4. **Delete** — `deleteSecret` (`DELETE /v2/aihub/secrets`).

## Notes
- Never log secret values. Errors return the `error` JSON schema (`errors/instabase-problem-types.yml`).
