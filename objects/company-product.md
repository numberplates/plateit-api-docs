# CompanyProduct

`https://api.plateit.co.uk/v3/products`

A `CompanyProduct` represents any product other than a number plate that a customer can purchase.

> A CompanyProduct can be delegated to another company to fulfil on your behalf. However, the delegated company must have a CompanyProduct with an *identical* SKU for the relationship to be recognised. The dimensions and weight used for fulfilment will be inherited from the delegatee's product settings rather than your own.
>
> Delegated products should only be shown to the customer if the delegated company has an active CompanyProduct with a matching SKU. This can be ensured by passing the `exclude_unmatched_delegations=true` query parameter when listing products. See the [suggested integration](/fundamentals/suggested-integration.md) guide for an example.

## Data References

### Attributes

* **id** `integer` The unique ID of the product.
* **name** `string` The name or title of the product.
* **sku** `string` The unique stock keeping unit code.
* **description** `string` A brief product description.
* **price** `integer` The price in pence including [VAT](/objects/company-tax-rate.md).
* **width** `integer` The width in mm, used for shipping calculations.
* **height** `integer` The height in mm, used for shipping calculations.
* **depth** `integer` The depth in mm, used for shipping calculations.
* **weight** `integer` The weight in g, used for shipping calculations.
* **is_active** `boolean` Indicates whether the product is currently active.
* **delegate_to_company_id** `integer|null` The ID of the [Company](/objects/company.md) delegated to fulfil the product, if applicable.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [delegate_to_company](/objects/company.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/products/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

> Plateit does not automatically exclude inactive resources. API consumers are responsible for deciding which resources should be shown publicly.

## Create

!> Requires the `company_products_write` permission.

**POST** `/v3/products`

### Body Parameters

* **name** `string`
* **sku** `string`
* **description** `string`
* **price** `integer`
* **width** `integer`
* **height** `integer`
* **depth** `integer`
* **weight** `integer`
* **is_active** `boolean`
* **delegate_to_company_id** `integer|null` Optional [Company](/objects/company.md) ID. The company must have an existing fulfilment relationship.

### Example Payload

```json
{
  "name": "Dual Port USB Charger",
  "sku": "DUALUSBCHARGER",
  "description": "A compact USB charger with two USB-C ports for charging multiple devices at once.",
  "price": 999,
  "width": 60,
  "height": 30,
  "depth": 15,
  "weight": 50,
  "is_active": true
}
```

Returns the created `CompanyProduct` with status `201`.

## Retrieve

!> Requires the `company_products_read` permission.

**GET** `/v3/products/{product_id}`

Returns the requested `CompanyProduct`.

## List

!> Requires the `company_products_read` permission.

**GET** `/v3/products`

Returns a paginated collection of `CompanyProduct` resources.

## Update

!> Requires the `company_products_write` permission.

**PATCH** `/v3/products/{product_id}`

### Body Parameters

All fields are optional:

* **name** `string`
* **sku** `string`
* **description** `string`
* **price** `integer`
* **width** `integer`
* **height** `integer`
* **depth** `integer`
* **weight** `integer`
* **is_active** `boolean`
* **delegate_to_company_id** `integer|null`

### Example Payload

```json
{
  "price": 1299
}
```

Returns the updated `CompanyProduct`.

## Delete

!> Requires the `company_products_write` permission.

**DELETE** `/v3/products/{product_id}`

Deletes the specified `CompanyProduct`.
