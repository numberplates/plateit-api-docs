# OrderPackageShipToOverride

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/ship-to-override`

> This is a singleton resource.

By default all [OrderPackage](/objects/order-package.md) objects inherit the [OrderShipTo](/objects/order-ship-to.md) address of their parent orders. This can optionally be overridden at the package level.

!> This page is a stub. However, the handling is almost idential to the [OrderShipTo](/objects/order-ship-to.md) documentation.

## Data References

### Attributes

* **package_id** `integer` The [OrderPackage](/objects/order-package.md) ID the resource belongs to.
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

* [package](/objects/package.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*