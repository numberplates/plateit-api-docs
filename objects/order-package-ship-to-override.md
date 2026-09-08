# OrderPackageShipToOverride

`https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/ship-to-override`

> This is a singleton resource.

By default, an [OrderPackage](/objects/order-package.md) inherits the [OrderShipTo](/objects/order-ship-to.md) address of its parent order. An `OrderPackageShipToOverride` can optionally be created to provide a different shipping address for an individual package.

## Data References

### Attributes

* **package_id** `integer` The ID of the [OrderPackage](/objects/order-package.md) the resource belongs to.
* **first_name** `string` The customer's first name.
* **last_name** `string` The customer's last name.
* **address_line_1** `string` The first line of the address.
* **address_line_2** `string|null` The second line of the address.
* **address_line_3** `string` The city or locality.
* **address_postcode** `string` The postcode.
* **address_country_code** `string` The two-character ISO country code, such as `GB`.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [package](/objects/order-package.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Create

!> Requires the `orders_packages_write` permission.

**POST** `/v3/orders/{order_id}/packages/{package_id}/ship-to-override`

### Body Parameters

* **first_name** `string`
* **last_name** `string`
* **address_line_1** `string`
* **address_line_2** `string|null`
* **address_line_3** `string`
* **address_postcode** `string`
* **address_country_code** `string`

### Example Payload

```json
{
  "first_name": "John",
  "last_name": "Turcotte",
  "address_line_1": "18 Market Street",
  "address_line_3": "Manchester",
  "address_postcode": "M1 1AA",
  "address_country_code": "GB"
}
```

Returns the created `OrderPackageShipToOverride` with status `201`.

## Retrieve

!> Requires the `orders_packages_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}/ship-to-override`

Returns the package's `OrderPackageShipToOverride`.

## Update

!> Requires the `orders_packages_write` permission.

**PATCH** `/v3/orders/{order_id}/packages/{package_id}/ship-to-override`

### Body Parameters

All fields are optional when updating this resource type.

* **first_name** `string`
* **last_name** `string`
* **address_line_1** `string`
* **address_line_2** `string|null`
* **address_line_3** `string`
* **address_postcode** `string`
* **address_country_code** `string`

### Example Payload

```jsonid="krcdsq"
{
  "address_postcode": "M1 2AB"
}
```

Returns the updated `OrderPackageShipToOverride`.

## Delete

!> Requires the `orders_packages_write` permission.

**DELETE** `/v3/orders/{order_id}/packages/{package_id}/ship-to-override`

Deletes the package's `OrderPackageShipToOverride`.
