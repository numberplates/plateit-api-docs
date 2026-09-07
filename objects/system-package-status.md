# SystemPackageStatus

`https://api.plateit.co.uk/v3/system-package-statuses`

!> Read only

A `SystemPackageStatus` represents the processing and fulfilment state of an [OrderPackage](/objects/order-package.md). It is used to categorise and filter packages.

## Data References

### Attributes

* **id** `integer` The unique ID of the package status.
* **name** `string` The name of the package status.
* **description** `string` A description of what the status represents.
* **href** `string` The path to the resource.

## Values

The following package statuses are available:

```json
[
  {
    "id": 1,
    "name": "Unprocessed",
    "description": "The contents of the package are waiting to be processed."
  },
  {
    "id": 2,
    "name": "Processing",
    "description": "The contents of the package are actively being processed."
  },
  {
    "id": 3,
    "name": "Processed",
    "description": "The contents of the package have been processed."
  },
  {
    "id": 4,
    "name": "Despatched",
    "description": "The package has been despatched."
  },
  {
    "id": 5,
    "name": "Held",
    "description": "The package is in a held state, awaiting further action."
  },
  {
    "id": 6,
    "name": "Cancelled",
    "description": "The fulfilment of the package has been cancelled."
  }
]
```

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-package-statuses/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-package-statuses`

Returns a collection of `SystemPackageStatus` resources.
