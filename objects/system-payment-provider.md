# System Payment Provider

`https://data.plateit.co.uk/v3/system-payment-providers`

!> Read only

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/system-payment-providers`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "name": "Manual",
      "href": "/system-payment-providers/1"
    },
    {
      "id": 2,
      "name": "PayPal",
      "href": "/system-payment-providers/2"
    }
  ]
}
```

<!-- tabs:end -->