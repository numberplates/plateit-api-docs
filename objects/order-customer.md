# Send To

`https://data.plateit.co.uk/v3/orders/{order_id}/customer`

An [order](/objects/order.md) can have a single customer. The data in this object is passed to the appropriate shipment provider.

> This is a singleton resource.

## Data References

### Attributes

* **order_id** `integer` The order ID the resource belongs to.
* **first_name** `string` The customer's first name.
* **last_name** `string` The customer's last name.
* **email** `string` The customer's email.
* **phone_number** `string|null` The customer's phone number (optional).
* **mobile_number** `string|null` The customer's mobile number (optional).
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Example Requests

### Create an Address

!> Requires the `orders_customer_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **first_name** `string`
* **last_name** `string`
* **email** `string`
* **phone_number** `string|null`
* **mobile_number** `string|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/customer`
* Method: `POST`

```json
{
  "first_name": "John",
  "last_name": "Turcotte",
  "email": "john_turcotte@example.com",
  "mobile_number": "07777777777"
}
```

#### **Response**

* Status code: `201`

```json
{
  "order_id": 51342,
  "first_name": "John",
  "last_name": "Turcotte",
  "email": "john_turcotte@example.com",
  "phone_number": null,
  "mobile_number": "07777777777",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-10-10T15:42:08.000000Z",
  "href": "/orders/51342/customer"
}
```

<!-- tabs:end -->

### Retrieve an Address

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/customer`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "order_id": 51342,
  "first_name": "John",
  "last_name": "Turcotte",
  "email": "john_turcotte@example.com",
  "phone_number": null,
  "mobile_number": "07777777777",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-10-10T15:42:08.000000Z",
  "href": "/orders/51342/customer"
}
```

<!-- tabs:end -->

### Update an Address

!> Requires the `orders_customer_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **first_name** `string|null`
* **last_name** `string|null`
* **email** `string|null`
* **phone_number** `string|null`
* **mobile_number** `string|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/customer`
* Method: `PATCH`

```json
{
  "email": "new_email_address@example.com"
}
```

#### **Response**

* Status code: `200`

```json
{
  "order_id": 51342,
  "first_name": "John",
  "last_name": "Turcotte",
  "email": "new_email_address@example.com",
  "phone_number": null,
  "mobile_number": "07777777777",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-11-10T07:21:23.000000Z",
  "href": "/orders/51342/customer"
}
```

<!-- tabs:end -->

### Delete an Address

!> Requires the `orders_customer_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/customer`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->