# Order

`https://data.plateit.co.uk/v3/orders`

The Order object is the outermost parent resource that represents an order. Most of its attributes are read-only and are automatically updated when changes to the child resources occur, for example, when an [OrderPackagePlate](/objects/order-package-plate.md) object is created or updated pertaining to the order.

## Data References

### Attributes

* **id** `integer` The unique ID of the order.
* **company_id** `integer` The ID of the [Company](/objects/company.md) the order belongs to.
* **system_order_status_id** `integer` The [SystemOrderStatus](/objects/system-order-status.md) ID.
* **system_order_fulfilment_status_id** `integer` The [SystemOrderFulfilmentStatus](/objects/system-order-fulfilment-status.md) ID.
* **amount_subtotal** `integer` The sum of all items in pence, minus shipping and VAT.
* **amount_shipping** `integer` The total shipping costs in pence.
* **amount_vat** `integer` The total VAT in pence.
* **amount_total** `integer` The order's grand total in pence.
* **amount_paid** `integer` The total amount paid in pence.
* **amount_refunded** `integer` The total amount refunded in pence.
* **amount_vat_collected** `integer` The total amount of VAT collected in pence, proportionate to the amount paid.
* **amount_vat_refunded** `integer` The total amount of VAT refunded in pence, proportionate to the amount refunded.
* **packages_count** `integer` The number of [OrderPackage](/objects/order-package.md) objects pertaining to the order.
* **is_dummy** `boolean` Indicates a test (dummy) order.
* **opened_at** `string|null` The timestamp of when the order first had its status changed to `Open`, in ISO 8601 format.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [company](/objects/company.md)
* [system_order_status](/objects/system-order-status.md)
* [system_order_fulfilment_status](/objects/system-order-fulfilment-status.md)
* [customer](/objects/order-customer.md)
* [ship_to](/objects/order-ship-to.md)
* [bill_to](/objects/order-bill-to.md)
* [packages](/objects/order-package.md)
* [notes](/objects/order-notes.md)

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

Dummy orders will be ignored in reports, and any delegations will NOT appear in the delegated company's processing queue.

An existing order cannot be updated to become a dummy order at a later time or vice versa.

## Example Requests

### Create

!> Requires the `orders_write` permission.

> If you want to create an entire order in one request, including plates, products and shipping, consider using the [BuildOrder](/helpers/build-order.md) helper endpoint. This may be better suited for applications with a customer-facing checkout facility.

<!-- tabs:start -->

#### **Body Parameters**

* **system_order_status_id** `integer|null` A [SystemOrderStatus](/objects/system-order-status.md) ID of either `1` (External Draft) or `2` (Internal Draft). It will change automatically in the future depending on the fulfilment state of its child packages.
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
  "system_order_status_id": 2,
  "system_order_fulfilment_status_id": 1,
  "amount_subtotal": 0,
  "amount_shipping": 0,
  "amount_vat": 0,
  "amount_total": 0,
  "amount_paid": 0,
  "amount_refunded": 0,
  "amount_vat_collected": 0,
  "amount_vat_refunded": 0,
  "packages_count": 0,
  "is_dummy": true,
  "opened_at": null,
  "created_at": "2025-02-26T16:09:50.000000Z",
  "updated_at": "2025-02-26T16:09:50.000000Z",
  "href": "/orders/100"
}
```

<!-- tabs:end -->

### Retrieve

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
  "system_order_status_id": 2,
  "system_order_fulfilment_status_id": 1,
  "amount_subtotal": 0,
  "amount_shipping": 0,
  "amount_vat": 0,
  "amount_total": 0,
  "amount_paid": 0,
  "amount_refunded": 0,
  "amount_vat_collected": 0,
  "amount_vat_refunded": 0,
  "packages_count": 0,
  "is_dummy": true,
  "opened_at": null,
  "created_at": "2025-02-26T16:09:50.000000Z",
  "updated_at": "2025-02-26T16:09:50.000000Z",
  "href": "/orders/100"
}
```

<!-- tabs:end -->

### List

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
      "system_order_status_id": 3,
      "system_order_fulfilment_status_id": 3,
      "amount_subtotal": 4777,
      "amount_shipping": 721,
      "amount_vat": 1104,
      "amount_total": 6602,
      "amount_paid": 6602,
      "amount_refunded": 0,
      "amount_vat_collected": 1104,
      "amount_vat_refunded": 0,
      "packages_count": 1,
      "is_dummy": true,
      "opened_at": "2025-03-25T15:11:53.000000Z",
      "created_at": "2025-03-25T14:36:37.000000Z",
      "updated_at": "2025-03-25T15:11:53.000000Z",
      "href": "/orders/1"
    },
    {
      "id": 100,
      "company_id": 1,
      "system_order_status_id": 2,
      "system_order_fulfilment_status_id": 1,
      "amount_subtotal": 0,
      "amount_shipping": 0,
      "amount_vat": 0,
      "amount_total": 0,
      "amount_paid": 0,
      "amount_refunded": 0,
      "amount_vat_collected": 0,
      "amount_vat_refunded": 0,
      "packages_count": 0,
      "is_dummy": false,
      "opened_at": null,
      "created_at": "2025-03-26T16:09:50.000000Z",
      "updated_at": "2025-03-26T16:09:50.000000Z",
      "href": "/orders/100"
    }
  ]
}
```

<!-- tabs:end -->

### Update

Once an order has been created, none of its properties can be updated manually.

### Delete

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