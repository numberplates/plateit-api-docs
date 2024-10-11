# Place Order

`https://data.plateit.co.uk/v3/actions/place-order`

This endpoint is used to create an entire order including plates, products, customer details and a shipping option **in a single request**. It is designed to be used at a customer-facing checkout.

> The request outlined on this page will create a new, *pending* order. It will not become an active order until payment has been recieved. See the [suggested integration](/fundamentals/suggested-integration.md) instructions for more details.

## Data References

### Attributes

* **plates** `array` An array of objects.
    * **company_plate_id** `integer` The ID of the [Company Plate](/objects/company-plate.md) being purchased.
    * **registration** `string` The registration, including any spaces (used for record keeping).
    * **price** `integer` The price in pence it is being sold for.
    * **qty** `integer` The quantity.
    * **is_legal** `boolean` Is the design road legal? Used for record keeping.
    * **svg_print** `string` The final [print file](/fundamentals/plate-files.md) in SVG format.
    * **svg_preview** `string` The [preview file](/fundamentals/plate-files.md) in SVG format if different from the print file (optional).
    * **custom_instructions** `string` Custom design instructions (optional).
* **products** `array` An array of objects.
    * **company_product_id** `integer` The ID of the [Company Product](/objects/company-product.md) being purchased.
    * **price** `integer` The price in pence it is being sold for.
    * **qty** `integer` The quantity.
* **shipping** `object`
    * **company_shipping_id** `integer` The ID of the [Company Shipping Option](/objects/company-shipping.md) being purchased.
    * **price** `integer` The price in pence it is being sold for.
    * **delivery_instructions** `string` Delivery instructions if the courier supports this (optional).
* **send_to** `object`
    * **first_name** `string` The recipient's first name.
    * **last_name** `string` The recipient's last name.
    * **email** `string` The recipient's email address.
    * **mobile_number** `string` The recipient's mobile number (required for some couriers) (optional).
    * **phone_number** `string` The recipient's phone number (optional).
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

## Example Request

!> Requires the `orders_write` permission.

> For testing purposes, pass the `?is_dummy=1` query parameter. This will create a test (dummy) order which will be omitted from your sales reports and won't be fulfilled by delegatees (if applicable).

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders`
* Method: `POST`
* Query:
  * is_dummy: `true`

```json
{
  "plates": [
    {
      "company_plate_id": 9602,
      "registration": "NG25 TTX",
      "price": 1500,
      "qty": 1,
      "is_legal": true,
      "svg_print": "<svg viewBox=\"0 0 520 111\"><!-- front plate --></svg>",
    },
    {
      "company_plate_id": 9603,
      "registration": "NG25 TTX",
      "price": 1500,
      "qty": 1,
      "is_legal": true,
      "svg_print": "<svg viewBox=\"0 0 520 111\"><!-- rear plate --></svg>",
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
  "send_to": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "mobile_number": "07777777777",
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