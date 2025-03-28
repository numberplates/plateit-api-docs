# OrderPackage

`https://data.plateit.co.uk/v3/orders/{order_id}/packages`

An OrderPackage belongs to an [Order](/objects/order.md), and an order can have many packages. If your company has one or more fulfilment agreements, an OrderPackage can be assigned to another company to fulfil on your behalf.

!> If delegating a package to another company to fulfil, there are important rules to follow. See the [delegation guide](/fundamentals/delegations.md) for more information.

!> This page is a stub. To be continued...

## Data References

### Attributes

* **id** `integer` The unique ID of the package.
* **order_id** `integer` The ID of the [Order](/objects/order.md) the package belongs to.
* **delegate_to_company_id** `integer|null` The ID of the [Company](/objects/company.md) the package has been delegated to, if applicable.
* **system_package_status_id** `integer` The ID of the [SystemPackageStatus](/objects/system-package-status.md).
* **plates_qty** `integer` The quantity of number plates in the package.
* **products_qty** `integer` The quantity of extra products in the package.
* **width** `integer` The estimated width of the package in mm.
* **height** `integer` The estimated height of the package in mm.
* **depth** `integer` The estimated depth of the package in mm.
* **weight** `integer` The estimated weight of the package in g.
* **has_overridden_dimensions** `boolean` This will be true if the estimated dimensions above have been manually overridden.
* **is_committed** `boolean` The package has been marked as ready to fulfil.
* **is_shipping_synced** `boolean` The package contents have been synced with the shipping provider.
* **is_paperwork_printed** `boolean` The package's label/s have been printed.
* **is_despatched** `boolean` The package has been despatched.
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

> Note: all packages (not just the ones pertaining to an order) can be retrieved at `https://data.plateit.co.uk/v3/packages`.