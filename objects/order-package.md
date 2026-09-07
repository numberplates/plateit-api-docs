# OrderPackage

`https://api.plateit.co.uk/v3/orders/{order_id}/packages`

An `OrderPackage` belongs to an [Order](/objects/order.md), and an order can contain multiple packages. A package groups together plates, products and shipping for fulfilment.

If your company has an active fulfilment agreement, an `OrderPackage` can also be delegated to another company to fulfil on your behalf.

!> Delegated packages are subject to specific matching and fulfilment rules. See the [delegation guide](/fundamentals/delegations.md) for more information.

> Packages belonging to a specific order can be retrieved from this endpoint. To retrieve packages across all orders, use `GET /v3/packages`.

## Data References

### Attributes

Many `OrderPackage` attributes are calculated automatically or managed through dedicated endpoints.

* **id** `integer` The unique ID of the package.
* **order_id** `integer` The ID of the [Order](/objects/order.md) the package belongs to.
* **delegate_to_company_id** `integer|null` The ID of the [Company](/objects/company.md) delegated to fulfil the package, if applicable.
* **system_package_status_id** `integer` The [SystemPackageStatus](/objects/system-package-status.md) ID.
* **amount_subtotal** `integer` The sum of all package items in pence, excluding shipping and VAT.
* **amount_shipping** `integer` The total package shipping cost in pence.
* **amount_vat** `integer` The total package VAT in pence.
* **amount_total** `integer` The package's grand total in pence.
* **plates_qty** `integer` The total quantity of number plates in the package.
* **products_qty** `integer` The total quantity of additional products in the package.
* **width** `integer` The package width in mm.
* **height** `integer` The package height in mm.
* **depth** `integer` The package depth in mm.
* **weight** `integer` The package weight in g.
* **has_overridden_dimensions** `boolean` Indicates whether the package dimensions or weight have been manually overridden. See [UpdateOrderPackageDimensions](/helpers/update-order-package-dimensions.md).
* **is_replacement** `boolean` Indicates whether the package was duplicated for replacement purposes.
* **is_committed** `boolean` Indicates whether the package has been committed and is ready for fulfilment.
* **is_shipping_synced** `boolean` Indicates whether the package has been synchronised with its shipping provider.
* **is_paperwork_printed** `boolean` Indicates whether the package's shipping paperwork has been printed.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [system_package_status](/objects/system-package-status.md)
* [delegate_to_company](/objects/company.md)
* [plates](/objects/order-package-plate.md)
* [products](/objects/order-package-product.md)
* [shipping](/objects/order-package-shipping.md)
* [shipping.system_courier_service](/objects/system-courier-service.md)
* [notes](/objects/order-package-note.md)
* [ship_to_override](/objects/order-package-ship-to-override.md)
* [order](/objects/order.md)
* [order.company](/objects/company.md)
* [order.system_order_status](/objects/system-order-status.md)
* [order.customer](/objects/order-customer.md)
* [order.ship_to](/objects/order-ship-to.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/{order_id}/packages/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## Create

!> Requires the `orders_packages_write` permission.

**POST** `/v3/orders/{order_id}/packages`

### Body Parameters

* **delegate_to_company_id** `integer|null`
* **system_package_status_id** `integer` Optional. Defaults to `1` (`Unprocessed`).
* **is_committed** `boolean` Optional. Defaults to `false`.

### Example Payload

```json
{
  "delegate_to_company_id": 2
}
```

Returns the created `OrderPackage` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}`

Returns the requested `OrderPackage`.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/packages`

Returns a collection of `OrderPackage` resources belonging to the specified order.

To retrieve packages across all orders:

**GET** `/v3/packages`

## Update

!> Requires the `orders_packages_write` permission.

**PATCH** `/v3/orders/{order_id}/packages/{package_id}`

Only attributes intended for direct package management can be updated through this endpoint. Calculated values and attributes managed by dedicated endpoints cannot be changed directly.

### Example Payload

```json
{
  "is_committed": true
}
```

Returns the updated `OrderPackage`.

> Committing a package marks it as ready for fulfilment. A package cannot be committed until its required order, shipping, contents and supporting-document requirements have been satisfied.

## Delete

!> Requires the `orders_packages_write` permission.

**DELETE** `/v3/orders/{order_id}/packages/{package_id}`

Deletes the specified `OrderPackage`.

A committed package cannot be deleted.
