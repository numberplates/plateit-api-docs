# OrderPackagePlate

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/plates`

An [OrderPackage](/objects/order-package.md) can have many plates. Think of them as individual line items on an invoice.

!> This page is a stub. To be continued...

## Data References

### Attributes

* **id** `integer` The unique ID of the line item.
* **package_id** `integer` The [OrderPackage](/objects/order-package-plate.md) ID the item belongs to.
* **company_plate_id** `integer` The [CompanyPlate](/objects/company-plate.md) ID.
* **company_plate_id_delegated** `null|integer` The [CompanyPlate](/objects/company-plate.md) ID with matching attributes belonging to the delegated company, if applicable.
* **registration** `string` The vehicle registration string.
* **type** `string` The plate type name, derived from the [CompanyPlate](/objects/company-plate.md).
* **colour** `string` The plate colour, derived from the [CompanyPlate](/objects/company-plate.md).
* **width** `integer` The plate width, derived from the [CompanyPlate](/objects/company-plate.md).
* **height** `integer` The plate height, derived from the [CompanyPlate](/objects/company-plate.md).
* **depth** `integer` The plate depth, derived from the [CompanyPlate](/objects/company-plate.md).
* **weight** `integer` The plate weight, derived from the [CompanyPlate](/objects/company-plate.md).
* **price** `integer` The price in pence minus VAT.
* **price_vat** `integer` The VAT in pence.
* **price_gross** `integer` The total price in pence including VAT.
* **qty** `integer` The quantity being sold.
* **is_printable** `boolean` Indicates whether the plate should be printed (false for certain pressed plates).
* **is_printed** `boolean` Indicates whether the plate has been printed.
* **custom_instructions** `null|string` Bespoke design instructions left by the customer.
* **design_preview** `string` Path to SVG preview file (or SVG string if creating/updating)
* **design_print** `string` Path to SVG print file (or SVG string if creating/updating)
* **design_object** `null|object` Optional design object allows for future design edits. [Click here](/fundamentals/editing-existing-plate-designs.md) for more info.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [company_plate](/objects/company-plate.md)
* [company_plate.system_plate_size](/objects/system-plate-size.md)
* [company_plate.company_plate_type](/objects/company-plate-type.md)
* [package](/objects/order-package.md)
* [package.order](/objects/order.md)
* [package.system_package_status](/objects/system-package-status.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* registration
* package_id
* width
* height
* colour
* type
* price
* qty
* is_printable
* is_printed
* created_at
* updated_at
* package.order_id
* package.is_committed
* package.order.is_dummy
* package.system_package_status.id
* package.system_package_status.name

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* package_id
* type
* width
* height
* colour
* is_printed
* is_printable
* package.order_id
* package.is_committed
* package.order.is_dummy
* package.system_package_status.id
* package.system_package_status.name

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

### Available Search Bys

* registration

*Learn more about searching results [here](fundamentals/conventions.md#searching).*