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
      "name": "Pending",
      "description": "The order has been created externally but not yet completed.",
      "href": "/system-order-statuses/1"
    },
    {
      "id": 2,
      "name": "Open",
      "description": "The order is open and is awaiting processing.",
      "href": "/system-order-statuses/2"
    },
    {
      "id": 3,
      "name": "Closed",
      "description": "The order has been closed and archived.",
      "href": "/system-order-statuses/3"
    },
    {
      "id": 4,
      "name": "Cancelled",
      "description": "The order has been cancelled.",
      "href": "/system-order-statuses/4"
    },
    {
      "id": 5,
      "name": "Draft",
      "description": "The order is in a draft state.",
      "href": "/system-order-statuses/5"
    }
  ]
}
```

<!-- tabs:end -->