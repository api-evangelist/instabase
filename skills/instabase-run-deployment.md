---
name: Run a production app deployment
description: Trigger a deployed AI Hub app against input files and collect the run results.
api: openapi/instabase-aihub-openapi.yaml
operations: [runDeployment, getRunStatus, getRunResults]
---

# Run a production app deployment

Deployments are production-scale, automated versions of AI Hub automation apps.

## Auth
- `Authorization: Bearer ${API_TOKEN}` + `IB-Context` header on every request.
- Base URL: `https://aihub.instabase.com/api`.

## Steps
1. **Run the deployment** — `runDeployment` (`POST /v2/apps/deployments/{deployment-id}/runs`) with the input files/batch. Returns a `run_id`.
2. **Poll status** — `getRunStatus` (`GET /v2/apps/runs/{run_id}`) until complete.
3. **Get results** — `getRunResults` (`GET /v2/apps/runs/{run_id}/results`).

## Notes
- Deployments can also emit **webhook notifications** on completion / review-required (see `asyncapi/instabase-webhooks.yml`) — prefer webhooks over tight polling for production.
- Legacy run/job endpoints exist but are deprecated; use the `/v2/apps/...` operations (see `lifecycle/instabase-lifecycle.yml`).
