# OrderPackage

`https://data.plateit.co.uk/v3/orders/{order_id}/packages`

A package belongs to an [Order](/objects/order.md), and an order can have many packages. If your company has one or more fulfilment agreements, a package can be assigned to another company to fulfil on your behalf.

>! If fulfilling for a delegating companies, there are important rules to follow. Click here to learn more.

## Data References

### Attributes

* **id** `integer` The unique ID of the package.
* **order_id** `integer` The ID of the [Order](/objects/order.md) the package belongs to.
* **delegate_to_company_id** `integer|null` The ID of the [company](/objects/company.md) the package has been delegated to, if applicable.
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

* [delegate_to_company](/objects/company.md)
* [system_package_status](/objects/system-package-status.md)
* [plates](/objects/order-package-plate.md)
* [products](/objects/order-package-product.md)
* [notes](/objects/order-package-note.md)
