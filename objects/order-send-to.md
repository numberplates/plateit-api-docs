# Send To

`https://data.plateit.co.uk/v3/orders/{order_id}/send-to`

The "send to" object consists of the customer's details, including their shipping address. The data in this object is passed to the appropriate shipment provider.

> This is a singleton resource.

## Data References

### Attributes

* **order_id** `integer` The order ID the resource belongs to.
* **first_name** `string` The customer's first name.
* **last_name** `string` The customer's last name.
* **email** `string` The customer's email.
* **phone_number** `string|null` The customer's phone number (optional).
* **mobile_number** `string|null` The customer's mobile number (optional).
* **address_line_1** `string` The first line of the address.
* **address_line_2** `string|null` The second line of the address (optional).
* **address_line_3** `string` The city.
* **address_postcode** `string` The postcode.
* **address_country_code** `string` The two-character ISO country code, such as "GB".
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Example Requests

### Create an Address

!> Requires the `orders_address_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **first_name** `string`
* **last_name** `string`
* **email** `string`
* **phone_number** `string|null`
* **mobile_number** `string|null`
* **address_line_1** `string`
* **address_line_2** `string|null`
* **address_line_3** `string`
* **address_postcode** `string` 
* **address_country_code** `string`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/send-to`
* Method: `POST`

```json
{
  "first_name": "John",
  "last_name": "Turcotte",
  "email": "john_turcotte@example.com",
  "mobile_number": "07777777777",
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
  "email": "john_turcotte@example.com",
  "phone_number": null,
  "mobile_number": "07777777777",
  "address_line_1": "78 Croft Way",
  "address_line_2": null,
  "address_line_3": "Port Jaron",
  "address_postcode": "HP23 2WB",
  "address_country_code": "GB",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-10-10T15:42:08.000000Z",
  "href": "/orders/51342/send-to"
}
```

<!-- tabs:end -->

### Retrieve an Address

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/send-to`
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
  "address_line_1": "78 Croft Way",
  "address_line_2": null,
  "address_line_3": "Port Jaron",
  "address_postcode": "HP23 2WB",
  "address_country_code": "GB",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-10-10T15:42:08.000000Z",
  "href": "/orders/51342/send-to"
}
```

<!-- tabs:end -->


### Update an Address

!> Requires the `orders_address_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **first_name** `string|null`
* **last_name** `string|null`
* **email** `string|null`
* **phone_number** `string|null`
* **mobile_number** `string|null`
* **address_line_1** `string|null`
* **address_line_2** `string|null`
* **address_line_3** `string|null`
* **address_postcode** `string|null`
* **address_country_code** `string|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/send-to`
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
  "address_line_1": "78 Croft Way",
  "address_line_2": null,
  "address_line_3": "Port Jaron",
  "address_postcode": "HP23 2WB",
  "address_country_code": "GB",
  "created_at": "2024-10-10T15:42:08.000000Z",
  "updated_at": "2024-11-10T07:21:23.000000Z",
  "href": "/orders/51342/send-to"
}
```

<!-- tabs:end -->

### Delete an Address

!> Requires the `orders_address_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/send-to`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->