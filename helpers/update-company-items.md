# UpdateCompanyItems (Bulk)

`https://api.plateit.co.uk/v3/actions/update-company-items`

This helper endpoint can be used to batch update supported company items that have a monetary value, including [CompanyPlate](/objects/company-plate.md), [CompanyProduct](/objects/company-product.md) and [CompanyShippingOption](/objects/company-shipping-option.md).

## Data References

### Request Attributes

* **item_type** `string` The type of company item being updated. Must be one of `company_plate`, `company_product` or `company_shipping_option`.
* **items** `array` An array of objects.
  * **id** `integer` The ID of the company item to update.
  * **price** `integer|null` The price value in pence.
  * **price_type** `string|null` Determines how the supplied `price` should be applied. Supported values are `set`, `increase` and `decrease`. Defaults to `set`.
  * **is_active** `boolean|null` Whether the company item should be active.

> Each item can be updated independently. For example, one item can have its price increased while another is decreased in the same request.

When `price_type` is:

* `set` - the supplied value becomes the new price.
* `increase` - the supplied value is added to the current price.
* `decrease` - the supplied value is deducted from the current price.

> If a price decrease would result in a value below zero, the resulting price will be set to `0`.

### Response Attributes

The response body contains data pertaining to the results of the request:

* **items** `array` An array of objects.
  * **id** `integer` The ID of the company item that may or may not have updated.
  * **price** `integer` The price after the request was made.
  * **previous_price** `integer` The price before the request was made.
  * **is_active** `boolean` Whether the item is active after the request was made.
  * **previous_is_active** `boolean` Whether the item was active before the request was made.
  * **has_item_updated** `boolean` This will be `true` if either the price or active state changed.

## Example Requests

### Update

!> Requires one of the following permissions depending on the item type being updated: `company_plates_write`, `company_products_write`, or `company_shipping_options_write`.

<!-- tabs:start -->

#### **Body Parameters**

* **item_type** `string`
* **items** `array`
  * **id** `integer`
  * **price** `integer|null`
  * **price_type** `string|null` (defaults to `set`)
  * **is_active** `boolean|null`

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/actions/update-company-items`
* Method: `POST`

```json
{
  "item_type": "company_plate",
  "items": [
    {
      "id": 12880,
      "price": 400,
      "is_active": false
    },
    {
      "id": 12881,
      "price": 400,
      "price_type": "increase"
    },
    {
      "id": 12882,
      "price": 200,
      "price_type": "decrease",
      "is_active": true
    }
  ]
}
```

#### **Response**

* Status code: `200`

```json
{
  "item_type": "company_plate",
  "items": [
    {
      "id": 12880,
      "price": 400,
      "previous_price": 500,
      "is_active": false,
      "previous_is_active": true,
      "has_item_updated": true
    },
    {
      "id": 12881,
      "price": 1400,
      "previous_price": 1000,
      "is_active": true,
      "previous_is_active": true,
      "has_item_updated": true
    },
    {
      "id": 12882,
      "price": 800,
      "previous_price": 1000,
      "is_active": true,
      "previous_is_active": true,
      "has_item_updated": true
    }
  ]
}
```

<!-- tabs:end -->
