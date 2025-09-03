# OrderPackageProduct

`https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/products`

An [OrderPackage](/objects/order-package.md) can have many products. Think of them as individual line items on an invoice.

!> This page is a stub. To be continued...

## Data References

### Attributes

* **id** `integer` The unique ID of the line item.
* **package_id** `integer` The [OrderPackage](/objects/order-package-plate.md) ID the item belongs to.
* **company_product_id** `integer` The [CompanyProduct](/objects/company-product.md) ID.
* **company_product_id_delegated** `null|integer` The [CompanyProduct](/objects/company-product.md) ID with a
matching SKU belonging to the delegated company, if applicable.
* **name** `string` The product name, derived from the [CompanyProduct](/objects/company-product.md).
* **sku** `string` The product SKU, derived from the [CompanyProduct](/objects/company-product.md).
* **width** `integer` The product width, derived from the [CompanyProduct](/objects/company-product.md).
* **height** `integer` The product height, derived from the [CompanyProduct](/objects/company-product.md).
* **depth** `integer` The product depth, derived from the [CompanyProduct](/objects/company-product.md).
* **weight** `integer` The product weight, derived from the [CompanyProduct](/objects/company-product.md).
* **price** `integer` The price in pence minus VAT.
* **price_vat** `integer` The VAT in pence.
* **price_gross** `integer` The total price in pence including VAT.
* **qty** `integer` The quantity being sold.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [package](/objects/order-package.md)
* [company_product](/objects/company-product.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* name
* price
* qty
* created_at
* updated_at

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*