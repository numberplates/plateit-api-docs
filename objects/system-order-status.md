# SystemOrderStatus

`https://data.plateit.co.uk/v3/system-order-statuses`

!> Read only

Each [Order](/objects/order.md) has an associated system order status. It is used to categorise and filter the orders.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/system-order-statuses`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "name": "External Draft",
      "description": "The order has been created externally, for example, by a customer on a website or app, but not yet completed.",
      "href": "/system-order-statuses/1"
    },
    {
      "id": 2,
      "name": "Internal Draft",
      "description": "The order has been created internally by a member of staff and is awaiting further action.",
      "href": "/system-order-statuses/2"
    },
    {
      "id": 3,
      "name": "Open",
      "description": "The order is open, and its committed packages are ready for processing.",
      "href": "/system-order-statuses/3"
    },
    {
      "id": 4,
      "name": "Closed",
      "description": "The order has been closed and archived.",
      "href": "/system-order-statuses/4"
    },
    {
      "id": 5,
      "name": "Cancelled",
      "description": "The order has been cancelled.",
      "href": "/system-order-statuses/5"
    }
  ]
}
```

<!-- tabs:end -->