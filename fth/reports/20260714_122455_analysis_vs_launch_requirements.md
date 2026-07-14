# FTH S3 Compatibility — Run `20260714_122455` Evaluation vs Launch Requirements

**Date:** 2026-07-14 (re-run, 12:24)
**Analyzed reports:** [`20260714_122455_compatibility_report.md`](20260714_122455_compatibility_report.md) (ceph/s3-tests) + [`20260714_145222_console_presign_report.md`](20260714_145222_console_presign_report.md) (presign/CORS) + [`20260714_145738_fetch_report.md`](20260714_145738_fetch_report.md) (fetch) + [`20260714_145750_delete_report.md`](20260714_145750_delete_report.md) (delete)
**Compared against:** [`FTH_launch_requirements_20260708.md`](FTH_launch_requirements_20260708.md), baseline [`20260708_122448`](20260708_122448_compatibility_report.md) (378 pass)
**Suites:** ceph/s3-tests (boto3/botocore, SigV4, marker `not fails_on_aws`) + console presigned-URL/CORS + fetch + delete

---

## TL;DR

- **ceph/s3-tests: valid run — 524 pass / 74 fail, `Error: 0`.** Up from the 378-pass launch baseline ([`20260708_122448`](20260708_122448_compatibility_report.md)).
- **The test key is scoped correctly** — only **4 `AccessDenied`** failures remain, so the run is almost entirely genuine FTH behavior rather than test-config noise.
- **6 of 8 s3-tests launch items are now MET** (P0-1, P1-2, P1-3, **P2-5 newly confirmed**, P2-8), and **P2-7 is substantially resolved** (the action-set gap that drove the noise is closed).
- **✅ Verified non-blocking — presign/CORS expose-headers** ([`20260714_145222`](20260714_145222_console_presign_report.md), 20/23): the compat test fails because presigned **GET/HEAD responses omit `Content-Type`/`Last-Modified` from `Access-Control-Expose-Headers`** — but a **real-browser check (2026-07-14) confirmed the console reads both from JS anyway**, because they're CORS-safelisted. This is an **ADR-compliance / correctness** item, **not** a functional launch blocker. See the presign section.
- **s3-tests residual blockers, both P2:** **P2-4 SSE-KMS** (still rejected) and **P2-6 SigV2** (still rejected).
- **The 74 s3-tests failures are dominated by two clusters:** ~39 SSE-KMS `InvalidRequest` (P2-4) and ~19 ACL owner-`DisplayName` mismatches (a config/behavior quirk, **not** on the launch list). SigV2 accounts for 4; the rest (~11) are minor ACL-enforcement and error-code-semantics cases, none launch-blocking.
- **Fetch (15/15) and delete (5/5) suites are fully green** — including head/preview/list-versions and delete on the three ~21 MB multipart objects, corroborating that the old multipart `BadDigest` upload regression is resolved.

---

## Run health

```
Collected : 838   Passed : 524   Failed : 74   Error : 0   Skipped : 5   Duration : 3838s
```

| Metric | [`20260714_122455`](20260714_122455_compatibility_report.md) | Baseline [`20260708_122448`](20260708_122448_compatibility_report.md) |
|---|---:|---:|
| Passed | **524** | 378 |
| Failed | 74 | 181 |
| Error (setup) | 0 | — |
| `AccessDenied` failures | **4** | — |
| Validity | ✅ | ✅ |

`Error: 0` and only 4 `AccessDenied` failures confirm the test key is scoped correctly — the remaining failures reflect actual FTH behavior, not fixture/config noise.

## What the 74 failures actually are

| Cluster | Count | Whose problem | Launch item |
|---|---:|---|---|
| SSE-KMS `InvalidRequest` (PutObject, CopyObject, CreateMultipartUpload; all `copy_enc`/`copy_part_enc` sse-kms variants, transfers, uploads, multipart) | **~39** | **FTH** | **P2-4** |
| ACL owner `DisplayName` mismatch — server returns numeric account id (`219`/`220`) vs configured `FilOne Compat main/alt User` | **~19** | FTH behavior / test-conf expectation | none |
| SigV2 `SignatureDoesNotMatch` (`test_cors_presigned_*_v2`, incl. tenant variants) | **4** | **FTH** | **P2-6** |
| Bucket/object ACL access-enforcement (`test_access_bucket_*`: `ClientError not raised` / `AccessDenied`) | ~5 | FTH ACL semantics | none |
| Misc: `test_100_continue` (`'100'=='403'`), `test_get_bucket_encryption_{s3,kms}` (empty vs `…NotFoundError`), `test_put_bucket_logging_errors` (negative test), 1 residual policy/tag `AccessDenied` | ~7 | mixed | none |

The **entire** `InvalidRequest` set is SSE-KMS — that single feature is what holds `encryption` at 61% (66/108) and is the only substantive FTH blocker of any size left in the run.

---

## Launch-requirements status

Legend: ✅ met · 🔴 not met · 🟡 largely resolved

| # | Requirement | Verdict | Evidence |
|---|---|:--:|---|
| **P0-1** | Zero-byte PutObject 500 + phantom | ✅ **MET** | All four tests pass; `conditional_write` 100% (7/7). |
| **P1-2** | `SignatureDoesNotMatch` on `+`/space/`%` keys | ✅ **MET** | All three cited tests pass, including `test_bucket_create_special_key_names`. The signing/canonicalization symptom is gone. |
| **P1-3** | `BadDigest` on 16 MB copy | ✅ **MET** | `test_object_copy_16m` passes; `copy` 100% (31/31), `checksum` 100% (11/11). |
| **P2-4** | SSE-KMS operations rejected | 🔴 **NOT met** | `InvalidRequest` across every SSE-KMS path (~39 failures): `test_sse_kms_present`, `_method_head`, `_multipart_upload`, all `_transfer_*`/`_default_upload_*`, and all `copy_enc[*sse-kms*]`. |
| **P2-5** | PutBucketLogging rejects all destinations | ✅ **MET** | `test_put_bucket_logging` and `test_bucket_logging_owner` **now pass** (`bucket_logging` 83%, 5/6). With the key permission granted, logging round-trips — the original `InvalidArgument: Invalid bucket logging destination` symptom is gone. (Remaining 1 failure is `test_put_bucket_logging_errors`, a negative/`expected failure` case.) |
| **P2-6** | SigV2 signatures rejected | 🔴 **NOT met** | `test_cors_presigned_{get,put}_object_v2` (and tenant variants) still fail `SignatureDoesNotMatch`. Fix, or confirm SigV4-only in writing. |
| **P2-7** | Document permission action model | 🟡 **largely resolved** | Only 4 `AccessDenied` failures remain; the key is now scoped correctly. Residual: a couple of ACL/policy edge cases. Still worth publishing the action list, but it's no longer blocking the suite. |
| **P2-8** | DeleteBucket on retention-locked objects | ✅ **MET** | Both object-lock mode-change tests pass. |

### Movement since the 2026-07-08 launch baseline

- **Newly MET:** **P0-1** (zero-byte), **P1-2** (special-char keys), **P1-3** (16 MB copy), **P2-5** (logging round-trips), **P2-8** (retention-locked delete) — all were failing at baseline.
- **P2-7 largely closed:** the key is now scoped correctly (4 residual `AccessDenied`).
- **Still open:** **P2-4 (SSE-KMS)** and **P2-6 (SigV2)** — the two genuine FTH blockers, both P2.

---

## Presign / console CORS suite — ✅ verified non-blocking ([`20260714_145222`](20260714_145222_console_presign_report.md), 20/23)

The presigned-URL pipeline is healthy: every `presign_*`, `preflight_*`, and `execute_*` step passes for put/get/head/list/delete/retention — signing, preflight (204 with correct `Allow-Origin`/`Allow-Methods`/`Allow-Headers`), and the S3 operations themselves all work. All 3 failures share one root cause.

**Finding — `Access-Control-Expose-Headers` incomplete on object GET/HEAD.** The gateway exposes `ETag, Content-Length, x-amz-request-id, x-amz-id-2, x-amz-version-id, x-amz-delete-marker` but **not `Content-Type` or `Last-Modified`**. The compat test requires them explicitly (per the *PR #198 ADR*) and so flags these three checks:

| Failing check | Test-required (missing) | Genuinely hidden from JS |
|---|---|---|
| `response_cors_getObject` | `content-type`, `last-modified` | — |
| `response_cors_headObject` | `content-type`, `last-modified` | — |
| `response_cors_headObjectFilMeta` | `content-type`, `last-modified` | `x-fil-cid` |

**Why this is *not* a functional blocker.** `Content-Type` and `Last-Modified` are on the **CORS-safelisted response-header** list (`Cache-Control, Content-Language, Content-Length, Content-Type, Expires, Last-Modified, Pragma`), which browsers expose to JS **regardless** of `Access-Control-Expose-Headers`.

**Verified in-browser (2026-07-14).** A real browser `fetch(..., {method:'HEAD'})` on `https://app.fil.one` against a presigned object HEAD (`bernie-review.jpeg`, the `response_cors_headObject` case) returned this JS-readable set from `r.headers`:

```
content-length, content-type, etag, last-modified, x-amz-id-2, x-amz-request-id
```

- `content-type`, `last-modified`, `content-length` → readable via the **CORS safelist** (not in the server's expose list, exposed anyway).
- `etag`, `x-amz-id-2`, `x-amz-request-id` → readable because the server **explicitly** exposes them.
- `via`, `date`, `vary` → **absent** (correctly hidden — not safelisted, not exposed), which confirms the browser *is* enforcing CORS filtering. So the readability of `content-type`/`last-modified` is genuine safelist behavior, not a wildcard/no-filter artifact.

The console therefore reads everything it needs off presigned GET/HEAD today. `x-fil-cid` is the only header that stays hidden (not safelisted, not exposed, not emitted on this path) — already agreed **non-blocking**.

**Status: closed as non-blocking.** The compat failure is a literal substring check of the `Access-Control-Expose-Headers` value; browser behavior is unaffected. Optional cleanup only: FTH may still add `Content-Type, Last-Modified` to the expose list for **PR #198 ADR** compliance (would take the suite to 23/23), but it changes nothing functionally.

**Ownership if fixed:** gateway CORS config, not app code (`CORS applied: no — provider manages CORS out-of-band`; bucket returns `NoSuchCORSConfiguration`). FTH adds `Content-Type, Last-Modified` to expose-headers on GET/HEAD → all three checks clear (23/23). **Not a regression** — identical to the "one narrow issue remains" in the [2026-07-08 presign comparison](20260708_141414_vs_prior_comparison.md); partially fixed since April, then plateaued.

---

## Fetch & delete suites — both fully green ✅

| Suite | Result | Coverage |
|---|---|---|
| Fetch ([`20260714_145738`](20260714_145738_fetch_report.md)) | **15/15 PASS** | `head_object`, `get_object_preview`, `list_versions` across 5 keys, all sub-400 ms |
| Delete ([`20260714_145750`](20260714_145750_delete_report.md)) | **5/5 PASS** | `delete_object` across the same 5 keys, 0.09–0.34 s |

Both suites exercised the same object set as the 2026-07-08 baseline, **including the three ~21 MB `.zip` objects** that were the subject of the earlier multipart `BadDigest` upload regression. This run shows them freshly PUT (multipart ETags, `…-2`), then **HEAD/preview/list-versions/delete cleanly** — direct corroboration (alongside s3-tests `copy` 100% and `checksum` 100%) that the large-object multipart integrity problem is resolved. `head_object` also returns correct `content_type`/`last_modified`/`etag` at the S3 layer — reinforcing that the flagged presign/CORS finding above is strictly a *header-exposure* nuance, not a missing-header problem on the wire.

---

## Assessment & actions

**Launch readiness:** all s3-tests P0/P1 items and all but two P2 items are met, and the critical-path s3 regressions are done. The two remaining **P2** s3-tests items are the only genuine blockers; the presign/CORS finding is **verified non-blocking** (real-browser check on 2026-07-14).

**FTH (blockers):**
1. **P2-4 SSE-KMS** — every `aws:kms` operation returns `InvalidRequest`. Largest s3-tests cluster (~39) and the sole reason `encryption` isn't ~100%. Either provide the per-tenant KMS key-provisioning step, or send written confirmation that SSE-KMS is unsupported for our launch docs.
2. **P2-6 SigV2** — SigV2-signed requests still rejected. Fix, or confirm SigV4-only in writing (per the launch doc, written confirmation suffices).

**Verified non-blocking (optional cleanup):**
3. **Presign expose-headers.** `Content-Type`/`Last-Modified` missing from `Access-Control-Expose-Headers` on GET/HEAD, but a real-browser check confirmed both are JS-readable via the CORS safelist. No functional impact. Optional: FTH may add `Content-Type, Last-Modified` to the expose list for **PR #198 ADR** compliance (clears the 3 test failures → 23/23).

**FTH (non-blocking follow-up):**
4. Emit + expose **`x-fil-cid`** on the Fil-meta HEAD path so the console can read the CID from JS.

**FilOne (non-blocking cleanup):**
5. The ~19 ACL `DisplayName` mismatches are FTH returning the numeric account id (`219`/`220`) as the owner `DisplayName`. Either align `s3tests.conf` `display_name` to the returned id, or ask FTH to echo the configured name. Cosmetic — but it inflates the failure count.
6. Grant the last couple of actions behind the 4 residual `AccessDenied` (object-tag policy path) to fully retire P2-7 noise.

**Bottom line:** the s3-tests run is the cleanest to date and clears the launch-critical S3 work. **The only genuine launch blockers are the two P2 s3-tests items — SSE-KMS and SigV2** — each needing either a fix or written confirmation of intended behavior. The presign/CORS expose-headers gap is **verified non-blocking** — a real-browser check confirmed the console reads `Content-Type`/`Last-Modified` via the CORS safelist; it remains only an optional ADR-compliance cleanup. Everything else is met or cosmetic.
