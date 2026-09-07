# SystemOrderFulfilmentStatus

`https://api.plateit.co.uk/v3/system-order-fulfilment-statuses`

!> Read only

A `SystemOrderFulfilmentStatus` represents the fulfilment state of an order. It is applied automatically as the despatch state of one or more of the order's packages changes (it is not set directly by the API consumer).

## Data References

### Attributes

* **id** `integer` The unique ID of the fulfilment status.
* **name** `string` The name of the fulfilment status.
* **description** `string` A description of what the status represents.
* **href** `string` The path to the resource.

## Values

The following fulfilment statuses are available:

```json
[
  {
    "id": 1,
    "name": "Unfulfilled",
    "description": "The order has been completed and is awaiting manufacture."
  },
  {
    "id": 2,
    "name": "Partially Fulfilled",
    "description": "At least one package in the order has been despatched."
  },
  {
    "id": 3,
    "name": "Fulfilled",
    "description": "All packages in the order have been despatched."
  }
]
```

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-order-fulfilment-statuses/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-order-fulfilment-statuses`

Returns a collection of `SystemOrderFulfilmentStatus` resources.
