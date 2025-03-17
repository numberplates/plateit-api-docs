# Build Order

`https://data.plateit.co.uk/v3/actions/build-order`

This endpoint is used to build an entire order, including its contents (plates, products, customer details and a shipping option) **in a single request**. It is designed to be used at a customer-facing checkout.

> The request outlined on this page will create a new, `External Draft` order. It will not become an active, `Open` order until payment has been recieved. See the [suggested integration](/fundamentals/suggested-integration.md) instructions for more details.

## Data References

### Attributes

* **plates** `array` An array of objects.
    * **company_plate_id** `integer` The ID of the [CompanyPlate](/objects/company-plate.md) being purchased.
    * **registration** `string` The registration, including any spaces (used for record keeping).
    * **price_gross** `integer` The price in pence it is being sold for including [VAT](/objects/company-tax-rate.md).
    * **qty** `integer` The quantity.
    * **design_print** `string` The final [print file](/fundamentals/plate-files.md) in SVG format.
    * **design_preview** `string` The [preview file](/fundamentals/plate-files.md) in SVG format if different from the print file (optional).
    * **design_object** `object` An object representation of the plate if you want to be able to bring the design back into an editor at a later date (optional).
    * **custom_instructions** `string` Custom design instructions (optional).
* **products** `array` An array of objects.
    * **company_product_id** `integer` The ID of the [CompanyProduct](/objects/company-product.md) being purchased.
    * **price_gross** `integer` The price in pence it is being sold for including [VAT](/objects/company-tax-rate.md).
    * **qty** `integer` The quantity.
* **shipping** `object`
    * **company_shipping_id** `integer` The ID of the [CompanyShippingOption](/objects/company-shipping.md) being purchased.
    * **price_gross** `integer` The price in pence it is being sold for including [VAT](/objects/company-tax-rate.md).
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
    * **address_country_code** `string` The two-character ISO country code, such as "GB".
* **bill_to** `object` (if different from the ship_to address - optional)
    * **first_name** `string` The payer's first name.
    * **last_name** `string` The payer's last name.
    * **address_line_1** `string` The first line of the address.
    * **address_line_2** `string` The second line of the address (optional).
    * **address_line_3** `string` The city.
    * **address_postcode** `string` The postcode.
    * **address_country_code** `string` The two-character ISO country code, such as "GB".

## Setting Prices

The item prices defined in the body of the request *need to be identical to the prices saved in Plateit*. If the prices do not match, it will return a validation error response.

This default behaviour can be overridden if you want to manually set a custom price instead. To do this append the following query string to the endpoint url:

`?bypass_price_checks=1`

!> To prevent price manipulation, always make the request from the server side, incorporating logic that safeguards against client-side tampering!

## Delegations

If any products are delegated to be fulfilled by other companies, the necessary delegated packages will be created automatically. If the delegated company uses a different shipping provider or doesn't have the same service available, the closest match will be found and applied.

More information about how this enpoint handles delegations can be found on [this page](/delegations/method-02.md).

## Example Request

!> Requires the `orders_build` permission.

> For testing purposes, pass the `?is_dummy=1` query parameter. This will create a test (dummy) order which will be omitted from your sales reports and won't be fulfilled by delegatees (if applicable).

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/actions/build-order`
* Method: `POST`
* Query:
  * is_dummy: `true`

```json
{
  "plates": [
    {
      "company_plate_id": 9602,
      "registration": "NG25 TTX",
      "price_gross": 1500,
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
      },
    },
    {
      "company_plate_id": 9603,
      "registration": "NG25 TTX",
      "price_gross": 1500,
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
      },
    }
  ],
  "products": [
    {
      "company_product_id": 2341,
      "price_gross": 299,
      "qty": 1
    }
  ],
  "shipping": {
    "company_shipping_id": 1189,
    "price_gross": 583,
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

The returned order ID should then be passed to the payment provider. See the [suggested integration](/fundamentals/suggested-integration.md) instructions for more details.