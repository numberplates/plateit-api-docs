# UpdateOrderPackageDimensions

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/dimensions`

Plateit will estimate the dimensions of an [OrderPackage](/objects/order-package.md) based on its contents (the combined [OrderPackagePlate](/objects/order-package-plate.md) and [OrderPackageProduct](/objects/order-package-product.md) objects). These dimensions can be fetched and/or manually overridden using this helper endpoint.

!> This page is a stub. To be continued...

## Data References

### Attributes

* **width** `integer` The package width in mm.
* **height** `integer` The package height in mm.
* **depth** `integer` The package depth in mm.
* **weight** `integer` The package weight in grams.
* **has_overridden_dimensions** `boolean` Signfies whether the above values have manually overridden the automatic estimates.
* **_calculated** `object`
    * **width** `integer` The estimated package width in mm.
    * **height** `integer` The estimated package height in mm.
    * **depth** `integer` The estimated package depth in mm.
    * **weight** `integer` The estimated package weight in grams.

> If left untouched, the outer values will be identical to the inner `_calculated` values and the `has_overridden_dimensions` value will be `false`. *It is the outer values that are passed to the shipping provider*. If the outer values are updated manually, the inner `_calculated` values will stay the same but the `has_overridden_dimensions` value will be `true`.