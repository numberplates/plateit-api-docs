# OrderPaymentRefund

`https://api.plateit.co.uk/v3/orders/{order_id}/payments/{payment_id}/refunds`

An [OrderPayment](/objects/order-payment.md) can have multiple `OrderPaymentRefund` resources representing refunds issued against that payment.

Refunds can be created and retrieved only. They cannot be updated or deleted.

## Data References

### Attributes

* **id** `integer` The unique ID of the refund.
* **payment_id** `integer` The ID of the [OrderPayment](/objects/order-payment.md) the refund belongs to.
* **refund_reference** `string` The unique reference associated with the refund.
* **amount** `integer` The gross refund amount in pence.
* **transaction_fee** `integer` The transaction fee associated with the refund, in pence.
* **reason** `string|null` An optional reason for the refund.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [payment](/objects/order-payment.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/{order_id}/payments/{payment_id}/refunds/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## Create

!> Requires the `orders_payments_refunds_write` permission.

**POST** `/v3/orders/{order_id}/payments/{payment_id}/refunds`

Creates a refund against the specified payment.

### Body Parameters

* **amount** `integer` The gross refund amount in pence.
* **reason** `string|null` Optional reason for the refund.

### Example Payload

```json id="mimc5a"
{
  "amount": 500,
  "reason": "Customer returned the item."
}
```

Returns the created `OrderPaymentRefund` with status `201`.

> If the original payment was received through an external payment provider, Plateit will attempt to process the refund through that provider, provided the payment integration settings have been completed for that gateway. The `OrderPaymentRefund` is created only if the provider confirms the refund was successful.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/payments/{payment_id}/refunds/{refund_id}`

Returns the requested `OrderPaymentRefund`.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/payments/{payment_id}/refunds`

Returns a collection of `OrderPaymentRefund` resources belonging to the specified payment.

## Update

`OrderPaymentRefund` resources cannot be updated.

## Delete

`OrderPaymentRefund` resources cannot be deleted.
