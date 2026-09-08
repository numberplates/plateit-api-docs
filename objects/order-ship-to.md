# OrderShipTo

`https://api.plateit.co.uk/v3/orders/{order_id}/ship-to`

> This is a singleton resource.

An [Order](/objects/order.md) can have a single `OrderShipTo` shipping address. The data in this resource is passed to the appropriate shipment provider.

It can be overridden at the [OrderPackage](/objects/order-package.md) level by creating an optional [OrderPackageShipToOverride](/objects/order-package-ship-to-override.md).

## Data References

### Attributes

* **order_id** `integer` The ID of the [Order](/objects/order.md) the resource belongs to.
* **first_name** `string` The customer's first name.
* **last_name** `string` The customer's last name.
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

**POST** `/v3/orders/{order_id}/ship-to`

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

Returns the created `OrderShipTo` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/ship-to`

Returns the order's `OrderShipTo`.

## Update

!> Requires the `orders_customer_write` permission.

**PATCH** `/v3/orders/{order_id}/ship-to`

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

Returns the updated `OrderShipTo`.

## Delete

!> Requires the `orders_customer_write` permission.

**DELETE** `/v3/orders/{order_id}/ship-to`

Deletes the order's `OrderShipTo`.
