# Webhooks

Delivering transactional emails reliably can be a headache, especially when sending on behalf of others. This is why, after much deliberation, it was deemed beyond the scope of Plateit to implement.

!>Plateit does not send any transactional emails.

However, Plateit can send webhooks to a designated endpoint. This allows you to email your customers with the progress of their orders after being "pinged" by Plateit. But this is your responsibility.

Inside your company settings you can:

* Specify an endpoint for your webhooks.
* Set a secret key to verify the authenticity of the webhooks.
* Subscribe to the available event types:
  * `order:place`
  * `order-package:status-update`

>To determine the event type, your application needs to check the value in the incoming `X-Webhook-Event` header.

## Contact Hints

The `X-Webhook-Contact-Hint` header is included in each webhook sent by Plateit. Its value is either `true` or `false` (strings), indicating whether a transactional email should be sent to the customer.

* `true` suggests sending an email, as the event is significant enough to warrant customer notification.
* `false` implies the event is an internal update and an email may not be necessary.

Honouring the contact hint is recommended, as it helps ensure that customers receive relevant and timely updates. However, the decision to send an email ultimately lies with your application.

!> The customer's email address can be found in the included [OrderCustomer](/objects/order-customer.md) object. However, the location of this differs depending on the event type. See the example payloads below to observe the different structures.

## Webhook Authenticity

Plateit includes a digital signature in each webhook request to ensure authenticity. The signature, a hexadecimal string, is found in the incoming `Signature` header.

To verify a webhook's authenticity, use your company's secret key to generate a hash-based message authentication code (HMAC) and compare it to the signature. The steps are:

* Create an HMAC using the secret key and the webhook request body.
* Compare the generated HMAC to the `Signature` header.
* If they match, the webhook is authentic and untampered.

Below is an example using server-side JavaScript. The process is more-or-less the same for all programming languages.

```javascript
// Import dependencies.
const express = require('express')
const crypto = require('crypto')

// Initiate app.
const app = express()
app.use(express.json())

// Set the secret key that will be used to verify the digital signature.
const secretKey = 'the_same_secret_key_in_your_settings'

// Define an endpoint route for your webhook listener.
app.post('/webhook-listener', (req, res) => {

  // Extract the pertinent data from the incoming request.
  const signature = req.header('Signature')
  const eventType = req.header('X-Webhook-Event')
  const makeContact = req.header('X-Webhook-Contact-Hint') === 'true'
  const payloadObj = req.body
  const payloadRaw = req.rawBody

  // Ensure data is well formed.
  if (!signature || !eventType || !payloadRaw || typeof payloadObj !== 'object') {
    return res.status(400).send('Invalid request')
  }

  // Generate a digital signature using the secret key and SHA-256 algorithm.
  const hmac = crypto.createHmac('sha256', secretKey)
  hmac.update(payloadRaw)
  const generatedSignature = hmac.digest('hex')

  // Compare the generated signature with the one in the request header.
  if (generatedSignature !== signature) {
    return res.status(401).send('Invalid webhook signature')
  }

  // If we get this far, the webhook is legitimate.

  // Handle payloadObj data here.

  return res.status(200).send('Webhook processed')
})
```

## Failing Webhooks

Webhook attempts that timeout or do no receive a 2XX response code will retry later. Persistently failing webhooks will be removed from the send queue and the company will be notified by email and encouraged to fix the problem.

## Event Types

Plateit currently supports two event types: `order:place` and `order-package:status-update`. These events are triggered by specific actions and provide relevant information about the order or package.

### order:place

This webhook is triggered when full payment is received for a draft [Order](/objects/order.md) (an order with either an `External Draft` or `Internal Draft` [SystemOrderStatus](/objects/system-order-status.md)). Upon payment, the order's corresponding [OrderPackage](/objects/order-package.md) objects will be marked as committed. When this occurs, an `order:place` webhook will be sent to your designated endpoint containing the entire [Order](/objects/order.md) object, including (most of) its nested relationships. The `X-Webhook-Contact-Hint` for this event is always `true`, as the order placement is a significant event that warrants customer notification.

#### Example

<!-- tabs:start -->

#### **Headers**

* Content-Type: `application/json`
* Signature: `9f86d081884c7d659a2feaa0c55ad023d9d677abf78fa9c65e2c63e3936461a5`
* X-Webhook-Contact-Hint: `true`
* X-Webhook-Event: `order:place`

#### **Payload**

```json
{
  "id": 323,
  "company_id": 1,
  "system_order_status_id": 3,
  "system_order_fulfilment_status_id": 1,
  "amount_subtotal": 3082,
  "amount_shipping": 416,
  "amount_vat": 702,
  "amount_total": 4200,
  "amount_paid": 4200,
  "amount_refunded": 0,
  "amount_vat_collected": 702,
  "amount_vat_refunded": 0,
  "packages_count": 1,
  "is_dummy": true,
  "opened_at": "2025-04-20T15:30:01.000000Z",
  "created_at": "2025-04-20T15:27:27.000000Z",
  "updated_at": "2025-04-20T15:30:01.000000Z",
  "href": "/orders/323",
  "company": {
    "id": 1,
    "name": "Top Plates LTD",
    "email": "info@top-plates.com",
    "phone_number": "0115 9876543",
    "website_url": "https://top-plates.com",
    "address_line_1": "234 Fake Road",
    "address_line_2": null,
    "address_line_3": "Leeds",
    "address_postcode": "LS7 6QZ",
    "address_country_code": "GB",
    "created_at": "2025-04-15T15:27:34.000000Z",
    "updated_at": "2025-04-16T11:41:22.000000Z",
    "href": "/companies/1"
  },
  "system_order_status": {
    "id": 3,
    "name": "Open",
    "description": "The order is open and ready for processing.",
    "href": "/system-order-statuses/3"
  },
  "system_order_fulfilment_status": {
    "id": 1,
    "name": "Unfulfilled",
    "description": "The order has been completed and is awaiting manufacture.",
    "href": "/system-order-fulfilment-statuses/1"
  },
  "customer": {
    "order_id": 323,
    "first_name": "Joe",
    "last_name": "Bloggs",
    "email": "joe.bloggs@mailinator.com",
    "mobile_number": null,
    "phone_number": null,
    "created_at": "2025-04-20T15:27:27.000000Z",
    "updated_at": "2025-04-20T15:27:27.000000Z",
    "href": "/orders/323/customer"
  },
  "ship_to": {
    "order_id": 323,
    "first_name": "Joe",
    "last_name": "Bloggs",
    "address_line_1": "10 Downing Street",
    "address_line_2": null,
    "address_line_3": "London",
    "address_postcode": "SW1A 2AA",
    "address_country_code": "GB",
    "created_at": "2025-04-20T15:27:27.000000Z",
    "updated_at": "2025-04-20T15:27:27.000000Z",
    "href": "/orders/323/ship-to"
  },
  "bill_to": null,
  "packages": [
    {
      "id": 570,
      "order_id": 323,
      "delegate_to_company_id": null,
      "system_package_status_id": 1,
      "plates_qty": 2,
      "products_qty": 2,
      "width": 520,
      "height": 83,
      "depth": 111,
      "weight": 464,
      "has_overridden_dimensions": false,
      "is_committed": true,
      "is_shipping_synced": false,
      "is_paperwork_printed": false,
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:30:00.000000Z",
      "href": "/orders/323/packages/570",
      "system_package_status": {
        "id": 1,
        "name": "Unprocessed",
        "description": "The contents of the package are waiting to be processed.",
        "href": "/system-package-statuses/1"
      },
      "delegate_to_company": null,
      "shipping": {
        "package_id": 570,
        "system_courier_service_id": 2,
        "company_shipping_id": 2,
        "name": "Manual Post (1)",
        "additional_options": null,
        "price": 416,
        "price_vat": 84,
        "price_gross": 500,
        "external_shipment_id": null,
        "label_files": [],
        "tracking_code": null,
        "delivery_instructions": null,
        "despatched_at": null,
        "created_at": "2025-04-20T15:27:27.000000Z",
        "updated_at": "2025-04-20T15:28:25.000000Z",
        "href": "/orders/323/packages/570/shipping"
      },
      "plates": [
        {
          "id": 1106,
          "package_id": 570,
          "company_plate_id": 1,
          "company_plate_id_delegated": null,
          "registration": "PS26 YTR",
          "type": "Standard",
          "colour": "white",
          "width": 520,
          "height": 111,
          "depth": 3,
          "weight": 200,
          "price": 1250,
          "price_vat": 250,
          "price_gross": 1500,
          "qty": 1,
          "is_printable": true,
          "is_printed": false,
          "custom_instructions": null,
          "design_preview": "/assets/plates/1/323/1jDAivGtK9mCxrwL.preview.svg?v=1",
          "design_print": "/assets/plates/1/323/1jDAivGtK9mCxrwL.print.svg?v=1",
          "design_object": {},
          "created_at": "2025-04-20T15:27:27.000000Z",
          "updated_at": "2025-04-20T15:28:37.000000Z",
          "href": "/orders/323/packages/570/plates/1106"
        },
        {
          "id": 1107,
          "package_id": 570,
          "company_plate_id": 2,
          "company_plate_id_delegated": null,
          "registration": "PS26 YTR",
          "type": "Standard",
          "colour": "yellow",
          "width": 520,
          "height": 111,
          "depth": 3,
          "weight": 200,
          "price": 1250,
          "price_vat": 250,
          "price_gross": 1500,
          "qty": 1,
          "is_printable": true,
          "is_printed": false,
          "custom_instructions": null,
          "design_preview": "/assets/plates/1/323/PBZWuSsIq2oYEo3m.preview.svg?v=1",
          "design_print": "/assets/plates/1/323/PBZWuSsIq2oYEo3m.print.svg?v=1",
          "design_object": {},
          "created_at": "2025-04-20T15:27:27.000000Z",
          "updated_at": "2025-04-20T15:28:44.000000Z",
          "href": "/orders/323/packages/570/plates/1107"
        }
      ],
      "products": [
        {
          "id": 608,
          "package_id": 570,
          "company_product_id": 1,
          "company_product_id_delegated": null,
          "name": "Sticky Pads",
          "sku": "stickypads",
          "width": 80,
          "height": 71,
          "depth": 1,
          "weight": 52,
          "price": 166,
          "price_vat": 34,
          "price_gross": 200,
          "qty": 1,
          "created_at": "2025-04-20T15:28:06.000000Z",
          "updated_at": "2025-04-20T15:28:15.000000Z",
          "href": "/orders/323/products/608"
        },
        {
          "id": 607,
          "package_id": 570,
          "company_product_id": 3,
          "company_product_id_delegated": null,
          "name": "USB-C Car Phone Charger",
          "sku": "usb-ccarphonecharger",
          "width": 31,
          "height": 96,
          "depth": 76,
          "weight": 12,
          "price": 416,
          "price_vat": 84,
          "price_gross": 500,
          "qty": 1,
          "created_at": "2025-04-20T15:27:27.000000Z",
          "updated_at": "2025-04-20T15:27:57.000000Z",
          "href": "/orders/323/products/607"
        }
      ],
      "notes": []
    }
  ]
}
```

<!-- tabs:end -->

### order-package:status-update

This webhook is triggered when the [SystemPackageStatus](/objects/system-package-status.md) of an [OrderPackage](/objects/order-package.md) is updated. The `X-Webhook-Contact-Hint` for this event is only `true` if the user changing the status requests it. For more information on updating package statuses, [see here](/helpers/update-order-package-statuses.md).

#### Example

<!-- tabs:start -->

#### **Headers**

* Content-Type: `application/json`
* Signature: `4538edefade3fdc71a9d3df8dfd4d89d94faf0c54f9e2490f16989901fc7438f`
* X-Webhook-Contact-Hint: `true`
* X-Webhook-Event: `order-package:status-update`

#### **Payload**

```json
{
  "id": 570,
  "order_id": 323,
  "delegate_to_company_id": null,
  "system_package_status_id": 4,
  "plates_qty": 2,
  "products_qty": 2,
  "width": 520,
  "height": 83,
  "depth": 111,
  "weight": 464,
  "has_overridden_dimensions": false,
  "is_committed": true,
  "is_shipping_synced": false,
  "is_paperwork_printed": false,
  "created_at": "2025-04-20T15:27:27.000000Z",
  "updated_at": "2025-04-20T15:43:09.000000Z",
  "href": "/orders/323/packages/570",
  "system_package_status": {
    "id": 4,
    "name": "Despatched",
    "description": "The package has been despatched.",
    "href": "/system-package-statuses/4"
  },
  "delegate_to_company": null,
  "order": {
    "id": 323,
    "company_id": 1,
    "system_order_status_id": 4,
    "system_order_fulfilment_status_id": 3,
    "amount_subtotal": 3082,
    "amount_shipping": 416,
    "amount_vat": 702,
    "amount_total": 4200,
    "amount_paid": 4200,
    "amount_refunded": 0,
    "amount_vat_collected": 702,
    "amount_vat_refunded": 0,
    "packages_count": 1,
    "is_dummy": true,
    "opened_at": "2025-04-20T15:30:01.000000Z",
    "created_at": "2025-04-20T15:27:27.000000Z",
    "updated_at": "2025-04-20T15:43:09.000000Z",
    "href": "/orders/323",
    "company": {
      "id": 1,
      "name": "Top Plates LTD",
      "email": "info@top-plates.com",
      "phone_number": "0115 9876543",
      "website_url": "https://top-plates.com",
      "address_line_1": "234 Fake Road",
      "address_line_2": null,
      "address_line_3": "Leeds",
      "address_postcode": "LS7 6QZ",
      "address_country_code": "GB",
      "created_at": "2025-04-15T15:27:34.000000Z",
      "updated_at": "2025-04-16T11:41:22.000000Z",
      "href": "/companies/1"
    },
    "customer": {
      "order_id": 323,
      "first_name": "Joe",
      "last_name": "Bloggs",
      "email": "joe.bloggs@mailinator.com",
      "mobile_number": null,
      "phone_number": null,
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:27:27.000000Z",
      "href": "/orders/323/customer"
    },
    "ship_to": {
      "order_id": 323,
      "first_name": "Joe",
      "last_name": "Bloggs",
      "address_line_1": "10 Downing Street",
      "address_line_2": null,
      "address_line_3": "London",
      "address_postcode": "SW1A 2AA",
      "address_country_code": "GB",
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:27:27.000000Z",
      "href": "/orders/323/ship-to"
    }
  },
  "shipping": {
    "package_id": 570,
    "system_courier_service_id": 2,
    "company_shipping_id": 2,
    "name": "Manual Post (1)",
    "additional_options": null,
    "price": 416,
    "price_vat": 84,
    "price_gross": 500,
    "external_shipment_id": null,
    "label_files": [],
    "tracking_code": null,
    "delivery_instructions": null,
    "despatched_at": "2025-04-20T15:43:09.000000Z",
    "created_at": "2025-04-20T15:27:27.000000Z",
    "updated_at": "2025-04-20T15:43:09.000000Z",
    "href": "/orders/323/packages/570/shipping",
    "system_courier_service": {
      "id": 2,
      "courier_key": "manual",
      "name": "Manual Post",
      "priority_level": 3,
      "service_reference": "n/a",
      "additional_options": null,
      "is_international": false,
      "max_width": 1000000,
      "max_height": 1000000,
      "max_depth": 1000000,
      "max_weight": 1000000,
      "position": 2,
      "is_active": true,
      "href": "/system-courier-services/2"
    }
  },
  "plates": [
    {
      "id": 1106,
      "package_id": 570,
      "company_plate_id": 1,
      "company_plate_id_delegated": null,
      "registration": "PS26 YTR",
      "type": "Standard",
      "colour": "white",
      "width": 520,
      "height": 111,
      "depth": 3,
      "weight": 200,
      "price": 1250,
      "price_vat": 250,
      "price_gross": 1500,
      "qty": 1,
      "is_printable": true,
      "is_printed": false,
      "custom_instructions": null,
      "design_preview": "/assets/plates/1/323/1jDAivGtK9mCxrwL.preview.svg?v=1",
      "design_print": "/assets/plates/1/323/1jDAivGtK9mCxrwL.print.svg?v=1",
      "design_object": {},
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:28:37.000000Z",
      "href": "/orders/323/packages/570/plates/1106"
    },
    {
      "id": 1107,
      "package_id": 570,
      "company_plate_id": 2,
      "company_plate_id_delegated": null,
      "registration": "PS26 YTR",
      "type": "Standard",
      "colour": "yellow",
      "width": 520,
      "height": 111,
      "depth": 3,
      "weight": 200,
      "price": 1250,
      "price_vat": 250,
      "price_gross": 1500,
      "qty": 1,
      "is_printable": true,
      "is_printed": false,
      "custom_instructions": null,
      "design_preview": "/assets/plates/1/323/PBZWuSsIq2oYEo3m.preview.svg?v=1",
      "design_print": "/assets/plates/1/323/PBZWuSsIq2oYEo3m.print.svg?v=1",
      "design_object": {},
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:28:44.000000Z",
      "href": "/orders/323/packages/570/plates/1107"
    }
  ],
  "products": [
    {
      "id": 608,
      "package_id": 570,
      "company_product_id": 1,
      "company_product_id_delegated": null,
      "name": "Sticky Pads (1)",
      "sku": "stickypads",
      "width": 80,
      "height": 71,
      "depth": 1,
      "weight": 52,
      "price": 166,
      "price_vat": 34,
      "price_gross": 200,
      "qty": 1,
      "created_at": "2025-04-20T15:28:06.000000Z",
      "updated_at": "2025-04-20T15:28:15.000000Z",
      "href": "/orders/323/products/608"
    },
    {
      "id": 607,
      "package_id": 570,
      "company_product_id": 3,
      "company_product_id_delegated": null,
      "name": "USB-C Car Phone Charger (1)",
      "sku": "usb-ccarphonecharger",
      "width": 31,
      "height": 96,
      "depth": 76,
      "weight": 12,
      "price": 416,
      "price_vat": 84,
      "price_gross": 500,
      "qty": 1,
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:27:57.000000Z",
      "href": "/orders/323/products/607"
    }
  ],
  "notes": [],
  "ship_to_override": null
}
```

<!-- tabs:end -->