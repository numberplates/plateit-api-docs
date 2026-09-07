# OrderCustomer

`https://api.plateit.co.uk/v3/orders/{order_id}/customer`

> This is a singleton resource.

An [Order](/objects/order.md) can have a single `OrderCustomer`. This resource stores the customer's contact details for the order.

## Data References

### Attributes

* **order_id** `integer` The ID of the [Order](/objects/order.md) the resource belongs to.
* **first_name** `string` The customer's first name.
* **last_name** `string` The customer's last name.
* **email** `string` The customer's email address.
* **phone_number** `string|null` The customer's phone number.
* **mobile_number** `string|null` The customer's mobile number.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Create

!> Requires the `orders_customer_write` permission.

**POST** `/v3/orders/{order_id}/customer`

### Body Parameters

* **first_name** `string`
* **last_name** `string`
* **email** `string`
* **phone_number** `string|null`
* **mobile_number** `string|null`

### Example Payload

```json
{
  "first_name": "John",
  "last_name": "Turcotte",
  "email": "john_turcotte@example.com",
  "mobile_number": "07777777777"
}
```

Returns the created `OrderCustomer` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/customer`

Returns the order's `OrderCustomer`.

## Update

!> Requires the `orders_customer_write` permission.

**PATCH** `/v3/orders/{order_id}/customer`

### Body Parameters

All fields are optional:

* **first_name** `string`
* **last_name** `string`
* **email** `string`
* **phone_number** `string|null`
* **mobile_number** `string|null`

### Example Payload

```json
{
  "email": "new_email_address@example.com"
}
```

Returns the updated `OrderCustomer`.

## Delete

!> Requires the `orders_customer_write` permission.

**DELETE** `/v3/orders/{order_id}/customer`

Deletes the order's `OrderCustomer`.
