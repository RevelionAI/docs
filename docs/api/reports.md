# Reports

## Download PDF Report

`GET /v1/scans/{scan_id}/report/pdf`

Requires `read` scope. Returns a signed download URL (valid for 1 hour).

```json
{
  "url": "https://storage.supabase.co/scan-reports/...",
  "filename": "revelion-report-2026-03-29.pdf",
  "size_bytes": 245760
}
```

## Download JSON Report

`GET /v1/scans/{scan_id}/report/json`

Requires `read` scope. Returns a signed download URL for the structured JSON report.

!!! note
    Reports are generated automatically when a scan completes. If a scan is still running, these endpoints return `404`.
