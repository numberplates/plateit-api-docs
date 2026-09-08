# OrderPackageShipping

`https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/shipping`

> This is a singleton resource.

An [OrderPackage](/objects/order-package.md) can have a single `OrderPackageShipping` resource representing the shipping option assigned to that package.

## Data References

### Attributes

* **package_id** `integer` The ID of the [OrderPackage](/objects/order-package.md) the shipping resource belongs to.
* **system_courier_service_id** `integer` The ID of the [SystemCourierService](/objects/system-courier-service.md) derived from the selected [CompanyShippingOption](/objects/company-shipping-option.md).
* **company_shipping_id** `integer` The ID of the selected [CompanyShippingOption](/objects/company-shipping-option.md).
* **name** `string` The shipping option name derived from the selected `CompanyShippingOption`.
* **price** `integer` The gross shipping price in pence, including VAT.
* **price_vat** `integer` The included VAT amount in pence.
* **external_shipment_id** `string|null` The shipment ID provided by the courier after calling the [CreateOrderPackageShipmentLabel](/helpers/create-order-package-shipment-label.md) helper.
* **label_files** `array` An array of paths to generated shipping label files.
* **tracking_code** `string|null` The shipment tracking code.
* **delivery_instructions** `string|null` Additional delivery instructions supplied by the customer.
* **despatched_at** `string|null` The despatch timestamp in ISO 8601 format.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [company_shipping](/objects/company-shipping-option.md)
* [system_courier_service](/objects/system-courier-service.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Create

!> Requires the `orders_packages_shipping_write` permission.

**POST** `/v3/orders/{order_id}/packages/{package_id}/shipping`

Creates the shipping resource for the package.

### Body Parameters

* **company_shipping_id** `integer` The [CompanyShippingOption](/objects/company-shipping-option.md) to use.
* **tracking_code** `string|null` Optional tracking code.
* **delivery_instructions** `string|null` Optional delivery instructions.
* **price** `integer|null` Optional custom gross price in pence.

### Example Payload

```json
{
  "company_shipping_id": 1,
  "delivery_instructions": "Leave with neighbour if unavailable."
}
```

Returns the created `OrderPackageShipping` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}/shipping`

Returns the package's `OrderPackageShipping`.

## Update

!> Requires the `orders_packages_shipping_write` permission.

**PATCH** `/v3/orders/{order_id}/packages/{package_id}/shipping`

### Body Parameters

All fields are optional when updating this resource type.

* **company_shipping_id** `integer`
* **tracking_code** `string|null`
* **delivery_instructions** `string|null`
* **price** `integer|null`

### Example Payload

```json
{
  "tracking_code": "6a9a9f3f78774"
}
```

Returns the updated `OrderPackageShipping`.

## Delete

!> Requires the `orders_packages_shipping_write` permission.

**DELETE** `/v3/orders/{order_id}/packages/{package_id}/shipping`

Deletes the package's `OrderPackageShipping`.