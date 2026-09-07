# Order

`https://api.plateit.co.uk/v3/orders`

An `Order` is the outermost parent resource representing a customer order. Most of its attributes are read-only and are recalculated automatically as its child resources change.

For example, totals may change when an [OrderPackagePlate](/objects/order-package-plate.md) or other package item is created or updated.

The order's lifecycle, document and fulfilment statuses are also managed automatically based on the state of the order and its related resources.

## Data References

### Attributes

* **id** `integer` The unique ID of the order.
* **company_id** `integer` The ID of the [Company](/objects/company.md) the order belongs to.
* **system_order_status_id** `integer` The [SystemOrderStatus](/objects/system-order-status.md) ID.
* **system_order_document_status_id** `integer` The [SystemOrderDocumentStatus](/objects/system-order-document-status.md) ID.
* **system_order_fulfilment_status_id** `integer` The [SystemOrderFulfilmentStatus](/objects/system-order-fulfilment-status.md) ID.
* **amount_subtotal** `integer` The sum of all items in pence, excluding shipping and VAT.
* **amount_shipping** `integer` The total shipping cost in pence.
* **amount_vat** `integer` The total VAT in pence.
* **amount_total** `integer` The order's grand total in pence.
* **amount_paid** `integer` The total amount paid in pence.
* **amount_refunded** `integer` The total amount refunded in pence.
* **amount_vat_collected** `integer` The amount of VAT collected in pence, proportionate to the amount paid.
* **amount_vat_refunded** `integer` The amount of VAT refunded in pence, proportionate to the amount refunded.
* **packages_count** `integer` The number of [OrderPackage](/objects/order-package.md) resources belonging to the order.
* **identifier** `string|null` An optional unique identifier that can be used to associate the order with another system.
* **opened_at** `string|null` The timestamp at which the order first became `Open`, in ISO 8601 format.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [system_order_status](/objects/system-order-status.md)
* [system_order_document_status](/objects/system-order-document-status.md)
* [system_order_fulfilment_status](/objects/system-order-fulfilment-status.md)
* [company](/objects/company.md)
* [customer](/objects/order-customer.md)
* [ship_to](/objects/order-ship-to.md)
* [bill_to](/objects/order-bill-to.md)
* [notes](/objects/order-note.md)
* [packages](/objects/order-package.md)
* [packages.system_package_status](/objects/system-package-status.md)
* [packages.delegate_to_company](/objects/company.md)
* [packages.plates](/objects/order-package-plate.md)
* [packages.products](/objects/order-package-product.md)
* [packages.shipping](/objects/order-package-shipping.md)
* [packages.notes](/objects/order-package-note.md)
* [packages.notes.company_user](/objects/company-user.md)
* [packages.ship_to_override](/objects/order-package-ship-to-override.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## Order Lifecycle

The order's lifecycle, fulfilment and document statuses are managed automatically and cannot be set directly by the API consumer after creation.

* **[system_order_status_id](/objects/system-order-status.md)** - Represents whether the order is in a draft, open or closed state.
* **[system_order_document_status_id](/objects/system-order-document-status.md)** - Represents the overall state of any required supporting documents associated with the order.
* **[system_order_fulfilment_status_id](/objects/system-order-fulfilment-status.md)** - Represents the fulfilment state of the order based on the despatch state of its packages.

> An order may be fully paid while still remaining in a draft state if required supporting documents are awaiting upload or approval.

## Create

!> Requires the `orders_write` permission.

> If you want to create an entire order in a single request, including its customer, packages, plates, products and shipping, consider using the [BuildOrder](/helpers/build-order.md) helper endpoint. This is generally better suited to customer-facing checkout integrations.

**POST** `/v3/orders`

### Body Parameters

* **system_order_status_id** `integer` Optional. May be used to create either an External Draft or Internal Draft order.

### Example Payload

```json
{}
```

Returns the created `Order` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}`

Returns the requested `Order`.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders`

Returns a paginated collection of `Order` resources.

## Update

An `Order` cannot be updated directly. Its values are managed automatically as its related resources change.

## Delete

!> Requires the `orders_write` permission.

**DELETE** `/v3/orders/{order_id}`

Deletes the specified `Order`.
