# SystemWebhookEvent

`https://api.plateit.co.uk/v3/system-webhook-events`

!> Read only

A `SystemWebhookEvent` represents an event that can trigger a webhook notification.

## Data References

### Attributes

* **id** `integer` The unique ID of the webhook event.
* **event_key** `string` The unique event key used when configuring webhooks.
* **description** `string` A description of when the event is triggered.
* **href** `string` The path to the resource.

## Values

The following webhook events are available:

```json
[
  {
    "id": 1,
    "event_key": "order:place",
    "description": "When an order is paid in full. Required to notify a customer of a successful order placement."
  },
  {
    "id": 2,
    "event_key": "order-package:status-update",
    "description": "When the status of a package is updated."
  },
  {
    "id": 3,
    "event_key": "order-document:status-update",
    "description": "When the status of a supporting document is updated."
  }
]
```

> An `order:place` event may be triggered while the order is still in a draft state, for example when required supporting documents are still awaiting approval.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-webhook-events/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-webhook-events`

Returns a collection of `SystemWebhookEvent` resources.
