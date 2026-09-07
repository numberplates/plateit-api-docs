# OrderDocument

`https://api.plateit.co.uk/v3/orders/{order_id}/documents`

An `OrderDocument` represents a supporting document supplied for an [Order](/objects/order.md), such as proof of identity or entitlement to use a vehicle registration.

Orders containing plates that require supporting documentation cannot become ready for fulfilment until all required documents have been supplied and approved.

> Note: *all* OrderDocuments (not just the ones pertaining to a single order) can be retrieved at `https://api.plateit.co.uk/v3/documents`.

> The overall document state of an order is reflected by its [SystemOrderDocumentStatus](/objects/system-order-document-status.md).

## Data References

### Attributes

* **id** `integer` The unique ID of the document.
* **order_id** `integer` The ID of the [Order](/objects/order.md) the document belongs to.
* **type** `string` The document type.
* **subtype** `string` The document subtype.
* **registration** `string|null` The vehicle registration the document relates to, where applicable.
* **mime_type** `string` The detected MIME type of the uploaded file.
* **size** `integer` The file size in bytes.
* **status** `string` The current approval status of the document.
* **rejection_reason** `string|null` The reason the document was rejected, where applicable.
* **approved_at** `string|null` The timestamp at which the document was approved, in ISO 8601 format.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Document Types

The following document types are supported:

* **id** - Proof of identity.
* **entitlement** - Proof of entitlement to use a vehicle registration.

An entitlement document is associated with the relevant vehicle `registration`.

## Document Statuses

An `OrderDocument` can have one of the following statuses:

* **pending** - The document has been uploaded and is awaiting review.
* **approved** - The document has been reviewed and approved.
* **rejected** - The document has been reviewed and rejected.

> These individual document statuses are separate from the aggregate [SystemOrderDocumentStatus](/objects/system-order-document-status.md) applied to the parent order.

## Relationships

The following relationships may be included:

* [order](/objects/order.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/{order_id}/documents/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/documents`

Returns a collection of `OrderDocument` resources associated with the order.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/documents/{document_id}`

Returns the requested `OrderDocument`.

## Create

!> Requires the `orders_documents_upload` permission.

**POST** `/v3/orders/{order_id}/documents`

Creates an `OrderDocument` from a previously uploaded temporary file.

See the [order documents guide](/fundamentals/order-documents.md) for the complete upload and replacement workflow.

## Request Upload URL

!> Requires the `orders_documents_upload` permission.

**POST** `/v3/orders/{order_id}/documents/upload`

Returns a temporary URL that can be used to upload a supporting document directly to private storage.

See the [order documents guide](/fundamentals/order-documents.md) for usage.

## Update

!> Requires the `orders_documents_write` permission.

**PATCH** `/v3/orders/{order_id}/documents/{document_id}`

Updates the approval status of the document.

A rejected document must include a valid `rejection_reason`.

## File

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/documents/{document_id}/file`

Provides temporary access to the document's private file.

## Delete

!> Requires the `orders_documents_write` permission.

**DELETE** `/v3/orders/{order_id}/documents/{document_id}`

Deletes the specified `OrderDocument` and its associated file.
