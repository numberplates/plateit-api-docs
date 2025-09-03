# OrderShipTo

`https://api.plateit.co.uk/v3/orders/{order_id}/ship-to`

> This is a singleton resource.

An [Order](/objects/order.md) can have a single shipping address. The data in this object is passed to the appropriate shipment provider. It can be overridden at the OrderPackage level by creating an optional [OrderPackageShipToOverride](/objects/order-package-ship-to-override.md) object.

## Data References

### Attributes

* **order_id** `integer` The [Order](/objects/order.md) ID the resource belongs to.
* **first_name** `string` The customer's first name.
* **last_name** `string` The customer's last name.
* **address_line_1** `string` The first line of the address.
* **address_line_2** `string|null` The second line of the address (optional).
* **address_line_3** `string` The city.
* **address_postcode** `string` The postcode.
* **address_country_code** `string` The two-character ISO country code, such as "GB".
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [order](/objects/order.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

## Example Requests

### Create

!> Requires the `orders_customer_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **first_name** `string`
* **last_name** `string`
* **address_line_1** `string`
* **address_line_2** `string|null`
* **address_line_3** `string`
* **address_postcode** `string` 
* **address_country_code** `string`

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/ship-to`
* Method: `POST`

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

#### **Response**

* Status code: `201`

```json
{
  "order_id": 51342,
  "first_name": "John",
  "last_name": "Turcotte",
  "address_line_1": "78 Croft Way",
  "address_line_2": null,
  "address_line_3": "Port Jaron",
  "address_postcode": "HP23 2WB",
  "address_country_code": "GB",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-10-10T15:42:08.000000Z",
  "href": "/orders/51342/ship-to"
}
```

<!-- tabs:end -->

### Retrieve

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/ship-to`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "order_id": 51342,
  "first_name": "John",
  "last_name": "Turcotte",
  "address_line_1": "78 Croft Way",
  "address_line_2": null,
  "address_line_3": "Port Jaron",
  "address_postcode": "HP23 2WB",
  "address_country_code": "GB",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-10-10T15:42:08.000000Z",
  "href": "/orders/51342/ship-to"
}
```

<!-- tabs:end -->

### Update

!> Requires the `orders_customer_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **first_name** `string|null`
* **last_name** `string|null`
* **address_line_1** `string|null`
* **address_line_2** `string|null`
* **address_line_3** `string|null`
* **address_postcode** `string|null`
* **address_country_code** `string|null`

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/ship-to`
* Method: `PATCH`

```json
{
  "first_name": "Johnny"
}
```

#### **Response**

* Status code: `200`

```json
{
  "order_id": 51342,
  "first_name": "Johnny",
  "last_name": "Turcotte",
  "address_line_1": "78 Croft Way",
  "address_line_2": null,
  "address_line_3": "Port Jaron",
  "address_postcode": "HP23 2WB",
  "address_country_code": "GB",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-11-10T07:21:23.000000Z",
  "href": "/orders/51342/ship-to"
}
```

<!-- tabs:end -->

### Delete

!> Requires the `orders_customer_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/ship-to`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->