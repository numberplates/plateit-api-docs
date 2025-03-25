# SystemWebhookEvent

`https://data.plateit.co.uk/v3/system-webhook-events`

!> Read only

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/system-webhook-events`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "event_key": "order:place",
      "description": "When a payment is received to activate (open) an external or internal draft order. Required to notify a customer of a successful order placement."
    },
    {
      "id": 2,
      "event_key": "order-package:status-update",
      "description": "When the status of a package is updated."
    },
    {
      "id": 3,
      "event_key": "order-package:despatch-status-update",
      "description": "When the despatch status of a package is updated."
    }
  ]
}
```

<!-- tabs:end -->