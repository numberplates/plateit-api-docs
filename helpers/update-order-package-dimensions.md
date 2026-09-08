# UpdateOrderPackageDimensions

`https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/dimensions`

Plateit automatically estimates the dimensions and weight of an [OrderPackage](/objects/order-package.md) based on its contents, including [OrderPackagePlate](/objects/order-package-plate.md) and [OrderPackageProduct](/objects/order-package-product.md) resources.

These values can be retrieved and, where necessary, manually overridden using this endpoint.

## Data References

### Attributes

* **width** `integer` The package width in mm.
* **height** `integer` The package height in mm.
* **depth** `integer` The package depth in mm.
* **weight** `integer` The package weight in grams.
* **has_overridden_dimensions** `boolean` Indicates whether the current dimensions or weight differ from the calculated values.
* **_calculated** `object` The dimensions and weight currently calculated by Plateit.

  * **width** `integer` The calculated package width in mm.
  * **height** `integer` The calculated package height in mm.
  * **depth** `integer` The calculated package depth in mm.
  * **weight** `integer` The calculated package weight in grams.
* **href** `string` The path to the resource.

> If no manual override has been applied, the outer values will match the `_calculated` values and `has_overridden_dimensions` will be `false`.
>
> The outer values are the values used for shipping. If they are changed manually, `_calculated` continues to show the current estimate and `has_overridden_dimensions` becomes `true`.

## Retrieve

!> Requires the `orders_packages_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}/dimensions`

Returns the package's current dimensions together with the estimated, calculated values.

### Example Response

```json
{
  "width": 520,
  "height": 114,
  "depth": 178,
  "weight": 1017,
  "has_overridden_dimensions": false,
  "href": "/v3/orders/1/packages/1/dimensions",
  "_calculated": {
    "width": 520,
    "height": 114,
    "depth": 178,
    "weight": 1017
  }
}
```

## Update

!> Requires the `orders_packages_write` permission.

**PATCH** `/v3/orders/{order_id}/packages/{package_id}/dimensions`

Any combination of the dimension fields may be supplied. Fields that are omitted retain their current values.

### Body Parameters

All fields are optional when updating this resource type.

* **width** `integer`
* **height** `integer`
* **depth** `integer`
* **weight** `integer`

### Example Payload

```json
{
  "weight": 1250
}
```

Returns the updated dimensions together with the current calculated values.

If the resulting outer values differ from `_calculated`, `has_overridden_dimensions` will be `true`.

> Setting the dimensions back to the calculated values removes the override and causes `has_overridden_dimensions` to return to `false`.
