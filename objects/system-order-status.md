# SystemOrderStatus

`https://api.plateit.co.uk/v3/system-order-statuses`

!> Read only

A `SystemOrderStatus` represents the lifecycle state of an [Order](/objects/order.md). The status is derived from the state of the order's packages rather than being set directly by the API consumer.

* An order is considered a draft if none of its associated packages have been committed.
* An order is considered open if one or more of its associated packages have been committed.
* An order is considered closed if all of its associated packages are in a state of despatched or cancelled.

## Data References

### Attributes

* **id** `integer` The unique ID of the order status.
* **name** `string` The name of the order status.
* **description** `string` A description of what the status represents.
* **href** `string` The path to the resource.

## Values

The following order statuses are available:

```json
[
  {
    "id": 1,
    "name": "External Draft",
    "description": "The order has been created externally, for example, by a customer on a website or app, but is not yet in a fulfillable state."
  },
  {
    "id": 2,
    "name": "Internal Draft",
    "description": "The order has been created internally by a member of staff but is not yet in a fulfillable state."
  },
  {
    "id": 3,
    "name": "Open",
    "description": "The order is in a fulfillable state and ready for processing."
  },
  {
    "id": 4,
    "name": "Closed",
    "description": "The order has been closed and archived."
  }
]
```

> An order may be fully paid while still remaining in a draft state, for example while required supporting documents are awaiting approval.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-order-statuses/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-order-statuses`

Returns a collection of `SystemOrderStatus` resources.
