# OrderPackageProduct

`https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/products`

An [OrderPackage](/objects/order-package.md) can have many products. Think of them as individual line items on an invoice.

Many of the product's physical and pricing attributes are copied from the selected [CompanyProduct](/objects/company-product.md) when the line item is created.

## Data References

### Attributes

* **id** `integer` The unique ID of the product line item.
* **package_id** `integer` The ID of the [OrderPackage](/objects/order-package.md) the product belongs to.
* **company_product_id** `integer` The ID of the selected [CompanyProduct](/objects/company-product.md).
* **company_product_id_delegated** `integer|null` The ID of the matching [CompanyProduct](/objects/company-product.md) belonging to the delegated fulfilment company, if applicable.
* **name** `string` The product name derived from the selected `CompanyProduct`.
* **sku** `string` The product SKU derived from the selected `CompanyProduct`.
* **width** `integer` The product width in mm.
* **height** `integer` The product height in mm.
* **depth** `integer` The product depth in mm.
* **weight** `integer` The product weight in grams.
* **price** `integer` The gross price in pence, including VAT.
* **price_vat** `integer` The included VAT amount in pence.
* **qty** `integer` The quantity of the product being sold.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [package](/objects/order-package.md)
* [company_product](/objects/company-product.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/{order_id}/packages/{package_id}/products/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## Create

!> Requires the `orders_packages_products_write` permission.

**POST** `/v3/orders/{order_id}/packages/{package_id}/products`

Creates a new product line item within the package.

### Body Parameters

* **company_product_id** `integer` The [CompanyProduct](/objects/company-product.md) to use.
* **price** `integer|null` Optional custom gross price in pence.
* **qty** `integer` The quantity being ordered.

### Example Payload

```json
{
  "company_product_id": 8,
  "qty": 2
}
```

Returns the created `OrderPackageProduct` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}/products/{product_id}`

Returns the requested `OrderPackageProduct`.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}/products`

Returns a collection of `OrderPackageProduct` resources belonging to the specified package.

## Update

!> Requires the `orders_packages_products_write` permission.

**PATCH** `/v3/orders/{order_id}/packages/{package_id}/products/{product_id}`

### Body Parameters

All fields are optional:

* **company_product_id** `integer`
* **price** `integer|null`
* **qty** `integer`

### Example Payload

```json
{
  "qty": 3
}
```

Returns the updated `OrderPackageProduct`.

## Delete

!> Requires the `orders_packages_products_write` permission.

**DELETE** `/v3/orders/{order_id}/packages/{package_id}/products/{product_id}`

Deletes the specified `OrderPackageProduct`.
