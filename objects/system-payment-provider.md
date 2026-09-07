# SystemPaymentProvider

`https://api.plateit.co.uk/v3/system-payment-providers`

!> Read only

A `SystemPaymentProvider` represents a supported payment provider that will be associated with an [OrderPayment](/objects/order-payment.md).

## Data References

### Attributes

* **id** `integer` The unique ID of the payment provider.
* **name** `string` The name of the payment provider.
* **href** `string` The path to the resource.

## Values

The following payment providers are available:

```json
[
  {
    "id": 1,
    "name": "Manual"
  },
  {
    "id": 2,
    "name": "PayPal"
  },
  {
    "id": 3,
    "name": "Stripe"
  }
]
```

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-payment-providers/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-payment-providers`

Returns a collection of `SystemPaymentProvider` resources.
