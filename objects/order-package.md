# OrderPackage

`https://data.plateit.co.uk/v3/orders/{order_id}/packages`

An OrderPackage belongs to an [Order](/objects/order.md), and an order can have many packages. If your company has one or more fulfilment agreements, an OrderPackage can be assigned to another company to fulfil on your behalf.

!> If delegating a package to another company to fulfil, there are important rules to follow. See the [delegation guide](/fundamentals/delegations.md) for more information.

## Data References

### Attributes

> Please read carefully because many OrderPackage attributes are updated *exclusively* using dedicated helper endpoints.

* **id** `integer` The unique ID of the package.
* **order_id** `integer` The ID of the [Order](/objects/order.md) the package belongs to.
* **delegate_to_company_id** `integer|null` The ID of the [Company](/objects/company.md) the package has been delegated to, if applicable.
* **system_package_status_id** `integer` The ID of the [SystemPackageStatus](/objects/system-package-status.md).
* **plates_qty** `integer` The quantity of number plates in the package.
* **products_qty** `integer` The quantity of extra products in the package.
* **width** `integer` The width of the package in mm.
* **height** `integer` The height of the package in mm.
* **depth** `integer` The depth of the package in mm.
* **weight** `integer` The weight of the package in g.
* **has_overridden_dimensions** `boolean` This will be true if the dimensions listed above have been manually set. *This is updated exclusively using the [UpdateOrderPackageDimensions](/helpers/update-order-package-dimensions.md) helper endpoint.*
* **is_committed** `boolean` The package has been marked as ready to fulfil if true.
* **is_shipping_synced** `boolean` The package contents have been synced with the shipping provider if true. *This is updated exclusively using the [CreateOrderPackageShipmentLabel](/helpers/create-order-package-shipment-label.md) helper endpoint.*
* **is_paperwork_printed** `boolean` The package's label/s have been printed if true. *This is updated exclusively using the [MarkPaperworkPrinted](/helpers/mark-paperwork-printed.md) helper endpoint.*
* **is_despatched** `boolean` The package has been despatched if true. *This is updated exclusively using the [UpdatePackageDespatchStatuses](/helpers/update-package-despatch-statuses.md) helper endpoint.*
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [system_package_status](/objects/system-package-status.md)
* [delegate_to_company](/objects/company.md)
* [plates](/objects/order-package-plate.md)
* [products](/objects/order-package-product.md)
* [shipping](/objects/order-package-shipping.md)
* [notes](/objects/order-package-note.md)
* [ship_to_override](/objects/order-package-ship-to-override.md)
* [order](/objects/order.md)
* [order.company](/objects/company.md)
* [order.system_order_status](/objects/system-order-status.md)
* [order.customer](/objects/order-customer.md)
* [order.ship_to](/objects/order-ship-to.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* is_committed
* is_shipping_synced
* is_despatched
* created_at
* updated_at
* order.id
* order.is_dummy
* order.opened_at
* order.company.id
* order.company.name
* order.system_order_status.id
* order.system_order_status.name
* system_package_status.id
* system_package_status.name
* shipping.name

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_committed
* is_shipping_synced
* is_despatched
* order.id
* order.is_dummy
* order.company.id
* order.company.name
* order.system_order_status.id
* order.system_order_status.name
* system_package_status.id
* system_package_status.name
* shipping.name

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

### Available Search Bys

* id
* order.customer.first_name
* order.customer.last_name
* order.customer.email

*Learn more about searching results [here](fundamentals/conventions.md#searching).*

> Note: *all* OrderPackages (not just the ones pertaining to a single order) can be retrieved at `https://data.plateit.co.uk/v3/packages`.

## Example Requests

### Create

!> Requires the `orders_packages_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **delegate_to_company_id** `integer|null`
* **system_package_status_id** `integer|null` (defaults to `1` - `External Draft`)
* **is_committed** `boolean|null` (defaults to `false`)

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages`
* Method: `POST`

```json
{
  "system_package_status_id": 2
}
```

#### **Response**

* Status code: `201`

```json
{
  "id": 4972,
  "order_id": 4006,
  "delegate_to_company_id": null,
  "system_package_status_id": 2,
  "plates_qty": 0,
  "products_qty": 0,
  "width": 0,
  "height": 0,
  "depth": 0,
  "weight": 0,
  "has_overridden_dimensions": false,
  "is_committed": false,
  "is_shipping_synced": false,
  "is_paperwork_printed": false,
  "is_despatched": false,
  "created_at": "2025-04-04T09:29:08.000000Z",
  "updated_at": "2025-04-04T09:29:08.000000Z",
  "href": "/orders/4006/packages/4972"
}
```

<!-- tabs:end -->

### Retrieve

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 4972,
  "order_id": 4006,
  "delegate_to_company_id": null,
  "system_package_status_id": 2,
  "plates_qty": 0,
  "products_qty": 0,
  "width": 0,
  "height": 0,
  "depth": 0,
  "weight": 0,
  "has_overridden_dimensions": false,
  "is_committed": false,
  "is_shipping_synced": false,
  "is_paperwork_printed": false,
  "is_despatched": false,
  "created_at": "2025-04-04T09:29:08.000000Z",
  "updated_at": "2025-04-04T09:29:08.000000Z",
  "href": "/orders/4006/packages/4972"
}
```

<!-- tabs:end -->

### List

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages`
* Method: `GET`

> Note: This will list all packages belonging to a specified order. To list all packages regardless of their parent orders, you can use the  `/packages` endpoint.

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 4971,
      "order_id": 4006,
      "delegate_to_company_id": null,
      "system_package_status_id": 5,
      "plates_qty": 2,
      "products_qty": 1,
      "width": 530,
      "height": 120,
      "depth": 10,
      "weight": 250,
      "has_overridden_dimensions": false,
      "is_committed": true,
      "is_shipping_synced": true,
      "is_paperwork_printed": true,
      "is_despatched": false,
      "created_at": "2025-04-04T09:20:01.000000Z",
      "updated_at": "2025-04-04T09:20:01.000000Z",
      "href": "/orders/4006/packages/4971"
    }
    {
      "id": 4972,
      "order_id": 4006,
      "delegate_to_company_id": null,
      "system_package_status_id": 1,
      "plates_qty": 0,
      "products_qty": 0,
      "width": 0,
      "height": 0,
      "depth": 0,
      "weight": 0,
      "has_overridden_dimensions": false,
      "is_committed": false,
      "is_shipping_synced": false,
      "is_paperwork_printed": false,
      "is_despatched": false,
      "created_at": "2025-04-04T09:29:08.000000Z",
      "updated_at": "2025-04-04T09:29:08.000000Z",
      "href": "/orders/4006/packages/4972"
    }
  ]
}
```

<!-- tabs:end -->

### Update

!> Requires the `orders_packages_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **system_package_status_id** `int`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}`
* Method: `PATCH`

```json
{
  "system_package_status_id": 3
}
```

#### **Response**

* Status code: `200`

```json
{
  "id": 4972,
  "order_id": 4006,
  "delegate_to_company_id": null,
  "system_package_status_id": 3,
  "plates_qty": 0,
  "products_qty": 0,
  "width": 0,
  "height": 0,
  "depth": 0,
  "weight": 0,
  "has_overridden_dimensions": false,
  "is_committed": false,
  "is_shipping_synced": false,
  "is_paperwork_printed": false,
  "is_despatched": false,
  "created_at": "2025-04-04T09:29:08.000000Z",
  "updated_at": "2025-04-04T09:31:45.000000Z",
  "href": "/orders/4006/packages/4972"
}
```

<!-- tabs:end -->

### Delete

!> Requires the `orders_packages_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->