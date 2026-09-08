# OrderBillTo

`https://api.plateit.co.uk/v3/orders/{order_id}/bill-to`

> This is a singleton resource.

An [Order](/objects/order.md) can have a single `OrderBillTo` billing address.

!> A billing address is only required when it is different from the [OrderShipTo](/objects/order-ship-to.md) shipping address.

## Data References

### Attributes

* **order_id** `integer` The ID of the [Order](/objects/order.md) the resource belongs to.
* **first_name** `string` The payer's first name.
* **last_name** `string` The payer's last name.
* **address_line_1** `string` The first line of the address.
* **address_line_2** `string|null` The second line of the address.
* **address_line_3** `string` The city or locality.
* **address_postcode** `string` The postcode.
* **address_country_code** `string` The two-character ISO country code, such as `GB`.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Create

!> Requires the `orders_customer_write` permission.

**POST** `/v3/orders/{order_id}/bill-to`

### Body Parameters

* **first_name** `string`
* **last_name** `string`
* **address_line_1** `string`
* **address_line_2** `string|null`
* **address_line_3** `string`
* **address_postcode** `string`
* **address_country_code** `string`

### Example Payload

```json
{
  "first_name": "John",
  "last_name": "Turcotte",
  "address_line_1": "78 Croft Way",
  "address_line_3": "Port Jaron",
  "address_postcode": "HP23 2WB",
  "address_country_code": "GB"
}
```

Returns the created `OrderBillTo` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/bill-to`

Returns the order's `OrderBillTo`.

## Update

!> Requires the `orders_customer_write` permission.

**PATCH** `/v3/orders/{order_id}/bill-to`

### Body Parameters

All fields are optional when updating this resource type.

* **first_name** `string`
* **last_name** `string`
* **address_line_1** `string`
* **address_line_2** `string|null`
* **address_line_3** `string`
* **address_postcode** `string`
* **address_country_code** `string`

### Example Payload

```json
{
  "first_name": "Johnny"
}
```

Returns the updated `OrderBillTo`.

## Delete

!> Requires the `orders_customer_write` permission.

**DELETE** `/v3/orders/{order_id}/bill-to`

Deletes the order's `OrderBillTo`.
