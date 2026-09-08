# BuildOrder

`https://api.plateit.co.uk/v3/actions/build-order`

This helper endpoint is used to build an entire [Order](/objects/order.md), including its nested contents **in a single request**. It is designed to be used at a customer-facing checkout.

> The request outlined on this page creates a new `External Draft` order. Once paid in full, the order will become `Open` when any supporting-document requirements have also been satisfied. See the [suggested integration](/fundamentals/suggested-integration.md) and [supporting documents](/fundamentals/documents.md) guides for more details.

## Data References

### Attributes

* **plates** `array` An array of objects.
  * **company_plate_id** `integer` The ID of the [CompanyPlate](/objects/company-plate.md) being purchased.
  * **registration** `string` The registration or plate text.
  * **requires_docs** `boolean` Whether the plate requires supporting identity and entitlement documents. Defaults to `true`. When `true`, `registration` must be a valid road registration. See [Supporting Documents](/fundamentals/documents.md).
  * **price** `integer` The gross price in pence.
  * **qty** `integer` The quantity.
  * **design_print** `string` The final [print file](/fundamentals/plate-files.md) in SVG format.
  * **design_preview** `string` The [preview file](/fundamentals/plate-files.md) in SVG format if different from the print file (optional).
  * **design_object** `object` An object representation of the plate if you want to be able to bring the design back into an editor at a later date (optional).
  * **custom_instructions** `string` Custom design instructions (optional).
* **products** `array` An array of objects.
  * **company_product_id** `integer` The ID of the [CompanyProduct](/objects/company-product.md) being purchased.
  * **price** `integer` The gross price in pence.
  * **qty** `integer` The quantity.
* **shipping** `object`
  * **company_shipping_id** `integer` The ID of the [CompanyShippingOption](/objects/company-shipping-option.md) being purchased.
  * **price** `integer` The gross price in pence.
  * **delivery_instructions** `string` Delivery instructions if the courier supports this (optional).
* **customer** `object`
  * **first_name** `string` The customer's first name.
  * **last_name** `string` The customer's last name.
  * **email** `string` The customer's email address.
  * **mobile_number** `string` The customer's mobile number (required for some couriers) (optional).
  * **phone_number** `string` The customer's phone number (optional).
* **ship_to** `object`
  * **first_name** `string` The recipient's first name.
  * **last_name** `string` The recipient's last name.
  * **address_line_1** `string` The first line of the address.
  * **address_line_2** `string` The second line of the address (optional).
  * **address_line_3** `string` The city.
  * **address_postcode** `string` The postcode.
  * **address_country_code** `string` The two-character ISO country code, such as `GB`.
* **bill_to** `object` Optional billing address if different from `ship_to`.
  * **first_name** `string` The payer's first name.
  * **last_name** `string` The payer's last name.
  * **address_line_1** `string` The first line of the address.
  * **address_line_2** `string` The second line of the address (optional).
  * **address_line_3** `string` The city.
  * **address_postcode** `string` The postcode.
  * **address_country_code** `string` The two-character ISO country code, such as `GB`.

## Delegations

If any items are delegated to be fulfilled by other companies, the necessary delegated [OrderPackage](/objects/order-package.md) objects will be created automatically.

If the delegated company uses a different shipping provider or does not have the same service available, the closest match will be found and applied.

More information about how this endpoint handles delegations can be found in the [delegation guide](/fundamentals/delegations.md).

### Bypassing Draft Status

By default, a successful request creates a new `External Draft` order.

For integrations where payment is handled outside Plateit, this behaviour can be overridden by appending:

`?bypass_draft=1`

This causes the order to be created directly in an `Open` state and its packages to be committed for fulfilment.

!> `bypass_draft` can only be used when the order does not require supporting documents. All plate line items must therefore have `requires_docs` set to `false`.

!> To prevent abuse, always make this request from the server side and ensure client-side input cannot be used to bypass your payment or order-validation logic.

### Prices

The `price` values supplied in the request are gross prices in pence, including VAT.

By default, the prices supplied for plates, products and shipping must match the corresponding prices saved in Plateit. If a price does not match, the request will fail validation.

This behaviour can be overridden when custom pricing is required by appending:

`?bypass_price_checks=1`

!> To prevent price manipulation, always make this request from the server side and ensure client-side values cannot be trusted to determine the final price.

## Example Request

!> Requires the `orders_build` permission.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/actions/build-order`
* Method: `POST`

```json
{
  "plates": [
    {
      "company_plate_id": 9602,
      "registration": "NG25 TTX",
      "requires_docs": true,
      "price": 1500,
      "qty": 1,
      "design_print": "<svg viewBox=\"0 0 520 111\"><!-- front plate --></svg>",
      "design_object": {
        "reg": {
          "text": "NG25 TTX",
          "textFontUrl": "../assets/fonts/CharlesWright-Car.ttf",
          "textHeight": 79,
          "textLineGap": 19,
          "textColour": "black"
        },
        "etc": "etc..."
      }
    },
    {
      "company_plate_id": 9603,
      "registration": "NG25 TTX",
      "requires_docs": true,
      "price": 1500,
      "qty": 1,
      "design_print": "<svg viewBox=\"0 0 520 111\"><!-- rear plate --></svg>",
      "design_object": {
        "reg": {
          "text": "NG25 TTX",
          "textFontUrl": "../assets/fonts/CharlesWright-Car.ttf",
          "textHeight": 79,
          "textLineGap": 19,
          "textColour": "black"
        },
        "etc": "etc..."
      }
    }
  ],
  "products": [
    {
      "company_product_id": 2341,
      "price": 299,
      "qty": 1
    }
  ],
  "shipping": {
    "company_shipping_id": 1189,
    "price": 583,
    "delivery_instructions": "Leave in front porch."
  },
  "customer": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "mobile_number": "07777777777"
  },
  "ship_to": {
    "first_name": "John",
    "last_name": "Doe",
    "address_line_1": "123 Something Street",
    "address_line_2": "Somewhere",
    "address_line_3": "Derby",
    "address_postcode": "DE6 1RT",
    "address_country_code": "GB"
  }
}
```

#### **Response**

* Status code: `201`

```json
{
  "id": 65743,
  "message": "Order successfully created."
}
```

<!-- tabs:end -->

Upon success, a new [Order](/objects/order.md) is created with an `External Draft` status and its order ID can be extracted from the response body.

> Plates that require supporting documentation will contribute to the order's document requirements. By default, plate line items require documents unless `requires_docs` is explicitly set to `false`.

If supporting documents are required, see the [Supporting Documents](/fundamentals/documents.md) guide.

The returned order ID should then be passed to the payment provider. See the [suggested integration](/fundamentals/suggested-integration.md) instructions for more details.
