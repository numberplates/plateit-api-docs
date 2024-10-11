# Company Product

`https://data.plateit.co.uk/v3/products`

The product object represents any product other than a number plate that the customer can buy.

> Products can be delegated to other companies to fulfil on your behalf. However, the delegated company must have a product with an *identical* SKU for this relationship to be recognised. The dimensions and weight will be inherited from their settings and not yours.

>Delegated products should only be shown to the customer if the delegated company has an active product with a matching SKU. This can be ensured by passing the `exclude_unmatched_delegations=true` query parameter when listing the available products. This will filter out any products the delegatee doesn't have. This can be seen in action on the [suggested integration](/fundamentals/suggested-integration.md) page.

## Data References

### Attributes

* **id** `integer` The unique ID of the product.
* **name** `string` The name or title or the product.
* **sku** `string` The unique stock keeping unit code.
* **description** `string` A brief product description.
* **price** `int` The price in pence.
* **width** `int` The width in mm (for shipping calculations).
* **height** `int` The height in mm (for shipping calculations).
* **depth** `int` The depth in mm (for shipping calculations).
* **weight** `int` The weight in g (for shipping calculations).
* **is_active** `boolean` Indicates whether the resource is live or a draft.
* **delegate_to_company_id** `integer|null` The [company](/objects/company.md) ID to delegate the product to fulfil.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [delegate_to_company](/objects/company.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* name
* sku
* weight
* width
* height
* depth
* price
* is_active
* created_at
* updated_at

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_active *

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

**Plateit does not filter out inactive resources for you. It is your responsibility to honour what is shown publicly and what's not.*

## Example Requests

### Create a Product

!> Requires the `company_products_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **name** `string`
* **sku** `string`
* **description** `string`
* **price** `int`
* **width** `int`
* **height** `int`
* **depth** `int`
* **weight** `int`
* **is_active** `boolean`
* **delegate_to_company_id** `integer|null` An optional [company](/objects/company.md) ID. (must have an existing fulfilment relationship contract)

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/products`
* Method: `POST`

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

#### **Response**

* Status code: `201`

```json
{
  "id": 15,
  "name": "Dual Port USB Charger",
  "sku": "DUALUSBCHARGER",
  "description": "A compact USB charger with two USB-C ports for charging multiple devices at once.",
  "price": 999,
  "width": 60,
  "height": 30,
  "depth": 15,
  "weight": 50,
  "is_active": true,
  "delegate_to_company_id": null,
  "created_at": "2024-09-30T10:21:30.000000Z",
  "updated_at": "2024-09-30T10:21:30.000000Z",
  "href": "/products/15"
}
```

<!-- tabs:end -->

### Retrieve a Product

!> Requires the `company_products_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/products/{product_id}`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 15,
  "name": "Dual Port USB Charger",
  "sku": "DUALUSBCHARGER",
  "description": "A compact USB charger with two USB-C ports for charging multiple devices at once.",
  "price": 999,
  "width": 60,
  "height": 30,
  "depth": 15,
  "weight": 50,
  "is_active": true,
  "delegate_to_company_id": null,
  "created_at": "2024-09-30T10:21:30.000000Z",
  "updated_at": "2024-09-30T10:21:30.000000Z",
  "href": "/products/15"
}
```

<!-- tabs:end -->

### List Products

!> Requires the `company_products_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/products`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 14,
      "name": "Car Fixing Kit",
      "sku": "CARFIXINGKIT",
      "description": "A selection of coloured screws and sticky pads for fixing two plates to a car or van.",
      "price": 299,
      "width": 50,
      "height": 50,
      "depth": 5,
      "weight": 15,
      "is_active": true,
      "delegate_to_company_id": null,
      "created_at": "2024-09-30T10:17:22.000000Z",
      "updated_at": "2024-09-30T10:17:22.000000Z",
      "href": "/products/14"
    },
    {
      "id": 15,
      "name": "Dual Port USB Charger",
      "sku": "DUALUSBCHARGER",
      "description": "A compact USB charger with two USB-C ports for charging multiple devices at once.",
      "price": 999,
      "width": 60,
      "height": 30,
      "depth": 15,
      "weight": 50,
      "is_active": true,
      "delegate_to_company_id": null,
      "created_at": "2024-09-30T10:21:30.000000Z",
      "updated_at": "2024-09-30T10:21:30.000000Z",
      "href": "/products/15"
    }
  ]
}
```

<!-- tabs:end -->

### Update a Product

!> Requires the `company_products_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **name** `string|null`
* **sku** `string|null`
* **description** `string|null`
* **price** `int|null`
* **width** `int|null`
* **height** `int|null`
* **depth** `int|null`
* **weight** `int|null`
* **is_active** `boolean|null`
* **delegate_to_company_id** `integer|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/products/{product_id}`
* Method: `PATCH`

```json
{
  "price": 1299
}
```

#### **Response**

* Status code: `200`

```json
{
  "id": 15,
  "name": "Dual Port USB Charger",
  "sku": "DUALUSBCHARGER",
  "description": "A compact USB charger with two USB-C ports for charging multiple devices at once.",
  "price": 1299,
  "width": 60,
  "height": 30,
  "depth": 15,
  "weight": 50,
  "is_active": true,
  "delegate_to_company_id": null,
  "created_at": "2024-09-30T10:21:30.000000Z",
  "updated_at": "2024-09-30T10:28:04.000000Z",
  "href": "/products/15"
}
```

<!-- tabs:end -->

### Delete a Product

!> Requires the `company_products_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/products/{product_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->