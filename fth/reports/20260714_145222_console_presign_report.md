# Console Presigned-URL Test

| Field | Value |
|---|---|
| Script | `console_presign` |
| Run | `20260714_145222` |

## Summary

| Total | OK | Failed | Status |
|---:|---:|---:|:---|
| 23 | 20 | 3 | **FAIL** |

## BY OPERATION

| Operation | OK | Failed | Total | Avg | Stddev | Min | Max |
|---|---:|---:|---:|---:|---:|---:|---:|
| `execute_deleteObject` | 1 | 0 | 1 | 0.145s | 0.000s | 0.145s | 0.145s |
| `execute_getObject` | 1 | 0 | 1 | 0.089s | 0.000s | 0.089s | 0.089s |
| `execute_getObjectRetention` | 1 | 0 | 1 | 0.075s | 0.000s | 0.075s | 0.075s |
| `execute_headObject` | 1 | 0 | 1 | 0.084s | 0.000s | 0.084s | 0.084s |
| `execute_headObjectFilMeta` | 1 | 0 | 1 | 0.083s | 0.000s | 0.083s | 0.083s |
| `execute_listObjects` | 1 | 0 | 1 | 0.085s | 0.000s | 0.085s | 0.085s |
| `execute_putObject` | 1 | 0 | 1 | 0.159s | 0.000s | 0.159s | 0.159s |
| `preflight_deleteObject` | 1 | 0 | 1 | 0.067s | 0.000s | 0.067s | 0.067s |
| `preflight_putObject` | 1 | 0 | 1 | 0.064s | 0.000s | 0.064s | 0.064s |
| `presign_deleteObject` | 1 | 0 | 1 | 0.001s | 0.000s | 0.001s | 0.001s |
| `presign_getObject` | 1 | 0 | 1 | 0.001s | 0.000s | 0.001s | 0.001s |
| `presign_getObjectRetention` | 1 | 0 | 1 | 0.001s | 0.000s | 0.001s | 0.001s |
| `presign_headObject` | 1 | 0 | 1 | 0.001s | 0.000s | 0.001s | 0.001s |
| `presign_headObjectFilMeta` | 1 | 0 | 1 | 0.001s | 0.000s | 0.001s | 0.001s |
| `presign_listObjects` | 1 | 0 | 1 | 0.002s | 0.000s | 0.002s | 0.002s |
| `presign_putObject` | 1 | 0 | 1 | 0.002s | 0.000s | 0.002s | 0.002s |
| `response_cors_deleteObject` | 1 | 0 | 1 | — | — | — | — |
| `response_cors_getObject` | 0 | 1 | 1 | — | — | — | — |
| `response_cors_getObjectRetention` | 1 | 0 | 1 | — | — | — | — |
| `response_cors_headObject` | 0 | 1 | 1 | — | — | — | — |
| `response_cors_headObjectFilMeta` | 0 | 1 | 1 | — | — | — | — |
| `response_cors_listObjects` | 1 | 0 | 1 | — | — | — | — |
| `response_cors_putObject` | 1 | 0 | 1 | — | — | — | — |

## Run details

```
TEST RUN
  Provider         : fth
  Endpoint         : https://us-east-1.s3.fil.one
  Bucket           : stray-cat-bucket
  Test key         : console-presign-test/f056bbda-9799-47be-b9e6-e0fa5182be07/probe.txt
  Browser origin   : https://app.fil.one
  Presign expiry   : 300s
  CORS applied     : no (provider manages CORS out-of-band)

BUCKET CORS CONFIGURATION (before test)
  (provider returned NoSuchCORSConfiguration)
```

## Successes

```json
{"ts": "2026-07-14T14:52:22.444964+00:00", "op": "presign_putObject", "status": "ok", "elapsed_s": 0.002, "s3_op": "put_object", "http_method": "PUT", "url_host": "us-east-1.s3.fil.one", "signed_query_contains_fil_meta": false}
{"ts": "2026-07-14T14:52:22.508754+00:00", "op": "preflight_putObject", "status": "ok", "elapsed_s": 0.064, "request_method": "PUT", "request_headers": ["Content-Type", "x-amz-meta-filename"], "status_code": 204, "response_headers_lower": {"access-control-allow-headers": "Content-Type, x-amz-meta-filename", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-max-age": "3600", "vary": "Origin, Access-Control-Request-Method, Access-Control-Request-Headers", "date": "Tue, 14 Jul 2026 14:52:21 GMT"}, "allow_origin": "https://app.fil.one", "allow_methods": ["DELETE", "GET", "HEAD", "OPTIONS", "POST", "PUT"], "allow_headers": ["content-type", "x-amz-meta-filename"], "missing_request_headers": [], "status_ok": true, "origin_ok": true, "method_ok": true, "headers_ok": true}
{"ts": "2026-07-14T14:52:22.667566+00:00", "op": "execute_putObject", "status": "ok", "elapsed_s": 0.159, "status_code": 200, "response_headers_lower": {"access-control-allow-headers": "*", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-expose-headers": "ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker", "content-length": "0", "date": "Tue, 14 Jul 2026 14:52:21 GMT", "etag": "\"3fa6f61e4062b664e24811f5d6045e9b\"", "vary": "Origin"}}
{"ts": "2026-07-14T14:52:22.667800+00:00", "op": "response_cors_putObject", "status": "ok", "status_code": 200, "allow_origin": "https://app.fil.one", "expose_headers": ["content-length", "etag", "x-amz-delete-marker", "x-amz-id-2", "x-amz-request-id", "x-amz-version-id"], "missing_expose_headers": [], "missing_response_meta_headers": [], "origin_ok": true, "expose_ok": true, "meta_ok": true}
{"ts": "2026-07-14T14:52:22.670867+00:00", "op": "presign_listObjects", "status": "ok", "elapsed_s": 0.002, "s3_op": "list_objects_v2", "http_method": "GET", "url_host": "us-east-1.s3.fil.one", "signed_query_contains_fil_meta": false}
{"ts": "2026-07-14T14:52:22.755618+00:00", "op": "execute_listObjects", "status": "ok", "elapsed_s": 0.085, "status_code": 200, "response_headers_lower": {"access-control-allow-headers": "*", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-expose-headers": "ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker", "content-length": "635", "content-type": "application/xml", "date": "Tue, 14 Jul 2026 14:52:21 GMT", "vary": "Origin"}}
{"ts": "2026-07-14T14:52:22.755849+00:00", "op": "response_cors_listObjects", "status": "ok", "status_code": 200, "allow_origin": "https://app.fil.one", "expose_headers": ["content-length", "etag", "x-amz-delete-marker", "x-amz-id-2", "x-amz-request-id", "x-amz-version-id"], "missing_expose_headers": [], "missing_response_meta_headers": [], "origin_ok": true, "expose_ok": true, "meta_ok": true}
{"ts": "2026-07-14T14:52:22.758572+00:00", "op": "presign_headObject", "status": "ok", "elapsed_s": 0.001, "s3_op": "head_object", "http_method": "HEAD", "url_host": "us-east-1.s3.fil.one", "signed_query_contains_fil_meta": false}
{"ts": "2026-07-14T14:52:22.843240+00:00", "op": "execute_headObject", "status": "ok", "elapsed_s": 0.084, "status_code": 200, "response_headers_lower": {"access-control-allow-headers": "*", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-expose-headers": "ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker", "content-length": "41", "content-type": "text/plain", "date": "Tue, 14 Jul 2026 14:52:21 GMT", "etag": "\"3fa6f61e4062b664e24811f5d6045e9b\"", "last-modified": "Tue, 14 Jul 2026 14:52:22 GMT", "vary": "Origin", "x-amz-meta-filename": "probe.txt"}}
{"ts": "2026-07-14T14:52:22.845981+00:00", "op": "presign_headObjectFilMeta", "status": "ok", "elapsed_s": 0.001, "s3_op": "head_object", "http_method": "HEAD", "url_host": "us-east-1.s3.fil.one", "signed_query_contains_fil_meta": true}
{"ts": "2026-07-14T14:52:22.929585+00:00", "op": "execute_headObjectFilMeta", "status": "ok", "elapsed_s": 0.083, "status_code": 200, "response_headers_lower": {"access-control-allow-headers": "*", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-expose-headers": "ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker", "content-length": "41", "content-type": "text/plain", "date": "Tue, 14 Jul 2026 14:52:21 GMT", "etag": "\"3fa6f61e4062b664e24811f5d6045e9b\"", "last-modified": "Tue, 14 Jul 2026 14:52:22 GMT", "vary": "Origin", "x-amz-meta-filename": "probe.txt"}}
{"ts": "2026-07-14T14:52:22.932328+00:00", "op": "presign_getObject", "status": "ok", "elapsed_s": 0.001, "s3_op": "get_object", "http_method": "GET", "url_host": "us-east-1.s3.fil.one", "signed_query_contains_fil_meta": false}
{"ts": "2026-07-14T14:52:23.021904+00:00", "op": "execute_getObject", "status": "ok", "elapsed_s": 0.089, "status_code": 200, "response_headers_lower": {"access-control-allow-headers": "*", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-expose-headers": "ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker", "content-length": "41", "content-type": "text/plain", "date": "Tue, 14 Jul 2026 14:52:21 GMT", "etag": "\"3fa6f61e4062b664e24811f5d6045e9b\"", "last-modified": "Tue, 14 Jul 2026 14:52:22 GMT", "vary": "Origin", "x-amz-meta-filename": "probe.txt"}}
{"ts": "2026-07-14T14:52:23.025152+00:00", "op": "presign_getObjectRetention", "status": "ok", "elapsed_s": 0.001, "s3_op": "get_object_retention", "http_method": "GET", "url_host": "us-east-1.s3.fil.one", "signed_query_contains_fil_meta": false}
{"ts": "2026-07-14T14:52:23.100316+00:00", "op": "execute_getObjectRetention", "status": "ok", "note": "acceptable S3 error (pipeline still validated)", "elapsed_s": 0.075, "status_code": 400, "response_headers_lower": {"access-control-allow-headers": "*", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-expose-headers": "ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker", "content-length": "226", "content-type": "application/xml", "date": "Tue, 14 Jul 2026 14:52:21 GMT", "vary": "Origin"}}
{"ts": "2026-07-14T14:52:23.100528+00:00", "op": "response_cors_getObjectRetention", "status": "ok", "status_code": 400, "allow_origin": "https://app.fil.one", "expose_headers": ["content-length", "etag", "x-amz-delete-marker", "x-amz-id-2", "x-amz-request-id", "x-amz-version-id"], "missing_expose_headers": [], "missing_response_meta_headers": [], "origin_ok": true, "expose_ok": true, "meta_ok": true}
{"ts": "2026-07-14T14:52:23.103276+00:00", "op": "presign_deleteObject", "status": "ok", "elapsed_s": 0.001, "s3_op": "delete_object", "http_method": "DELETE", "url_host": "us-east-1.s3.fil.one", "signed_query_contains_fil_meta": false}
{"ts": "2026-07-14T14:52:23.170163+00:00", "op": "preflight_deleteObject", "status": "ok", "elapsed_s": 0.067, "request_method": "DELETE", "request_headers": [], "status_code": 204, "response_headers_lower": {"access-control-allow-headers": "", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-max-age": "3600", "vary": "Origin, Access-Control-Request-Method, Access-Control-Request-Headers", "date": "Tue, 14 Jul 2026 14:52:22 GMT"}, "allow_origin": "https://app.fil.one", "allow_methods": ["DELETE", "GET", "HEAD", "OPTIONS", "POST", "PUT"], "allow_headers": [], "missing_request_headers": [], "status_ok": true, "origin_ok": true, "method_ok": true, "headers_ok": true}
{"ts": "2026-07-14T14:52:23.315149+00:00", "op": "execute_deleteObject", "status": "ok", "elapsed_s": 0.145, "status_code": 204, "response_headers_lower": {"access-control-allow-headers": "*", "access-control-allow-methods": "GET, HEAD, PUT, POST, DELETE, OPTIONS", "access-control-allow-origin": "https://app.fil.one", "access-control-expose-headers": "ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker", "date": "Tue, 14 Jul 2026 14:52:21 GMT", "vary": "Origin"}}
{"ts": "2026-07-14T14:52:23.315411+00:00", "op": "response_cors_deleteObject", "status": "ok", "status_code": 204, "allow_origin": "https://app.fil.one", "expose_headers": ["content-length", "etag", "x-amz-delete-marker", "x-amz-id-2", "x-amz-request-id", "x-amz-version-id"], "missing_expose_headers": [], "missing_response_meta_headers": [], "origin_ok": true, "expose_ok": true, "meta_ok": true}
```

## Errors

<details markdown="1">
<summary>response_cors_headObject — ResponseCorsMissing: Response lacks CORS headers the browser needs</summary>

**Error details**

```json
{
  "ts": "2026-07-14T14:52:22.843478+00:00",
  "op": "response_cors_headObject",
  "status": "err",
  "error_code": "ResponseCorsMissing",
  "error_message": "Response lacks CORS headers the browser needs",
  "status_code": 200,
  "allow_origin": "https://app.fil.one",
  "expose_headers": [
    "content-length",
    "etag",
    "x-amz-delete-marker",
    "x-amz-id-2",
    "x-amz-request-id",
    "x-amz-version-id"
  ],
  "missing_expose_headers": [
    "content-type",
    "last-modified"
  ],
  "missing_response_meta_headers": [],
  "origin_ok": true,
  "expose_ok": false,
  "meta_ok": true
}
```

</details>

<details markdown="1">
<summary>response_cors_headObjectFilMeta — ResponseCorsMissing: Response lacks CORS headers the browser needs</summary>

**Error details**

```json
{
  "ts": "2026-07-14T14:52:22.929807+00:00",
  "op": "response_cors_headObjectFilMeta",
  "status": "err",
  "error_code": "ResponseCorsMissing",
  "error_message": "Response lacks CORS headers the browser needs",
  "status_code": 200,
  "allow_origin": "https://app.fil.one",
  "expose_headers": [
    "content-length",
    "etag",
    "x-amz-delete-marker",
    "x-amz-id-2",
    "x-amz-request-id",
    "x-amz-version-id"
  ],
  "missing_expose_headers": [
    "content-type",
    "last-modified",
    "x-fil-cid"
  ],
  "missing_response_meta_headers": [],
  "origin_ok": true,
  "expose_ok": false,
  "meta_ok": true
}
```

</details>

<details markdown="1">
<summary>response_cors_getObject — ResponseCorsMissing: Response lacks CORS headers the browser needs</summary>

**Error details**

```json
{
  "ts": "2026-07-14T14:52:23.022135+00:00",
  "op": "response_cors_getObject",
  "status": "err",
  "error_code": "ResponseCorsMissing",
  "error_message": "Response lacks CORS headers the browser needs",
  "status_code": 200,
  "allow_origin": "https://app.fil.one",
  "expose_headers": [
    "content-length",
    "etag",
    "x-amz-delete-marker",
    "x-amz-id-2",
    "x-amz-request-id",
    "x-amz-version-id"
  ],
  "missing_expose_headers": [
    "content-type",
    "last-modified"
  ],
  "missing_response_meta_headers": [],
  "origin_ok": true,
  "expose_ok": false,
  "meta_ok": true
}
```

</details>


## Log files

- Success: `../logs/20260714_145222_console_presign_success.jsonl`
- Errors: `../logs/20260714_145222_console_presign_errors.jsonl`
