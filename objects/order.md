# Order

`https://data.plateit.co.uk/v3/orders`

The order object is the outermost parent resource that represents an order. Most of its attributes are read-only and are automatically updated when changes to the child resources occur, for example, when a [plate](/objects/order-package-plate.md) is added to a [package](/objects/order-package.md) that belongs to an order.

## Data References

### Attributes

* **id** `integer` The unique ID of the order.
* **company_id** `integer` The ID of the [company](/objects/company.md) the order belongs to.
* **system_order_status_id** `integer` The [system order status](/objects/system-order-status.md) ID.
* **system_order_fulfilment_status_id** `integer` The [system order fulfilment status](/objects/system-order-fulfilment-status.md) ID.
* **price_subtotal** `integer` The sum of all items in pence, minus shipping.
* **price_shipping** `integer` The total shipping costs in pence.
* **price_total** `integer` The order's grand total in pence.
* **amount_paid** `integer` The total amount paid in pence.
* **amount_refunded** `integer` The total amount refunded in pence.
* **packages_count** `integer` The number of [packages](/objects/order-package.md) pertaining to the order.
* **is_dummy** `boolean` Indicates a test (dummy) order.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [company](/objects/company.md)
* [system_order_status](/objects/system-order-status.md)
* [system_order_fulfilment_status](/objects/system-order-fulfilment-status.md)
* [send_to](/objects/order-send-to.md)
* [packages](/objects/order-package.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* is_dummy
* created_at
* company.id
* company.name
* system_order_status.id
* system_order_status.name
* system_order_fulfilment_status.id
* system_order_fulfilment_status.name

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_dummy
* company.id
* company.name
* system_order_status.id
* system_order_status.name
* system_order_fulfilment_status.id
* system_order_fulfilment_status.name

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

## Test (Dummy) Orders

A dummy order can be created by passing `is_dummy` `true` when creating a new order.

Dummy orders will be ignored in reports, and any delegations will NOT appear in the delegated company's print queue.

An existing order cannot be updated to become a dummy order at a later time or vice versa.

## Example Requests

### Create an Order

!> Requires the `orders_write` permission.

> If you want to create an entire order in one request, including plates, products and shipping, consider using the [place-order](/actions/place-order.md) endpoint. This may be better suited for applications with a customer-facing checkout facility.

<!-- tabs:start -->

#### **Body Parameters**

* **system_order_status_id** `integer|null` A valid [system order status](/objects/system-order-status.md) ID. Defaults to `5` (Draft).
* **is_dummy** `boolean|null` Defaults to `false`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders`
* Method: `POST`

```json
{}
```

#### **Response**

* Status code: `201`

```json
{
  "id": 100,
  "company_id": 1,
  "system_order_status_id": 5,
  "system_order_fulfilment_status_id": 1,
  "price_subtotal": 0,
  "price_shipping": 0,
  "price_total": 0,
  "amount_paid": 0,
  "amount_refunded": 0,
  "packages_count": 0,
  "is_dummy": false,
  "created_at": "2024-05-24T09:15:20.000000Z",
  "updated_at": "2024-05-24T09:15:20.000000Z",
  "href": "/orders/100"
}
```

<!-- tabs:end -->

### Retrieve an Order

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 100,
  "company_id": 1,
  "system_order_status_id": 3,
  "system_order_fulfilment_status_id": 1,
  "price_subtotal": 0,
  "price_shipping": 0,
  "price_total": 0,
  "amount_paid": 0,
  "amount_refunded": 0,
  "packages_count": 0,
  "is_dummy": false,
  "created_at": "2024-05-24T09:15:20.000000Z",
  "updated_at": "2024-05-24T09:15:20.000000Z",
  "href": "/orders/100"
}
```

<!-- tabs:end -->

### List Orders

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 99,
      "company_id": 1,
      "system_order_status_id": 2,
      "system_order_fulfilment_status_id": 2,
      "price_subtotal": 2000,
      "price_shipping": 500,
      "price_total": 2500,
      "amount_paid": 2500,
      "amount_refunded": 0,
      "packages_count": 0,
      "is_dummy": false,
      "created_at": "2024-05-24T09:14:56.000000Z",
      "updated_at": "2024-05-24T09:14:56.000000Z",
      "href": "/orders/99"
    },
    {
      "id": 100,
      "company_id": 1,
      "system_order_status_id": 3,
      "system_order_fulfilment_status_id": 1,
      "price_subtotal": 0,
      "price_shipping": 0,
      "price_total": 0,
      "amount_paid": 0,
      "amount_refunded": 0,
      "packages_count": 0,
      "is_dummy": false,
      "created_at": "2024-05-24T09:15:20.000000Z",
      "updated_at": "2024-05-24T09:15:20.000000Z",
      "href": "/orders/100"
    }
  ]
}
```

<!-- tabs:end -->

### Update an Order

!> Requires the `orders_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **system_order_status_id** `integer|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}`
* Method: `PATCH`

```json
{
  "system_order_status_id": 3
}
```

#### **Response**

* Status code: `200`

```json
{
  "id": 100,
  "company_id": 1,
  "system_order_status_id": 3,
  "system_order_fulfilment_status_id": 1,
  "price_subtotal": 0,
  "price_shipping": 0,
  "price_total": 0,
  "amount_paid": 0,
  "amount_refunded": 0,
  "packages_count": 0,
  "is_dummy": false,
  "created_at": "2024-05-24T09:15:20.000000Z",
  "updated_at": "2024-05-24T09:15:55.000000Z",
  "href": "/orders/100"
}
```

<!-- tabs:end -->

### Delete an Order

!> Requires the `orders_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->