# OrderPackageShipping

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/shipping`

> This is a singleton resource.

An [OrderPackage](/objects/order-package.md) can have a single shipping.

!> This page is a stub. To be continued...

## Data References

### Attributes

* **package_id** `integer` The [OrderPackage](/objects/order-package-plate.md) ID the shipping pertains to.
* **company_shipping_id** `integer` The [CompanyShippingOption](/objects/company-shipping-option.md) ID.
* **system_courier_service_id** `integer` The [SystemCourierService](/objects/system-courier-service.md) ID derived from the [CompanyShippingOption](/objects/company-shipping-option.md).
* **name** `string` The name of the shipping option derived from the [CompanyShippingOption](/objects/company-shipping-option.md).
* **additional_options** `array|null` Array of courier-specific additional postage options. For example `['SIG']` for signature required.
* **price** `integer` The price in pence minus VAT.
* **price_vat** `integer` The VAT in pence.
* **price_gross** `integer` The total price in pence including VAT.
* **external_shipment_id** `string|null` The shipment ID provided by the courier after calling the [CreateOrderPackageShipmentLabel](/helpers/create-order-package-shipment-label.md) helper.
* **label_files** `array|null` Array of filepaths to PNG shipping labels provided by the courier.
* **tracking_code** `string|null` The tracking code provided by the courier.
* **delivery_instructions** `string|null` Additional delivery instructions from customer.
* **despatched_at** `string|null` The despatch timestamp in ISO 8601 format.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [package](/objects/order-package.md)
* [company_shipping](/objects/company-shipping.md)
* [system_courier_service](/objects/system-courier-service.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*