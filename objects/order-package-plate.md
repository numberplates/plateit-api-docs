# OrderPackagePlate

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/plates`

An [OrderPackage](/objects/order-package.md) can have many plates.

!> This page is a stub. To be continued...

## Data References

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