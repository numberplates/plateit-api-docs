# Supporting Documents

Supporting documents are used to verify a customer's identity and their entitlement to use a vehicle registration.

Plateit determines whether an [Order](/objects/order.md) requires supporting documentation based on the contents of its packages. Where supporting documents are required, the order cannot become ready for fulfilment until all required documents have been supplied and approved.

The overall document state of the order is exposed through its [SystemOrderDocumentStatus](/objects/system-order-document-status.md).

## Document Requirements

There are two types of supporting document:

* **id** — Proof of the customer's identity.
* **entitlement** — Proof that the customer is entitled to use a particular vehicle registration.

An order may require:

* one identity document;
* one entitlement document for each registration requiring supporting documentation.

Only plates configured as requiring documentation contribute to these requirements.

## Checking What Is Required

The order's document collection can be used to determine which supporting documents have already been supplied.

**GET** `/v3/orders/{order_id}/documents`

The response also indicates any outstanding document requirements.

> The order's [SystemOrderDocumentStatus](/objects/system-order-document-status.md) provides a convenient aggregate status, but the document collection should be used when you need to know the specific outstanding requirements.

## Upload Process

!> Requires the `orders_documents_upload` permission.

Documents are uploaded directly to temporary private storage rather than being sent through the Plateit API.

The process consists of three steps:

1. Request a temporary upload URL from Plateit.
2. Upload the file directly to the returned URL.
3. Create the [OrderDocument](/objects/order-documents.md) using the returned temporary path.

Supported file types are:

* JPEG
* PNG
* PDF

The maximum file size is **5 MB**.

### Step 1 — Request an Upload URL

Plateit first provides a temporary signed URL that can be used to upload the file directly to private storage.

<!-- tabs:start -->

#### **Body Parameters**

* **type** `string` The document type. Either `id` or `entitlement`.
* **subtype** `string` The specific document subtype.
* **registration** `string|null` Required for entitlement documents and prohibited for identity documents.
* **mime_type** `string` The MIME type of the file being uploaded.
* **size** `integer` The file size in bytes.

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/documents/upload`
* Method: `POST`

```json
{
  "type": "id",
  "subtype": "driving_licence",
  "mime_type": "image/jpeg",
  "size": 284193
}
```

#### **Response**

* Status code: `200`

```json
{
  "path": "tmp/documents/51342/01JXYZ123456789_example.jpg",
  "url": "https://...",
  "headers": {
    "Content-Type": "image/jpeg"
  },
  "expires_at": "2027-09-07T15:45:00.000000Z"
}
```

<!-- tabs:end -->

The response contains:

* **path** `string` The temporary storage path. Keep this value for step 3.
* **url** `string` The temporary signed URL used to upload the file directly to storage.
* **headers** `object` The headers that must be included with the upload request.
* **expires_at** `string` The expiry time of the upload URL in ISO 8601 format.

> Registration values are normalised before validation, so spaces do not affect matching.

For an entitlement document, the request would also include the registration:

```json
{
  "type": "entitlement",
  "subtype": "v5c",
  "registration": "AB12 CDE",
  "mime_type": "application/pdf",
  "size": 481227
}
```

### Step 2 — Upload the File

The file must now be uploaded directly to the `url` returned in step 1.

<!-- tabs:start -->

#### **Request**

* Endpoint: `{url}`
* Method: `PUT`
* Headers:
  * Content-Type: `image/jpeg`

The request body should contain the raw file contents.

#### **Response**

A successful response confirms that the file has been uploaded to temporary storage.

<!-- tabs:end -->

!> Do not send the document file to the Plateit API. The upload URL points directly to private object storage.

The headers returned in step 1 should be treated as part of the upload contract and included with this request.

### Step 3 — Create the OrderDocument

Once the file has uploaded successfully, create the [OrderDocument](/objects/order-documents.md) using the temporary `path` returned in step 1.

<!-- tabs:start -->

#### **Body Parameters**

* **type** `string` The document type.
* **subtype** `string` The specific document subtype.
* **registration** `string|null` Required for entitlement documents and prohibited for identity documents.
* **path** `string` The temporary storage path returned in step 1.

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/documents`
* Method: `POST`

```json
{
  "type": "id",
  "subtype": "driving_licence",
  "path": "tmp/documents/51342/01JXYZ123456789_example.jpg"
}
```

#### **Response**

* Status code: `201`

Returns the created [OrderDocument](/objects/order-documents.md).

<!-- tabs:end -->

For an entitlement document:

```json
{
  "type": "entitlement",
  "subtype": "v5c",
  "registration": "AB12 CDE",
  "path": "tmp/documents/51342/01JXYZ987654321_example.pdf"
}
```

When the document is created, Plateit validates the uploaded file before moving it into permanent private storage.

Validation includes checking:

* the temporary path belongs to the correct order;
* the uploaded file exists;
* the actual file size is within the permitted limit;
* the actual file type is supported.

## Document Review

!> Requires the `orders_documents_write` permission.

Uploaded documents are reviewed by updating their [OrderDocument](/objects/order-documents.md) resource.

### Approve

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/documents/{document_id}`
* Method: `PATCH`

```json
{
  "status": "approved"
}
```

#### **Response**

* Status code: `200`

Returns the updated `OrderDocument`.

<!-- tabs:end -->

Approving a document records its approval time and clears any previous rejection reason.

### Reject

A rejected document must include a valid `rejection_reason`.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/documents/{document_id}`
* Method: `PATCH`

```json
{
  "status": "rejected",
  "rejection_reason": "document_unreadable"
}
```

#### **Response**

* Status code: `200`

Returns the updated `OrderDocument`.

<!-- tabs:end -->

The available rejection reasons are:

* **id_not_permitted**
* **reg_does_not_match**
* **document_too_old**
* **document_unreadable**
* **document_incomplete**
* **wrong_document_type**
* **other**

## Replacing a Rejected Document

!> Requires the `orders_documents_upload` permission.

A rejected document can be replaced by repeating the normal three-step upload process for the same document requirement.

When the replacement is completed:

* the existing `OrderDocument` is reused;
* its status returns to `pending`;
* `rejection_reason` is cleared;
* `approved_at` is cleared;
* the previous file is replaced by the new upload.

A document that is currently pending or approved cannot be replaced.

## Accessing a Document File

!> Requires the `orders_read` permission.

Supporting document files are private.

By default, requesting the file endpoint redirects to a temporary signed URL for the underlying document.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/documents/{document_id}/file`
* Method: `GET`

#### **Response**

* Status code: `302`

Redirects to a temporary signed URL for the private document file.

<!-- tabs:end -->

If you do not want the API to redirect automatically, pass `redirect=false`.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/documents/{document_id}/file`
* Method: `GET`
* Query:
  * redirect: `false`

#### **Response**

* Status code: `200`

```json
{
  "url": "https://...",
  "expires_at": "2027-09-07T16:30:00.000000Z"
}
```

<!-- tabs:end -->

The returned `url` provides temporary access to the private document file until the `expires_at` time.

## Deleting a Document

!> Requires the `orders_documents_write` permission.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/documents/{document_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

<!-- tabs:end -->

Deleting an `OrderDocument` also removes its associated private file.

## Order Lifecycle

Supporting documents contribute to determining whether a paid draft order is ready for fulfilment.

An order may therefore be fully paid while still remaining in a draft state if one or more required documents are:

* awaiting upload;
* awaiting approval.

When the final required supporting document is approved, a fully paid draft order can automatically become `Open`, and its uncancelled packages are committed for fulfilment.

See [SystemOrderStatus](/objects/system-order-status.md) and [SystemOrderDocumentStatus](/objects/system-order-document-status.md) for the corresponding order-level statuses.
