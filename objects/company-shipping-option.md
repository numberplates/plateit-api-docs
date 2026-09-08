# CompanyShippingOption

`https://api.plateit.co.uk/v3/shipping-options`

A `CompanyShippingOption` represents a shipping option that a customer can choose. It references a [SystemCourierService](/objects/system-courier-service.md).

## Data References

### Attributes

* **id** `integer` The unique ID of the shipping option.
* **system_courier_service_id** `integer` The ID of the associated [SystemCourierService](/objects/system-courier-service.md).
* **name** `string` The name of the shipping option.
* **price** `integer` The price in pence including [VAT](/objects/company-tax-rate.md).
* **is_active** `boolean` Indicates whether the shipping option is currently active.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [system_courier_service](/objects/system-courier-service.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/shipping-options/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

> Plateit does not automatically exclude inactive resources. API consumers are responsible for deciding which resources should be shown publicly.

## Create

!> Requires the `company_shipping_options_write` permission.

**POST** `/v3/shipping-options`

### Body Parameters

* **name** `string`
* **system_courier_service_id** `integer`
* **price** `integer`
* **is_active** `boolean`

### Example Payload

```json
{
  "system_courier_service_id": 5,
  "name": "Special Delivery",
  "price": 999,
  "is_active": true
}
```

Returns the created `CompanyShippingOption` with status `201`.

## Retrieve

!> Requires the `company_shipping_options_read` permission.

**GET** `/v3/shipping-options/{shipping_id}`

Returns the requested `CompanyShippingOption`.

## List

!> Requires the `company_shipping_options_read` permission.

**GET** `/v3/shipping-options`

Returns a paginated collection of `CompanyShippingOption` resources.

## Update

!> Requires the `company_shipping_options_write` permission.

**PATCH** `/v3/shipping-options/{shipping_id}`

### Body Parameters

All fields are optional when updating this resource type.

* **name** `string`
* **system_courier_service_id** `integer`
* **price** `integer`
* **is_active** `boolean`

### Example Payload

```json
{
  "is_active": false
}
```

Returns the updated `CompanyShippingOption`.

## Delete

!> Requires the `company_shipping_options_write` permission.

**DELETE** `/v3/shipping-options/{shipping_id}`

Deletes the specified `CompanyShippingOption`.
