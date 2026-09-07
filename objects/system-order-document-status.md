# SystemOrderDocumentStatus

`https://api.plateit.co.uk/v3/system-order-document-statuses`

!> Read only

A `SystemOrderDocumentStatus` represents the overall supporting-document state of an [Order](/objects/order.md). It is maintained automatically based on whether the order requires supporting documents and the current state of its associated [OrderDocument](/objects/order-documents.md) objects.

## Data References

### Attributes

* **id** `integer` The unique ID of the document status.
* **name** `string` The name of the document status.
* **description** `string` A description of what the status represents.
* **href** `string` The path to the resource.

## Values

The following document statuses are available:

```json
[
  {
    "id": 1,
    "name": "Not Required",
    "description": "The order does not require supporting documentation."
  },
  {
    "id": 2,
    "name": "Awaiting Upload",
    "description": "One or more required documents have not yet been supplied."
  },
  {
    "id": 3,
    "name": "Awaiting Approval",
    "description": "All required documents have been supplied and are awaiting approval."
  },
  {
    "id": 4,
    "name": "Approved",
    "description": "All required documentation has been approved."
  }
]
```

> An order may be fully paid while still having a document status of `Awaiting Upload` or `Awaiting Approval`. The order will remain in a draft state until all required supporting documents have been approved.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-order-document-statuses/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-order-document-statuses`

Returns a collection of `SystemOrderDocumentStatus` resources.
