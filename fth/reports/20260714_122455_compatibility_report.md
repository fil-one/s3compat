# S3 Compatibility Test — fth

| Field | Value |
|---|---|
| Script | `compatibility_test` |
| Run | `20260714_122455` |

## Summary

| Total | OK | Failed | Status |
|---:|---:|---:|:---|
| 598 | 524 | 74 | **FAIL** |

## BY CATEGORY

| Category | Pass rate | OK | Failed | Total | Avg | Stddev | Min | Max |
|---|:---|---:|---:|---:|---:|---:|---:|---:|
| `bucket_logging` | **83%** (5/6) | 5 | 1 | 6 | 2.507s | 0.345s | 2.033s | 3.039s |
| `bucket_policy` | **100%** (12/12) | 12 | 0 | 12 | 2.764s | 0.705s | 2.064s | 4.307s |
| `checksum` | **100%** (11/11) | 11 | 0 | 11 | 8.029s | 4.695s | 2.076s | 17.426s |
| `conditional_write` | **100%** (7/7) | 7 | 0 | 7 | 7.117s | 3.499s | 3.370s | 14.076s |
| `copy` | **100%** (31/31) | 31 | 0 | 31 | 6.158s | 5.995s | 1.448s | 24.435s |
| `delete_marker` | **100%** (3/3) | 3 | 0 | 3 | 3.507s | 1.063s | 2.043s | 4.535s |
| `encryption` | **61%** (66/108) | 66 | 42 | 108 | 3.478s | 5.429s | 1.288s | 47.491s |
| `lifecycle` | **100%** (15/15) | 15 | 0 | 15 | 1.528s | 0.244s | 1.284s | 2.317s |
| `lifecycle_expiration` | **100%** (6/6) | 6 | 0 | 6 | 12.263s | 22.980s | 1.815s | 63.647s |
| `list_objects_v2` | **98%** (46/47) | 46 | 1 | 47 | 3.567s | 1.693s | 0.734s | 12.410s |
| `s3_core` | **91%** (296/324) | 296 | 28 | 324 | 8.200s | 43.866s | 0.720s | 497.193s |
| `sse_s3` | **67%** (2/3) | 2 | 1 | 3 | 1.472s | 0.044s | 1.438s | 1.534s |
| `tagging` | **96%** (24/25) | 24 | 1 | 25 | 4.006s | 4.838s | 1.453s | 26.940s |

## Run details

```
TEST RUN
  Provider  : fth
  Collected : 838
  Passed    : 524
  Failed    : 74
  Error     : 0
  Skipped   : 5
  Duration  : 3838.1s
  Marks     : not fails_on_aws
  Filter    : (none)
  Passes    : main (not (object_lock)), quarantine (object_lock)
  Target    : s3tests/functional/test_s3.py
  Raw JSON  : ../logs/20260714_122455_compatibility_pytest_main.json, ../logs/20260714_122455_compatibility_pytest_quarantine.json
```

## Errors

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_bucket_acl_default</summary>

**Test description**

> GetBucketAcl on a freshly created bucket; expects a single FULL_CONTROL grant to the bucket owner.

**Error stack trace** — `s3_core` — `failed` — 1.483s

```pytb
s3tests/functional/test_s3.py:3946: in test_bucket_acl_default
    assert response['Owner']['DisplayName'] == display_name
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_bucket_acl_canned</summary>

**Test description**

> PutBucketAcl with canned ACL public-read; GetBucketAcl reflects the public-read grant.

**Error stack trace** — `s3_core` — `failed` — 1.522s

```pytb
s3tests/functional/test_s3.py:4007: in test_bucket_acl_canned
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_bucket_acl_canned_publicreadwrite</summary>

**Test description**

> PutBucketAcl public-read-write applies READ + WRITE grants to AllUsers.

**Error stack trace** — `s3_core` — `failed` — 1.352s

```pytb
s3tests/functional/test_s3.py:4056: in test_bucket_acl_canned_publicreadwrite
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_bucket_acl_canned_authenticatedread</summary>

**Test description**

> PutBucketAcl authenticated-read applies READ to AuthenticatedUsers group.

**Error stack trace** — `s3_core` — `failed` — 1.403s

```pytb
s3tests/functional/test_s3.py:4096: in test_bucket_acl_canned_authenticatedread
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_put_bucket_acl_grant_group_read</summary>

**Test description**

> PutBucketAcl with a Group grantee for READ permission; GetBucketAcl reflects it.

**Error stack trace** — `s3_core` — `failed` — 1.691s

```pytb
s3tests/functional/test_s3.py:4131: in test_put_bucket_acl_grant_group_read
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_object_acl_default</summary>

**Test description**

> New objects have a single FULL_CONTROL grant to the bucket owner.

**Error stack trace** — `s3_core` — `failed` — 2.539s

```pytb
s3tests/functional/test_s3.py:4165: in test_object_acl_default
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_object_acl_canned_during_create</summary>

**Test description**

> PutObject with ACL=public-read sets that canned ACL on creation.

**Error stack trace** — `s3_core` — `failed` — 2.689s

```pytb
s3tests/functional/test_s3.py:4191: in test_object_acl_canned_during_create
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_object_acl_canned</summary>

**Test description**

> PutObjectAcl with canned public-read; GetObjectAcl reflects the new grant.

**Error stack trace** — `s3_core` — `failed` — 2.872s

```pytb
s3tests/functional/test_s3.py:4225: in test_object_acl_canned
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_object_acl_canned_publicreadwrite</summary>

**Test description**

> PutObjectAcl public-read-write; GetObjectAcl shows READ + WRITE grants to AllUsers.

**Error stack trace** — `s3_core` — `failed` — 3.038s

```pytb
s3tests/functional/test_s3.py:4277: in test_object_acl_canned_publicreadwrite
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_object_acl_canned_authenticatedread</summary>

**Test description**

> PutObjectAcl authenticated-read; GetObjectAcl shows READ to AuthenticatedUsers.

**Error stack trace** — `s3_core` — `failed` — 2.116s

```pytb
s3tests/functional/test_s3.py:4318: in test_object_acl_canned_authenticatedread
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_object_acl_canned_bucketownerread</summary>

**Test description**

> PutObjectAcl bucket-owner-read; bucket owner gets READ on objects owned by another user.

**Error stack trace** — `s3_core` — `failed` — 2.239s

```pytb
s3tests/functional/test_s3.py:4360: in test_object_acl_canned_bucketownerread
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '220' == 'FilOne Compat alt User'
E     
E     [0m[91m- FilOne Compat alt User[39;49;00m[90m[39;49;00m
E     [92m+ 220[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_object_acl_canned_bucketownerfullcontrol</summary>

**Test description**

> PutObjectAcl bucket-owner-full-control transfers ownership-equivalent grants to the bucket owner.

**Error stack trace** — `s3_core` — `failed` — 2.512s

```pytb
s3tests/functional/test_s3.py:4402: in test_object_acl_canned_bucketownerfullcontrol
    check_grants(
s3tests/functional/test_s3.py:3929: in check_grants
    assert g['Grantee'].pop('DisplayName', None) == w['DisplayName']
E   AssertionError: assert '220' == 'FilOne Compat alt User'
E     
E     [0m[91m- FilOne Compat alt User[39;49;00m[90m[39;49;00m
E     [92m+ 220[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_access_bucket_private_object_private</summary>

**Test description**

> Both private; alt user cannot GET either object, ListObjects, or PUT.

**Error stack trace** — `s3_core` — `failed` — 2.506s

```pytb
s3tests/functional/test_s3.py:5097: in test_access_bucket_private_object_private
    check_access_denied(alt_client.list_objects, Bucket=bucket_name)
s3tests/functional/test_s3.py:3904: in check_access_denied
    e = assert_raises(ClientError, fn, *args, **kwargs)
        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
s3tests/functional/utils.py:19: in assert_raises
    raise AssertionError("%s not raised" % excName)
E   AssertionError: ClientError not raised
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_access_bucket_private_objectv2_private</summary>

**Test description**

> Both bucket and object ACLs private; alt user fails GET on either object, ListObjectsV2 on the bucket, and PUT to any key.

**Error stack trace** — `list_objects_v2` — `failed` — 2.8s

```pytb
s3tests/functional/test_s3.py:5125: in test_access_bucket_private_objectv2_private
    check_access_denied(alt_client.list_objects_v2, Bucket=bucket_name)
s3tests/functional/test_s3.py:3904: in check_access_denied
    e = assert_raises(ClientError, fn, *args, **kwargs)
        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
s3tests/functional/utils.py:19: in assert_raises
    raise AssertionError("%s not raised" % excName)
E   AssertionError: ClientError not raised
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_access_bucket_publicread_object_private</summary>

**Test description**

> Bucket public-read, object private; alt user can ListObjects but cannot GET the private object.

**Error stack trace** — `s3_core` — `failed` — 3.624s

```pytb
s3tests/functional/test_s3.py:5238: in test_access_bucket_publicread_object_private
    objs = get_objects_list(bucket=bucket_name, client=alt_client3)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
s3tests/functional/__init__.py:70: in get_objects_list
    response = client.list_objects(Bucket=bucket)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.AccessDenied: An error occurred (AccessDenied) when calling the ListObjects operation: Access Denied
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_access_bucket_publicreadwrite_object_private</summary>

**Test description**

> Bucket public-read-write, object private; alt user can ListObjects and PUT; GET on the private object fails.

**Error stack trace** — `s3_core` — `failed` — 3.715s

```pytb
s3tests/functional/test_s3.py:5306: in test_access_bucket_publicreadwrite_object_private
    alt_client.put_object(Bucket=bucket_name, Key=newkey, Body='newcontent')
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.AccessDenied: An error occurred (AccessDenied) when calling the PutObject operation: Access Denied
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_access_bucket_publicreadwrite_object_publicreadwrite</summary>

**Test description**

> Both public-read-write; alt user has full operational access.

**Error stack trace** — `s3_core` — `failed` — 3.083s

```pytb
s3tests/functional/test_s3.py:5336: in test_access_bucket_publicreadwrite_object_publicreadwrite
    alt_client.put_object(Bucket=bucket_name, Key=key2, Body='baroverwrite')
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.AccessDenied: An error occurred (AccessDenied) when calling the PutObject operation: Access Denied
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_list_multipart_upload_owner</summary>

**Test description**

> ListMultipartUploads returns the Owner who initiated each upload.

**Error stack trace** — `s3_core` — `failed` — 2.804s

```pytb
s3tests/functional/test_s3.py:6574: in test_list_multipart_upload_owner
    match(uploads1[0], key1, upload1, user1, name1)
s3tests/functional/test_s3.py:6567: in match
    assert upload['Initiator']['DisplayName'] == username
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_100_continue</summary>

**Test description**

> PutObject sends Expect:100-continue; server returns 100 before body is sent.

**Error stack trace** — `s3_core` — `failed` — 1.411s

```pytb
s3tests/functional/test_s3.py:6860: in test_100_continue
    assert status == '403'
E   AssertionError: assert '100' == '403'
E     
E     [0m[91m- 403[39;49;00m[90m[39;49;00m
E     [92m+ 100[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_cors_presigned_get_object_v2</summary>

**Test description**

> SigV2 variant.

**Error stack trace** — `s3_core` — `failed` — 0.72s

```pytb
s3tests/functional/test_s3.py:7095: in test_cors_presigned_get_object_v2
    _test_cors_options_presigned_method(
s3tests/functional/test_s3.py:7043: in _test_cors_options_presigned_method
    bucket_name = _setup_bucket_object_acl('public-read', 'public-read', client=client)
                  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
s3tests/functional/test_s3.py:3282: in _setup_bucket_object_acl
    client.create_bucket(ACL=bucket_acl, Bucket=bucket_name)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.exceptions.ClientError: An error occurred (SignatureDoesNotMatch) when calling the CreateBucket operation: The request signature we calculated does not match the signature you provided.
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_cors_presigned_get_object_tenant_v2</summary>

**Test description**

> Tenant + SigV2 variant.

**Error stack trace** — `s3_core` — `failed` — 0.777s

```pytb
s3tests/functional/test_s3.py:7102: in test_cors_presigned_get_object_tenant_v2
    _test_cors_options_presigned_method(
s3tests/functional/test_s3.py:7043: in _test_cors_options_presigned_method
    bucket_name = _setup_bucket_object_acl('public-read', 'public-read', client=client)
                  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
s3tests/functional/test_s3.py:3282: in _setup_bucket_object_acl
    client.create_bucket(ACL=bucket_acl, Bucket=bucket_name)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.exceptions.ClientError: An error occurred (SignatureDoesNotMatch) when calling the CreateBucket operation: The request signature we calculated does not match the signature you provided.
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_cors_presigned_put_object_v2</summary>

**Test description**

> SigV2 variant.

**Error stack trace** — `s3_core` — `failed` — 0.722s

```pytb
s3tests/functional/test_s3.py:7122: in test_cors_presigned_put_object_v2
    _test_cors_options_presigned_method(
s3tests/functional/test_s3.py:7043: in _test_cors_options_presigned_method
    bucket_name = _setup_bucket_object_acl('public-read', 'public-read', client=client)
                  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
s3tests/functional/test_s3.py:3282: in _setup_bucket_object_acl
    client.create_bucket(ACL=bucket_acl, Bucket=bucket_name)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.exceptions.ClientError: An error occurred (SignatureDoesNotMatch) when calling the CreateBucket operation: The request signature we calculated does not match the signature you provided.
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_cors_presigned_put_object_tenant_v2</summary>

**Test description**

> Tenant + SigV2 variant.

**Error stack trace** — `s3_core` — `failed` — 0.737s

```pytb
s3tests/functional/test_s3.py:7129: in test_cors_presigned_put_object_tenant_v2
    _test_cors_options_presigned_method(
s3tests/functional/test_s3.py:7043: in _test_cors_options_presigned_method
    bucket_name = _setup_bucket_object_acl('public-read', 'public-read', client=client)
                  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
s3tests/functional/test_s3.py:3282: in _setup_bucket_object_acl
    client.create_bucket(ACL=bucket_acl, Bucket=bucket_name)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.exceptions.ClientError: An error occurred (SignatureDoesNotMatch) when calling the CreateBucket operation: The request signature we calculated does not match the signature you provided.
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_versioned_object_acl</summary>

**Test description**

> GetObjectAcl with a specific VersionId returns default owner FULL_CONTROL; PutObjectAcl ACL='public-read' with VersionId scopes the grant to that version; new put_object creates a fresh version with default ACL.

**Error stack trace** — `s3_core` — `failed` — 3.423s

```pytb
s3tests/functional/test_s3.py:8252: in test_versioned_object_acl
    assert response['Owner']['DisplayName'] == display_name
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_versioned_object_acl_no_version_specified</summary>

**Test description**

> PutObjectAcl without VersionId targets the current head version; verifies that ACL change is observable via GetObjectAcl with the head VersionId.

**Error stack trace** — `s3_core` — `failed` — 3.968s

```pytb
s3tests/functional/test_s3.py:8321: in test_versioned_object_acl_no_version_specified
    assert response['Owner']['DisplayName'] == display_name
E   AssertionError: assert '219' == 'FilOne Compat main User'
E     
E     [0m[91m- FilOne Compat main User[39;49;00m[90m[39;49;00m
E     [92m+ 219[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_method_head</summary>

**Test description**

> After SSE-KMS PutObject, HeadObject returns x-amz-server-side-encryption=aws:kms and the key id; HeadObject sent with SSE-KMS request headers expects 400.

**Error stack trace** — `encryption` — `failed` — 1.392s

```pytb
s3tests/functional/test_s3.py:11244: in test_sse_kms_method_head
    client.put_object(Bucket=bucket_name, Key=key, Body=data)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_present</summary>

**Test description**

> SSE-KMS PutObject and GetObject without re-sending KMS headers; body must come back intact.

**Error stack trace** — `encryption` — `failed` — 1.552s

```pytb
s3tests/functional/test_s3.py:11271: in test_sse_kms_present
    client.put_object(Bucket=bucket_name, Key=key, Body=data)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_multipart_upload</summary>

**Test description**

> SSE-KMS multipart upload of 30 MB; verifies length, metadata, Content-Type, body, and range reads.

**Error stack trace** — `encryption` — `failed` — 1.29s

```pytb
s3tests/functional/test_s3.py:11327: in test_sse_kms_multipart_upload
    (upload_id, data, parts) = _multipart_upload_enc(client, bucket_name, key, objlen,
s3tests/functional/test_s3.py:10860: in _multipart_upload_enc
    response = client.create_multipart_upload(Bucket=bucket_name, Key=key, Metadata=metadata)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CreateMultipartUpload operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_multipart_invalid_chunks_1</summary>

**Test description**

> SSE-KMS multipart with different KMS key ids between init and parts (no assertion — just verifies the upload helper attempts the call).

**Error stack trace** — `encryption` — `failed` — 1.453s

```pytb
s3tests/functional/test_s3.py:11377: in test_sse_kms_multipart_invalid_chunks_1
    _multipart_upload_enc(client, bucket_name, key, objlen, part_size=5*1024*1024,
s3tests/functional/test_s3.py:10860: in _multipart_upload_enc
    response = client.create_multipart_upload(Bucket=bucket_name, Key=key, Metadata=metadata)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CreateMultipartUpload operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_multipart_invalid_chunks_2</summary>

**Test description**

> SSE-KMS multipart where parts use a non-existent KMS key id (no assertion — just verifies the upload helper attempts the call).

**Error stack trace** — `encryption` — `failed` — 1.539s

```pytb
s3tests/functional/test_s3.py:11403: in test_sse_kms_multipart_invalid_chunks_2
    _multipart_upload_enc(client, bucket_name, key, objlen, part_size=5*1024*1024,
s3tests/functional/test_s3.py:10860: in _multipart_upload_enc
    response = client.create_multipart_upload(Bucket=bucket_name, Key=key, Metadata=metadata)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CreateMultipartUpload operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_post_object_authenticated_request</summary>

**Test description**

> POST presigned upload with SSE-KMS conditions; subsequent GET returns the body.

**Error stack trace** — `encryption` — `failed` — 1.941s

```pytb
s3tests/functional/test_s3.py:11448: in test_sse_kms_post_object_authenticated_request
    assert r.status_code == 204
E   assert 400 == 204
E    +  where 400 = <Response [400]>.status_code
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_transfer_1b</summary>

**Test description**

> SSE-KMS round-trip at 1 byte. Skipped when [s3 main] has no kms_keyid.

**Error stack trace** — `encryption` — `failed` — 1.663s

```pytb
s3tests/functional/test_s3.py:11460: in test_sse_kms_transfer_1b
    _test_sse_kms_customer_write(1, key_id = kms_keyid)
s3tests/functional/test_s3.py:11222: in _test_sse_kms_customer_write
    client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_transfer_1kb</summary>

**Test description**

> SSE-KMS round-trip at 1 KB. Skipped when [s3 main] has no kms_keyid.

**Error stack trace** — `encryption` — `failed` — 1.593s

```pytb
s3tests/functional/test_s3.py:11469: in test_sse_kms_transfer_1kb
    _test_sse_kms_customer_write(1024, key_id = kms_keyid)
s3tests/functional/test_s3.py:11222: in _test_sse_kms_customer_write
    client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_transfer_1MB</summary>

**Test description**

> SSE-KMS round-trip at 1 MB. Skipped when [s3 main] has no kms_keyid.

**Error stack trace** — `encryption` — `failed` — 1.748s

```pytb
s3tests/functional/test_s3.py:11478: in test_sse_kms_transfer_1MB
    _test_sse_kms_customer_write(1024*1024, key_id = kms_keyid)
s3tests/functional/test_s3.py:11222: in _test_sse_kms_customer_write
    client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_transfer_13b</summary>

**Test description**

> SSE-KMS round-trip at 13 bytes. Skipped when [s3 main] has no kms_keyid.

**Error stack trace** — `encryption` — `failed` — 1.576s

```pytb
s3tests/functional/test_s3.py:11487: in test_sse_kms_transfer_13b
    _test_sse_kms_customer_write(13, key_id = kms_keyid)
s3tests/functional/test_s3.py:11222: in _test_sse_kms_customer_write
    client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_bucket_policy_put_obj_kms_noenc</summary>

**Test description**

> Policy requires `aws:kms` SSE and forbids unencrypted; KMS PutObject succeeds, unencrypted is denied. Skipped when [s3 main] has no kms_keyid configured.

**Error stack trace** — `encryption` — `failed` — 1.446s

```pytb
s3tests/functional/test_s3.py:13140: in test_bucket_policy_put_obj_kms_noenc
    response = client.put_object(Bucket=bucket_name, Key=key1_str,
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_bucket_policy_put_obj_request_obj_tag</summary>

**Test description**

> Policy allows PutObject only when `s3:RequestObjectTag/security=public`; alt user is denied without the tag header and succeeds with `x-amz-tagging: security=public`.

**Error stack trace** — `tagging` — `failed` — 1.453s

```pytb
s3tests/functional/test_s3.py:13216: in test_bucket_policy_put_obj_request_obj_tag
    alt_client.put_object(Bucket=bucket_name, Key=key1_str, Body=key1_str)
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.AccessDenied: An error occurred (AccessDenied) when calling the PutObject operation: Access Denied
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_get_bucket_encryption_s3</summary>

**Test description**

> GetBucketEncryption on a fresh bucket returns ServerSideEncryptionConfigurationNotFoundError; after Put it returns the SSE-S3 rule.

**Error stack trace** — `sse_s3` — `failed` — 1.443s

```pytb
s3tests/functional/test_s3.py:14555: in test_get_bucket_encryption_s3
    assert response_code == 'ServerSideEncryptionConfigurationNotFoundError'
E   AssertionError: assert '' == 'ServerSideEn...NotFoundError'
E     
E     [0m[91m- ServerSideEncryptionConfigurationNotFoundError[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_get_bucket_encryption_kms</summary>

**Test description**

> GetBucketEncryption on a fresh bucket returns ServerSideEncryptionConfigurationNotFoundError; after Put it returns the SSE-KMS rule with KMSMasterKeyID.

**Error stack trace** — `encryption` — `failed` — 1.459s

```pytb
s3tests/functional/test_s3.py:14578: in test_get_bucket_encryption_kms
    assert response_code == 'ServerSideEncryptionConfigurationNotFoundError'
E   AssertionError: assert '' == 'ServerSideEn...NotFoundError'
E     
E     [0m[91m- ServerSideEncryptionConfigurationNotFoundError[39;49;00m[90m[39;49;00m
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_default_upload_1b</summary>

**Test description**

> With SSE-KMS bucket default, plain PutObject at 1 byte; the stored object must come back with aws:kms encryption and the configured key id.

**Error stack trace** — `encryption` — `failed` — 1.425s

```pytb
s3tests/functional/test_s3.py:14707: in test_sse_kms_default_upload_1b
    _test_sse_kms_default_upload(1)
s3tests/functional/test_s3.py:14692: in _test_sse_kms_default_upload
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_default_upload_1kb</summary>

**Test description**

> SSE-KMS bucket-default upload at 1 KB.

**Error stack trace** — `encryption` — `failed` — 1.325s

```pytb
s3tests/functional/test_s3.py:14714: in test_sse_kms_default_upload_1kb
    _test_sse_kms_default_upload(1024)
s3tests/functional/test_s3.py:14692: in _test_sse_kms_default_upload
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_default_upload_1mb</summary>

**Test description**

> SSE-KMS bucket-default upload at 1 MB.

**Error stack trace** — `encryption` — `failed` — 1.487s

```pytb
s3tests/functional/test_s3.py:14721: in test_sse_kms_default_upload_1mb
    _test_sse_kms_default_upload(1024*1024)
s3tests/functional/test_s3.py:14692: in _test_sse_kms_default_upload
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_default_upload_8mb</summary>

**Test description**

> SSE-KMS bucket-default upload at 8 MB.

**Error stack trace** — `encryption` — `failed` — 1.647s

```pytb
s3tests/functional/test_s3.py:14728: in test_sse_kms_default_upload_8mb
    _test_sse_kms_default_upload(8*1024*1024)
s3tests/functional/test_s3.py:14692: in _test_sse_kms_default_upload
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_sse_kms_default_post_object_authenticated_request</summary>

**Test description**

> POST presigned upload to a bucket with SSE-KMS default; the resulting object reports aws:kms and the key id. Skipped when [s3 main] has no kms_keyid.

**Error stack trace** — `encryption` — `failed` — 1.42s

```pytb
s3tests/functional/test_s3.py:14890: in test_sse_kms_default_post_object_authenticated_request
    assert r.status_code == 204
E   assert 400 == 204
E    +  where 400 = <Response [400]>.status_code
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_put_bucket_logging_errors</summary>

**Test description**

> Negative tests for PutBucketLogging — invalid target bucket, missing policy, malformed TargetObjectKeyFormat, etc.

**Error stack trace** — `bucket_logging` — `failed` — 3.039s

```pytb
s3tests/functional/test_s3.py:16605: in test_put_bucket_logging_errors
    assert False, 'expected failure'
E   AssertionError: expected failure
E   assert False
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_create_bucket_bucket_owner_enforced</summary>

**Test description**

> CreateBucket with ObjectOwnership=BucketOwnerEnforced disables ACLs entirely.

**Error stack trace** — `s3_core` — `failed` — 2.092s

```pytb
s3tests/functional/test_s3.py:20291: in test_create_bucket_bucket_owner_enforced
    _test_object_ownership_bucket_owner_enforced(get_alt_client(), bucket, bucket_owner)
s3tests/functional/test_s3.py:20163: in _test_object_ownership_bucket_owner_enforced
    assert bucket_owner == get_object_acl_owner(client, bucket, 'put-object-no-acl')
E   AssertionError: assert ('219', 'FilO...at main User') == ('220', '220')
E     
E     At index 0 diff: [0m[33m'[39;49;00m[33m219[39;49;00m[33m'[39;49;00m[90m[39;49;00m != [0m[33m'[39;49;00m[33m220[39;49;00m[33m'[39;49;00m[90m[39;49;00m
E     Use -v to get more diff
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_create_bucket_bucket_owner_preferred</summary>

**Test description**

> CreateBucket with BucketOwnerPreferred causes new objects to be owned by the bucket owner when uploaded with bucket-owner-full-control.

**Error stack trace** — `s3_core` — `failed` — 2.696s

```pytb
s3tests/functional/test_s3.py:20303: in test_create_bucket_bucket_owner_preferred
    _test_object_ownership_bucket_owner_preferred(get_alt_client(), bucket, bucket_owner)
s3tests/functional/test_s3.py:20204: in _test_object_ownership_bucket_owner_preferred
    assert bucket_owner == get_object_acl_owner(client, bucket, 'put-object-bucket-owner-full-control')
E   AssertionError: assert ('219', 'FilO...at main User') == ('220', '220')
E     
E     At index 0 diff: [0m[33m'[39;49;00m[33m219[39;49;00m[33m'[39;49;00m[90m[39;49;00m != [0m[33m'[39;49;00m[33m220[39;49;00m[33m'[39;49;00m[90m[39;49;00m
E     Use -v to get more diff
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_put_bucket_ownership_bucket_owner_enforced</summary>

**Test description**

> PutBucketOwnershipControls flipping a bucket to BucketOwnerEnforced disables ACLs.

**Error stack trace** — `s3_core` — `failed` — 2.297s

```pytb
s3tests/functional/test_s3.py:20340: in test_put_bucket_ownership_bucket_owner_enforced
    _test_object_ownership_bucket_owner_enforced(get_alt_client(), bucket, bucket_owner)
s3tests/functional/test_s3.py:20163: in _test_object_ownership_bucket_owner_enforced
    assert bucket_owner == get_object_acl_owner(client, bucket, 'put-object-no-acl')
E   AssertionError: assert ('219', 'FilO...at main User') == ('220', '220')
E     
E     At index 0 diff: [0m[33m'[39;49;00m[33m219[39;49;00m[33m'[39;49;00m[90m[39;49;00m != [0m[33m'[39;49;00m[33m220[39;49;00m[33m'[39;49;00m[90m[39;49;00m
E     Use -v to get more diff
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_put_bucket_ownership_bucket_owner_preferred</summary>

**Test description**

> PutBucketOwnershipControls to BucketOwnerPreferred.

**Error stack trace** — `s3_core` — `failed` — 2.574s

```pytb
s3tests/functional/test_s3.py:20353: in test_put_bucket_ownership_bucket_owner_preferred
    _test_object_ownership_bucket_owner_preferred(get_alt_client(), bucket, bucket_owner)
s3tests/functional/test_s3.py:20204: in _test_object_ownership_bucket_owner_preferred
    assert bucket_owner == get_object_acl_owner(client, bucket, 'put-object-bucket-owner-full-control')
E   AssertionError: assert ('219', 'FilO...at main User') == ('219', '219')
E     
E     At index 1 diff: [0m[33m'[39;49;00m[33mFilOne Compat main User[39;49;00m[33m'[39;49;00m[90m[39;49;00m != [0m[33m'[39;49;00m[33m219[39;49;00m[33m'[39;49;00m[90m[39;49;00m
E     Use -v to get more diff
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_part_enc[sse-s3-sse-kms-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized UploadPartCopy matrix across (source_mode_key, dest_mode_key, source_storage_class, dest_storage_class, obj_size); verifies that encryption-mode transitions during copy preserve bytes.

**Error stack trace** — `encryption` — `failed` — 3.685s

```pytb
s3tests/functional/test_s3.py:20708: in test_copy_part_enc
    _test_copy_part_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20536: in _test_copy_part_enc
    response = client.create_multipart_upload(Bucket=dest_bucket_name, Key='testobj2', **upload_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CreateMultipartUpload operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_part_enc[sse-c-sse-kms-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized UploadPartCopy matrix across (source_mode_key, dest_mode_key, source_storage_class, dest_storage_class, obj_size); verifies that encryption-mode transitions during copy preserve bytes.

**Error stack trace** — `encryption` — `failed` — 3.298s

```pytb
s3tests/functional/test_s3.py:20708: in test_copy_part_enc
    _test_copy_part_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20536: in _test_copy_part_enc
    response = client.create_multipart_upload(Bucket=dest_bucket_name, Key='testobj2', **upload_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CreateMultipartUpload operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_part_enc[sse-kms-sse-s3-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized UploadPartCopy matrix across (source_mode_key, dest_mode_key, source_storage_class, dest_storage_class, obj_size); verifies that encryption-mode transitions during copy preserve bytes.

**Error stack trace** — `encryption` — `failed` — 1.657s

```pytb
s3tests/functional/test_s3.py:20708: in test_copy_part_enc
    _test_copy_part_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20528: in _test_copy_part_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_part_enc[sse-kms-sse-c-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized UploadPartCopy matrix across (source_mode_key, dest_mode_key, source_storage_class, dest_storage_class, obj_size); verifies that encryption-mode transitions during copy preserve bytes.

**Error stack trace** — `encryption` — `failed` — 1.639s

```pytb
s3tests/functional/test_s3.py:20708: in test_copy_part_enc
    _test_copy_part_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20528: in _test_copy_part_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_part_enc[sse-kms-sse-kms-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized UploadPartCopy matrix across (source_mode_key, dest_mode_key, source_storage_class, dest_storage_class, obj_size); verifies that encryption-mode transitions during copy preserve bytes.

**Error stack trace** — `encryption` — `failed` — 1.606s

```pytb
s3tests/functional/test_s3.py:20708: in test_copy_part_enc
    _test_copy_part_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20528: in _test_copy_part_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-s3-sse-kms-STANDARD-STANDARD-1]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 3.178s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-s3-sse-kms-STANDARD-STANDARD-1024]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 2.632s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-s3-sse-kms-STANDARD-STANDARD-1048576]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 5.555s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-s3-sse-kms-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 2.775s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-c-sse-kms-STANDARD-STANDARD-1]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 2.839s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-c-sse-kms-STANDARD-STANDARD-1024]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 2.972s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-c-sse-kms-STANDARD-STANDARD-1048576]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 3.035s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-c-sse-kms-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 3.362s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20506: in _test_copy_enc
    response = client.copy_object(Bucket=dest_bucket_name, Key='testobj2', CopySource={'Bucket': bucket_name, 'Key': 'testobj'}, **copy_args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the CopyObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-s3-STANDARD-STANDARD-1]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.428s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-s3-STANDARD-STANDARD-1024]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.373s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-s3-STANDARD-STANDARD-1048576]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.485s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-s3-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.518s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-c-STANDARD-STANDARD-1]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.405s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-c-STANDARD-STANDARD-1024]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.47s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-c-STANDARD-STANDARD-1048576]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.634s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-c-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.532s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-kms-STANDARD-STANDARD-1]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.355s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-kms-STANDARD-STANDARD-1024]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.332s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-kms-STANDARD-STANDARD-1048576]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.582s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

<details markdown="1">
<summary>s3tests/functional/test_s3.py::test_copy_enc[sse-kms-sse-kms-STANDARD-STANDARD-8388608]</summary>

**Test description**

> Parametrized CopyObject matrix across encryption modes and storage classes; verifies same behavior at the single-part copy level.

**Error stack trace** — `encryption` — `failed` — 1.571s

```pytb
s3tests/functional/test_s3.py:20753: in test_copy_enc
    _test_copy_enc(obj_size, source_mode_key, dest_mode_key, source_storage_class, dest_storage_class)
s3tests/functional/test_s3.py:20497: in _test_copy_enc
    response = client.put_object(Bucket=bucket_name, Key='testobj', Body=data, **args)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:602: in _api_call
    return self._make_api_call(operation_name, kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/context.py:123: in wrapper
    return func(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^
../.venv/lib/python3.14/site-packages/botocore/client.py:1078: in _make_api_call
    raise error_class(parsed_response, operation_name)
E   botocore.errorfactory.InvalidRequest: An error occurred (InvalidRequest) when calling the PutObject operation: InvalidRequest
```

</details>

