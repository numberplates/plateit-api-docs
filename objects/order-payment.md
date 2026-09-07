# OrderPayment

`https://api.plateit.co.uk/v3/orders/{order_id}/payments`

An [Order](/objects/order.md) can have multiple `OrderPayment` resources representing payments received against the order.

Manual payments can be created and deleted directly through the API. Payments from supported external providers are created automatically when Plateit receives and verifies the provider's webhook.

> For PayPal payment integration, see the [PayPal guide](/fundamentals/paypal.md).

## Data References

### Attributes

* **id** `integer` The unique ID of the payment.
* **order_id** `integer` The ID of the [Order](/objects/order.md) the payment belongs to.
* **system_payment_provider_id** `integer` The ID of the [SystemPaymentProvider](/objects/system-payment-provider.md).
* **transaction_reference** `string` The payment transaction reference.
* **amount** `integer` The gross payment amount in pence.
* **transaction_fee** `integer` The payment provider transaction fee in pence.
* **note** `string|null` An optional note associated with the payment.
* **amount_refunded** `integer` The total amount refunded against this payment in pence.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [order](/objects/order.md)
* [system_payment_provider](/objects/system-payment-provider.md)
* [refunds](/objects/order-payment-refund.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/{order_id}/payments/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## Create

!> Requires the `orders_payments_write` permission.

**POST** `/v3/orders/{order_id}/payments`

Only manual payments can be created directly using this endpoint.

### Body Parameters

* **amount** `integer` The gross payment amount in pence.
* **note** `string|null` Optional note associated with the payment.

### Example Payload

```json
{
  "amount": 24000,
  "note": "Payment received by bank transfer."
}
```

Returns the created `OrderPayment` with status `201`.

> Payments from external providers such as PayPal are not created manually. Plateit creates them automatically after receiving and verifying the provider webhook.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/payments/{payment_id}`

Returns the requested `OrderPayment`.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/payments`

Returns a collection of `OrderPayment` resources belonging to the specified order.

## Update

`OrderPayment` resources cannot be updated.

## Delete

!> Requires the `orders_payments_write` permission.

**DELETE** `/v3/orders/{order_id}/payments/{payment_id}`

Only manual payments can be deleted.

Deletes the specified `OrderPayment`.
