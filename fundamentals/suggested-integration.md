# Suggested Website Integration

This page assumes you are developing a website that sells number plates. Here you will find a suggested way to integrate Plateit that will be practical and sufficient for most use cases.

## Prerequisites

You will need a [CompanyAccessToken](/objects/company-access-token.md) with the following permissions:

* `company_plates_read`
* `company_products_read`
* `company_shipping_options_read`
* `orders_build`

Although outside the scope of this tutorial, you may also want to include the following permissions if you intend on your application being able to [edit purchased plates at a later date](/fundamentals/editing-existing-plate-designs.md).

* `orders_read`
* `company_plate_types_read`
* `orders_packages_plates_write`

## Overview

Here is a bulletted list of stages to help understand what goes on behind the scenes:

1. A request is made to Plateit to obtain all available [CompanyPlate](/objects/company-plate.md) objects.
2. This data is used to build a customer-facing number plate designer.
3. The customer designs their plates and adds them to a basket.
4. Further requests are made to Plateit to obtain the available [CompanyShippingOption](/objects/company-shipping-option.md) objects and [CompanyProduct](/objects/company-product.md) objects (upsells).
5. The customer adds any extra products to the basket and selects a shipping option.
6. The contents of the basket are used to build the final [BuildOrder](/helpers/build-order.md) payload which is sent to Plateit. This creates a new [Order](/objects/order.md) with an `External Draft` status and its ID is returned.
7. The draft order ID is passed to the payment processor.
8. Once paid, the payment processor sends a webhook to Plateit.
9. Plateit receieves the webhook and changes its status to `Open` (active).
10. Plateit then sends a webhook to your application which triggers a confirmation email.

> The number plate designer and the shopping basket are your responsibilty to build. A modern, javascript website boilerplate can be purchased at an additional charge. It is a fully functional application with everything built in which will save a lot of time and development money.

## Fetching Available Plates

When a customer lands on your designer page, make a request to obtain all of your available [CompanyPlate](/objects/company-plate.md) objects with their pertinent relationships. The quantity of results can be up to 1000.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/company-plates`
* Method: `GET`
* Query:
  * per_page: `1000`
  * filter_by[]: `is_active:true`
  * filter_by[]: `company_plate_type.is_active:true`
  * exclude_unmatched_delegations: `true` *
  * with[]: `system_plate_size`
  * with[]: `company_plate_type`

\* *Ensures any plates delegated to another company are excluded if the delegated company doesn't have a matching plate in their catalogue.*

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 385,
      "system_plate_size_id": 1,
      "company_plate_type_id": 14,
      "colour": "white",
      "price": 1499,
      "is_front": true,
      "is_rear": false,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:53:40.000000Z",
      "updated_at": "2024-09-30T09:53:40.000000Z",
      "href": "/plates/385",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
        "id": 14,
        "name": "Standard",
        "reference": "standard",
        "depth": 3,
        "weight_std_oblong": 200,
        "is_printable": true,
        "is_active": true,
        "delegate_to_company_id": null,
        "created_at": "2024-09-30T09:00:18.000000Z",
        "updated_at": "2024-09-30T09:00:18.000000Z",
        "href": "/plate-types/14"
      }
    },
    {
      "id": 386,
      "system_plate_size_id": 1,
      "company_plate_type_id": 14,
      "colour": "yellow",
      "price": 1499,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:54:13.000000Z",
      "updated_at": "2024-09-30T09:54:13.000000Z",
      "href": "/plates/386",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
        "id": 14,
        "name": "Standard",
        "reference": "standard",
        "depth": 3,
        "weight_std_oblong": 200,
        "is_printable": true,
        "is_active": true,
        "delegate_to_company_id": null,
        "created_at": "2024-09-30T09:00:18.000000Z",
        "updated_at": "2024-09-30T09:00:18.000000Z",
        "href": "/plate-types/14"
      }
    },
    {
      "id": 387,
      "system_plate_size_id": 2,
      "company_plate_type_id": 14,
      "colour": "white",
      "price": 1499,
      "is_front": true,
      "is_rear": false,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:54:41.000000Z",
      "updated_at": "2024-09-30T09:54:41.000000Z",
      "href": "/plates/387",
      "system_plate_size": {
        "id": 2,
        "width": 279,
        "height": 203,
        "line_span": 2,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 40,
        "href": "/system-plate-sizes/2"
      },
      "company_plate_type": {
        "id": 14,
        "name": "Standard",
        "reference": "standard",
        "depth": 3,
        "weight_std_oblong": 200,
        "is_printable": true,
        "is_active": true,
        "delegate_to_company_id": null,
        "created_at": "2024-09-30T09:00:18.000000Z",
        "updated_at": "2024-09-30T09:00:18.000000Z",
        "href": "/plate-types/14"
      }
    },
    {
      "id": 388,
      "system_plate_size_id": 2,
      "company_plate_type_id": 14,
      "colour": "yellow",
      "price": 1499,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:55:03.000000Z",
      "updated_at": "2024-09-30T09:55:03.000000Z",
      "href": "/plates/388",
      "system_plate_size": {
        "id": 2,
        "width": 279,
        "height": 203,
        "line_span": 2,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 40,
        "href": "/system-plate-sizes/2"
      },
      "company_plate_type": {
        "id": 14,
        "name": "Standard",
        "reference": "standard",
        "depth": 3,
        "weight_std_oblong": 200,
        "is_printable": true,
        "is_active": true,
        "delegate_to_company_id": null,
        "created_at": "2024-09-30T09:00:18.000000Z",
        "updated_at": "2024-09-30T09:00:18.000000Z",
        "href": "/plate-types/14"
      }
    },
    {
      "id": 389,
      "system_plate_size_id": 3,
      "company_plate_type_id": 14,
      "colour": "yellow",
      "price": 1499,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:55:16.000000Z",
      "updated_at": "2024-09-30T09:55:16.000000Z",
      "href": "/plates/389",
      "system_plate_size": {
        "id": 3,
        "width": 229,
        "height": 178,
        "line_span": 2,
        "vehicle": "motorcycle",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 30,
        "href": "/system-plate-sizes/3"
      },
      "company_plate_type": {
        "id": 14,
        "name": "Standard",
        "reference": "standard",
        "depth": 3,
        "weight_std_oblong": 200,
        "is_printable": true,
        "is_active": true,
        "delegate_to_company_id": null,
        "created_at": "2024-09-30T09:00:18.000000Z",
        "updated_at": "2024-09-30T09:00:18.000000Z",
        "href": "/plate-types/14"
      }
    },
    {
      "id": 390,
      "system_plate_size_id": 1,
      "company_plate_type_id": 15,
      "colour": "white",
      "price": 1999,
      "is_front": true,
      "is_rear": false,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:56:08.000000Z",
      "updated_at": "2024-09-30T09:56:08.000000Z",
      "href": "/plates/390",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
        "id": 15,
        "name": "4D Laser Cut",
        "reference": "4dlasercut",
        "depth": 6,
        "weight_std_oblong": 215,
        "is_printable": true,
        "is_active": true,
        "delegate_to_company_id": null,
        "created_at": "2024-09-30T09:00:18.000000Z",
        "updated_at": "2024-09-30T09:00:18.000000Z",
        "href": "/plate-types/15"
      }
    },
    {
      "id": 391,
      "system_plate_size_id": 1,
      "company_plate_type_id": 15,
      "colour": "yellow",
      "price": 1999,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:56:35.000000Z",
      "updated_at": "2024-09-30T09:56:35.000000Z",
      "href": "/plates/391",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
        "id": 15,
        "name": "4D Laser Cut",
        "reference": "4dlasercut",
        "depth": 6,
        "weight_std_oblong": 215,
        "is_printable": true,
        "is_active": true,
        "delegate_to_company_id": null,
        "created_at": "2024-09-30T09:00:18.000000Z",
        "updated_at": "2024-09-30T09:00:18.000000Z",
        "href": "/plate-types/15"
      }
    }
  ]
}
```

<!-- tabs:end -->

Once fetched, loop over the results to extract all of the [CompanyPlateType](/objects/company-plate-type.md) objects in play and use this data to dynamically build your customer-facing "Plate Type" and "Plate Size" selectors.

## Fetching Extra Products

Assuming your customer has designed a plate and added it to a basket, you may now want to present them with additional upsell items. Here is an example request to obtain the available [CompanyProduct](/objects/company-product.md) objects:

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/company-products`
* Method: `GET`
* Query:
  * per_page: `1000`
  * filter_by: `is_active:true`
  * exclude_unmatched_delegations: `true` *

\* *Ensures any products delegated to another company are excluded if the delegated company doesn't have a matching product in their catalogue.*

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

## Fetching Shipping Options

The last `GET` request you'll need to make is to obtain the available [CompanyShippingOption](/objects/company-shipping-option.md) objects to present to the customer.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/company-shipping-options`
* Method: `GET`
* Query:
  * per_page: `1000`
  * filter_by: `is_active:true`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 11,
      "system_courier_service_id": 1,
      "name": "Free Collection From Store",
      "additional_options": null,
      "price": 0,
      "is_active": true,
      "created_at": "2025-01-16T10:42:45.000000Z",
      "updated_at": "2025-01-16T10:42:45.000000Z",
      "href": "/shipping-options/11",
      "system_courier_service": {
        "id": 1,
        "courier_key": "manual",
        "name": "Manual Collection",
        "priority_level": 3,
        "service_reference": "n/a",
        "additional_options": null,
        "is_international": false,
        "max_width": 1000000,
        "max_height": 1000000,
        "max_depth": 1000000,
        "max_weight": 1000000,
        "position": 1,
        "is_active": true,
        "href": "/system-courier-services/1"
      }
    }
  ]
}
```

<!-- tabs:end -->

## Creating the Order

The contents of the basket and the selected shipping option are used to build the final payload to send to Plateit to create the `External Draft` order. More information can be found on the [BuildOrder](/helpers/build-order.md) page.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/actions/build-order`
* Method: `POST`

```json
{
  "plates": [
    {
      "company_plate_id": 385,
      "registration": "NG25 TTX",
      "price_gross": 1499,
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
      "company_plate_id": 386,
      "registration": "NG25 TTX",
      "price_gross": 1499,
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
      "company_product_id": 14,
      "price_gross": 299,
      "qty": 1
    }
  ],
  "shipping": {
    "company_shipping_id": 11,
    "price_gross": 0
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

* Status code: `200`

```json
{
  "id": 9576,
  "message": "Order successfully created."
}
```

<!-- tabs:end -->

Upon success, a new [Order](/objects/order.md) is created with an `External Draft` status and its order ID can be extracted from the response body.

## Processing the Payment

The order ID returned from the last stage is to be sent to PayPal using PayPal's `invoice_id` parameter. Important PayPal setup instructions can be found [here](/fundamentals/paypal.md).

## Activating the Order

Once the payment has been processed, PayPal will send a webhook to Plateit to notify it of the payment. If the payment has been made in full, Plateit will update the order status from `External Draft` to `Open` (active).

When this occurs, Plateit will send an `order:place` webhook to your application containing the entire [Order](/objects/order.md) object. When your application receives this, it is recommended to use the data within it to send the customer a confirmation email. More information about Plateit's webhooks can be found [here](/fundamentals/webhooks.md).