# SystemOrderFulfilmentStatus

`https://data.plateit.co.uk/v3/system-order-fulfilment-statuses`

!> Read only

An order fulfilment status is automatically applied to an order when the despatch state of one or more of its packages change.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/system-order-fulfilment-statuses`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "name": "Unfulfilled",
      "description": "The order has been completed and is awaiting manufacture.",
      "href": "/system-order-fulfilment-statuses/1"
    },
    {
      "id": 2,
      "name": "Partially Fulfilled",
      "description": "At least one package in the order has been despatched.",
      "href": "/system-order-fulfilment-statuses/2"
    },
    {
      "id": 3,
      "name": "Fulfilled",
      "description": "All packages in the order have been despatched.",
      "href": "/system-order-fulfilment-statuses/3"
    }
  ]
}
```

<!-- tabs:end -->