---
name: Process documents with an AI Hub app
description: Upload files to a batch and run an automation app to extract structured data, then fetch the results.
api: openapi/instabase-aihub-openapi.yaml
operations: [createBatch, addFileToBatch, runApp, getRunStatus, getRunResults]
---

# Process documents with an AI Hub app

Use the Instabase AI Hub API to turn documents into structured data.

## Auth
- Send `Authorization: Bearer ${API_TOKEN}` on every request (create a token under Settings > APIs).
- Always send the `IB-Context` header (your organization ID). See `authentication/instabase-authentication.yml`.
- Base URL: `https://aihub.instabase.com/api` (or `https://{org}.instabase.com/api`). HTTPS only.

## Steps
1. **Create a batch** — `createBatch` (`POST /v2/batches`) to get a `batch_id`.
2. **Add files** — `addFileToBatch` (`PUT /v2/batches/{batch_id}/files/{filename}`) for each document (pdf, image, docx, xlsx, etc.).
3. **Run an app** — `runApp` (`POST /v2/apps/runs`) referencing the app and the `batch_id`. This returns a `run_id`.
4. **Poll status** — `getRunStatus` (`GET /v2/apps/runs/{run_id}`) until the run completes (async job pattern, see `conventions/instabase-conventions.yml`).
5. **Fetch results** — `getRunResults` (`GET /v2/apps/runs/{run_id}/results`) to read extracted fields. Optional query flags: `include_confidence_scores`, `include_validation_results`, `include_source_info`.

## Notes
- No idempotency-key contract; do not blindly retry non-idempotent POSTs. Retry behavior is tuned via the `IB-Retry-Config` header.
- Errors return the `error` JSON schema; see `errors/instabase-problem-types.yml`.
