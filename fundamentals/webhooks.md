# Webhooks

Plateit can send webhooks for certain events to a designated endpoint. This allows you to notify customers about the progress of their orders after being "pinged" by Plateit. However, sending those notifications is your responsibility.

!> Plateit does not send any transactional emails.

Inside your company settings you can:

* Specify an endpoint for your webhooks.
* Set a secret key to verify the authenticity of the webhooks.
* Subscribe to the available event types:
  * `order:place`
  * `order-document:status-update`
  * `order-package:status-update`

> To determine the event type, your application should check the value in the incoming `X-Webhook-Event` header.

## Contact Hints

The `X-Webhook-Contact-Hint` header is included in each webhook sent by Plateit. Its value is either `true` or `false` as a string, indicating whether a transactional email should normally be sent to the customer.

* `true` suggests sending an email, as the event is significant enough to warrant customer notification.
* `false` implies the event is primarily an internal update and an email may not be necessary.

Honouring the contact hint is recommended, as it helps ensure customers receive relevant and timely updates. However, the decision to send an email ultimately lies with your application.

!> The customer's email address can be found in the included [OrderCustomer](/objects/order-customer.md) object. However, its location differs depending on the event type. See the example payloads below for the different structures.

## Event Types

### order:place

This webhook is triggered when full payment is received for a draft [Order](/objects/order.md) - an order with either an `External Draft` or `Internal Draft` [SystemOrderStatus](/objects/system-order-status.md).

It represents a successful order placement from a commercial perspective and is typically the event used to notify the customer that their order has been received and paid for.

The `X-Webhook-Contact-Hint` for this event is always `true`.

> An `order:place` event does not necessarily mean the order has become `Open`. If required supporting documents are still awaiting upload or approval, the order may remain in a draft state until those requirements have been satisfied. The incoming `Order` object includes a `system_order_document_status` object, which can be used to determine and communicate any further action the customer needs to take.

> When all required supporting documents have been approved, a fully paid draft order will automatically become `Open` and its uncancelled packages will be committed for fulfilment.

The payload contains the [Order](/objects/order.md) and its relevant nested relationships.

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
  "system_order_status_id": 1,
  "system_order_document_status_id": 2,
  "system_order_fulfilment_status_id": 1,
  "amount_subtotal": 3700,
  "amount_shipping": 500,
  "amount_total": 4200,
  "amount_paid": 4200,
  "amount_refunded": 0,
  "packages_count": 1,
  "identifier": null,
  "opened_at": null,
  "created_at": "2025-04-20T15:27:27.000000Z",
  "updated_at": "2025-04-20T15:30:01.000000Z",
  "href": "/v3/orders/323",
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
    "href": "/v3/companies/1"
  },
  "system_order_status": {
    "id": 1,
    "name": "External Draft",
    "description": "The order has been created externally, for example, by a customer on a website or app, but is not yet in a fulfillable state.",
    "href": "/v3/system-order-statuses/1"
  },
  "system_order_document_status": {
    "id": 2,
    "name": "Awaiting Upload",
    "description": "One or more required documents have not yet been supplied.",
    "href": "/v3/system-order-document-statuses/2"
  },
  "system_order_fulfilment_status": {
    "id": 1,
    "name": "Unfulfilled",
    "description": "The order has been completed and is awaiting manufacture.",
    "href": "/v3/system-order-fulfilment-statuses/1"
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
    "href": "/v3/orders/323/customer"
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
    "href": "/v3/orders/323/ship-to"
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
      "is_committed": false,
      "is_shipping_synced": false,
      "is_paperwork_printed": false,
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:30:00.000000Z",
      "href": "/v3/orders/323/packages/570",
      "system_package_status": {
        "id": 1,
        "name": "Unprocessed",
        "description": "The contents of the package are waiting to be processed.",
        "href": "/v3/system-package-statuses/1"
      },
      "delegate_to_company": null,
      "shipping": {
        "package_id": 570,
        "system_courier_service_id": 2,
        "company_shipping_id": 2,
        "name": "Manual Post",
        "price": 500,
        "external_shipment_id": null,
        "label_files": [],
        "tracking_code": null,
        "delivery_instructions": null,
        "despatched_at": null,
        "created_at": "2025-04-20T15:27:27.000000Z",
        "updated_at": "2025-04-20T15:28:25.000000Z",
        "href": "/v3/orders/323/packages/570/shipping"
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
          "price": 1500,
          "qty": 1,
          "requires_docs": true,
          "is_printable": true,
          "is_printed": false,
          "custom_instructions": null,
          "design_preview": "/v3/assets/plates/1/323/1jDAivGtK9mCxrwL.preview.svg?v=1",
          "design_print": "/v3/assets/plates/1/323/1jDAivGtK9mCxrwL.print.svg?v=1",
          "design_object": {},
          "created_at": "2025-04-20T15:27:27.000000Z",
          "updated_at": "2025-04-20T15:28:37.000000Z",
          "href": "/v3/orders/323/packages/570/plates/1106"
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
          "price": 1500,
          "qty": 1,
          "requires_docs": true,
          "is_printable": true,
          "is_printed": false,
          "custom_instructions": null,
          "design_preview": "/v3/assets/plates/1/323/PBZWuSsIq2oYEo3m.preview.svg?v=1",
          "design_print": "/v3/assets/plates/1/323/PBZWuSsIq2oYEo3m.print.svg?v=1",
          "design_object": {},
          "created_at": "2025-04-20T15:27:27.000000Z",
          "updated_at": "2025-04-20T15:28:44.000000Z",
          "href": "/v3/orders/323/packages/570/plates/1107"
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
          "price": 200,
          "qty": 1,
          "created_at": "2025-04-20T15:28:06.000000Z",
          "updated_at": "2025-04-20T15:28:15.000000Z",
          "href": "/v3/orders/323/products/608"
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
          "price": 500,
          "qty": 1,
          "created_at": "2025-04-20T15:27:27.000000Z",
          "updated_at": "2025-04-20T15:27:57.000000Z",
          "href": "/v3/orders/323/products/607"
        }
      ],
      "notes": []
    }
  ]
}
```

<!-- tabs:end -->

### order-document:status-update

This webhook is triggered when the status of an [OrderDocument](/objects/order-document.md) is updated, for example when a supporting document is approved or rejected.

The payload contains the updated `OrderDocument` together with its associated [Order](/objects/order.md) and relevant nested relationships.

The `X-Webhook-Contact-Hint` value depends on the new document status:

* `true` indicates that the update is significant enough that the customer should normally be contacted.
* `false` indicates that the update is primarily an internal state change and customer contact may not be necessary.

> A document status update may also change the parent order's [SystemOrderDocumentStatus](/objects/system-order-document-status.md).

> If the final required supporting document is approved for a fully paid draft order, the order may automatically become `Open` and its uncancelled packages will be committed for fulfilment.

For more information about supporting documents, uploading files and document approval, see the [Supporting Documents](/fundamentals/documents.md) guide.

#### Example

<!-- tabs:start -->

#### **Headers**

* Content-Type: `application/json`
* Signature: `7ac19e4f2b8d6a03c5f1e9b7d4a2c8f06e3b9d1a7f5c2e8b4d6a0f3c9e1b7efa`
* X-Webhook-Contact-Hint: `true`
* X-Webhook-Event: `order-document:status-update`

#### **Payload**

```json
{
  "id": 1230,
  "order_id": 323,
  "type": "entitlement",
  "subtype": "v5c",
  "registration": "PS26 YTR",
  "mime_type": "image/jpeg",
  "size": 109916,
  "status": "rejected",
  "rejection_reason": "reg_does_not_match",
  "file": "/v3/orders/323/documents/1230/file",
  "approved_at": null,
  "created_at": "2025-04-20T16:00:01.000000Z",
  "updated_at": "2025-05-20T09:01:12.000000Z",
  "href": "/v3/orders/323/documents/1230",
  "order": {
    "id": 323,
    "company_id": 1,
    "system_order_status_id": 1,
    "system_order_document_status_id": 2,
    "system_order_fulfilment_status_id": 1,
    "amount_subtotal": 3082,
    "amount_shipping": 416,
    "amount_total": 4200,
    "amount_paid": 4200,
    "amount_refunded": 0,
    "packages_count": 1,
    "identifier": null,
    "opened_at": null,
    "created_at": "2025-04-20T15:27:27.000000Z",
    "updated_at": "2025-04-20T15:30:01.000000Z",
    "href": "/v3/orders/323",
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
      "href": "/v3/companies/1"
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
      "href": "/v3/orders/323/customer"
    }
  }
}
```

<!-- tabs:end -->

### order-package:status-update

This webhook is triggered when the [SystemPackageStatus](/objects/system-package-status.md) of an [OrderPackage](/objects/order-package.md) is updated.

The `X-Webhook-Contact-Hint` for this event is only `true` if the user changing the status requests it.

For more information on updating package statuses, see [UpdateOrderPackageStatuses](/helpers/update-order-package-statuses.md).

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
  "is_shipping_synced": true,
  "is_paperwork_printed": true,
  "created_at": "2025-04-20T15:27:27.000000Z",
  "updated_at": "2025-04-20T15:43:09.000000Z",
  "href": "/v3/orders/323/packages/570",
  "system_package_status": {
    "id": 4,
    "name": "Despatched",
    "description": "The package has been despatched.",
    "href": "/v3/system-package-statuses/4"
  },
  "delegate_to_company": null,
  "order": {
    "id": 323,
    "company_id": 1,
    "system_order_status_id": 4,
    "system_order_document_status_id": 4,
    "system_order_fulfilment_status_id": 3,
    "amount_subtotal": 3700,
    "amount_shipping": 500,
    "amount_total": 4200,
    "amount_paid": 4200,
    "amount_refunded": 0,
    "packages_count": 1,
    "identifier": null,
    "opened_at": "2025-04-20T15:30:01.000000Z",
    "created_at": "2025-04-20T15:27:27.000000Z",
    "updated_at": "2025-04-20T15:43:09.000000Z",
    "href": "/v3/orders/323",
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
      "href": "/v3/companies/1"
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
      "href": "/v3/orders/323/customer"
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
      "href": "/v3/orders/323/ship-to"
    }
  },
  "shipping": {
    "package_id": 570,
    "system_courier_service_id": 2,
    "company_shipping_id": 2,
    "name": "Manual Post",
    "price": 500,
    "external_shipment_id": null,
    "label_files": [],
    "tracking_code": null,
    "delivery_instructions": null,
    "despatched_at": "2025-04-20T15:43:09.000000Z",
    "created_at": "2025-04-20T15:27:27.000000Z",
    "updated_at": "2025-04-20T15:43:09.000000Z",
    "href": "/v3/orders/323/packages/570/shipping",
    "system_courier_service": {
      "id": 2,
      "courier_key": "manual",
      "name": "Manual Post",
      "priority_level": 3,
      "is_international": false,
      "is_active": true,
      "href": "/v3/system-courier-services/2"
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
      "price": 1500,
      "qty": 1,
      "requires_docs": true,
      "is_printable": true,
      "is_printed": false,
      "custom_instructions": null,
      "design_preview": "/v3/assets/plates/1/323/1jDAivGtK9mCxrwL.preview.svg?v=1",
      "design_print": "/v3/assets/plates/1/323/1jDAivGtK9mCxrwL.print.svg?v=1",
      "design_object": {},
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:28:37.000000Z",
      "href": "/v3/orders/323/packages/570/plates/1106"
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
      "price": 1500,
      "qty": 1,
      "requires_docs": true,
      "is_printable": true,
      "is_printed": false,
      "custom_instructions": null,
      "design_preview": "/v3/assets/plates/1/323/PBZWuSsIq2oYEo3m.preview.svg?v=1",
      "design_print": "/v3/assets/plates/1/323/PBZWuSsIq2oYEo3m.print.svg?v=1",
      "design_object": {},
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:28:44.000000Z",
      "href": "/v3/orders/323/packages/570/plates/1107"
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
      "price": 200,
      "qty": 1,
      "created_at": "2025-04-20T15:28:06.000000Z",
      "updated_at": "2025-04-20T15:28:15.000000Z",
      "href": "/v3/orders/323/products/608"
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
      "price": 500,
      "qty": 1,
      "created_at": "2025-04-20T15:27:27.000000Z",
      "updated_at": "2025-04-20T15:27:57.000000Z",
      "href": "/v3/orders/323/products/607"
    }
  ],
  "notes": [],
  "ship_to_override": null
}
```

<!-- tabs:end -->

## Webhook Authenticity

Plateit includes a digital signature in each webhook request to ensure authenticity. The signature, a hexadecimal string, is found in the incoming `Signature` header.

To verify a webhook's authenticity, use your company's secret key to generate a hash-based message authentication code (HMAC) and compare it to the signature.

The steps are:

* Create an HMAC using the secret key and the raw webhook request body.
* Compare the generated HMAC to the `Signature` header.
* If they match, the webhook is authentic and untampered.

Below is an example using server-side JavaScript. The process is broadly the same for all programming languages.

```javascript
// Import dependencies.

const express = require('express')
const crypto = require('crypto')

// Initiate app.

const app = express()

// Keep a copy of the raw request body for signature verification.

app.use(express.json({
  verify: (req, res, buf) => {
    req.rawBody = buf
  }
}))

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

Webhook attempts that time out or do not receive a 2XX response code will retry later.

Persistently failing webhooks will be removed from the send queue and the company will be notified by email and encouraged to fix the problem.