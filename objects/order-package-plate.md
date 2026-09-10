# OrderPackagePlate

`https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/plates`

An [OrderPackage](/objects/order-package.md) can have many plates. Think of them as individual line items on an invoice.

Many of the plate's physical and pricing attributes are copied from the selected [CompanyPlate](/objects/company-plate.md) when the line item is created.

> Plates belonging to a specific package can be retrieved from this endpoint. To retrieve plates across all packages, use `GET /v3/packages`.

## Data References

### Attributes

* **id** `integer` The unique ID of the plate line item.
* **package_id** `integer` The ID of the [OrderPackage](/objects/order-package.md) the plate belongs to.
* **company_plate_id** `integer` The ID of the selected [CompanyPlate](/objects/company-plate.md).
* **company_plate_id_delegated** `integer|null` The ID of the matching [CompanyPlate](/objects/company-plate.md) belonging to the delegated fulfilment company, if applicable.
* **registration** `string` The vehicle registration displayed on the plate.
* **type** `string` The plate type name derived from the selected `CompanyPlate`.
* **shape** `string|null` The plate shape, where applicable.
* **colour** `string` The plate colour derived from the selected `CompanyPlate`.
* **width** `integer` The plate width in mm.
* **height** `integer` The plate height in mm.
* **depth** `integer` The plate depth in mm.
* **weight** `integer` The plate weight in grams.
* **price** `integer` The gross price in pence.
* **qty** `integer` The quantity of this plate being sold.
* **is_printable** `boolean` Indicates whether the plate requires printing.
* **is_printed** `boolean` Indicates whether the plate has been printed.
* **requires_docs** `boolean` Indicates whether supporting identity and entitlement documents are required for this plate.
* **custom_instructions** `string|null` Bespoke design or manufacturing instructions supplied for the plate.
* **design_preview** `string` Path to the SVG preview file when retrieving the resource, or an SVG string when creating or updating it.
* **design_print** `string` Path to the SVG print file when retrieving the resource, or an SVG string when creating or updating it.
* **design_object** `object|null` Optional structured design data that can be retained for future editing. See [Editing Existing Plate Designs](/fundamentals/editing-existing-plate-designs.md).
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

> When `requires_docs` is `true`, the registration must represent a valid road registration and the order will require the relevant supporting documentation before it can become ready for fulfilment. See the [Supporting Documents](/fundamentals/documents.md) guide.

## Relationships

The following relationships may be included:

* [company_plate](/objects/company-plate.md)
* [company_plate.system_plate_size](/objects/system-plate-size.md)
* [company_plate.company_plate_type](/objects/company-plate-type.md)
* [package](/objects/order-package.md)
* [package.order](/objects/order.md)
* [package.system_package_status](/objects/system-package-status.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/{order_id}/packages/{package_id}/plates/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## Create

!> Requires the `orders_packages_plates_write` permission.

**POST** `/v3/orders/{order_id}/packages/{package_id}/plates`

Creates a new plate line item within the package.

### Body Parameters

* **company_plate_id** `integer` The [CompanyPlate](/objects/company-plate.md) to use.
* **registration** `string` The registration to display on the plate.
* **requires_docs** `boolean` Optional. Defaults to `true`.
* **price** `integer|null` Optional custom gross price in pence.
* **qty** `integer` The quantity being ordered.
* **is_printed** `boolean` Optional.
* **custom_instructions** `string|null` Optional bespoke design or manufacturing instructions.
* **design_print** `string|null` SVG string containing the print design.
* **design_preview** `string|null` Optional SVG string containing the preview design.
* **design_object** `object|null` Optional structured design metadata used for future editing.

> If `design_preview` is supplied, `design_print` must also be supplied.

> When `requires_docs` is `true`, the registration must be a valid road registration. When `requires_docs` is `false`, arbitrary registration text may be used.

### Example Payload

```json
{
  "company_plate_id": 53,
  "registration": "AB12 CDE",
  "requires_docs": true,
  "qty": 1,
  "design_print": "<svg>...</svg>",
  "design_preview": "<svg>...</svg>"
}
```

Returns the created `OrderPackagePlate` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}/plates/{plate_id}`

Returns the requested `OrderPackagePlate`.

> When retrieving the resource, `design_print` and `design_preview` contain paths to the stored SVG assets rather than the original SVG strings supplied when creating or updating the plate.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/packages/{package_id}/plates`

Returns a collection of `OrderPackagePlate` resources belonging to the specified package.

## Update

!> Requires the `orders_packages_plates_write` permission.

**PATCH** `/v3/orders/{order_id}/packages/{package_id}/plates/{plate_id}`

Updates the specified `OrderPackagePlate`.

### Body Parameters

All fields are optional when updating this resource type.

* **company_plate_id** `integer`
* **registration** `string`
* **requires_docs** `boolean`
* **price** `integer|null`
* **qty** `integer`
* **is_printed** `boolean`
* **custom_instructions** `string|null`
* **design_print** `string` SVG string containing the updated print design.
* **design_preview** `string|null` SVG string containing the updated preview design.
* **design_object** `object|null`

> If `design_preview` is supplied, `design_print` must also be supplied.

### Example Payload

```json
{
  "registration": "XY24 ABC",
  "design_print": "<svg>...</svg>",
  "design_preview": "<svg>...</svg>"
}
```

Returns the updated `OrderPackagePlate`.

## Delete

!> Requires the `orders_packages_plates_write` permission.

**DELETE** `/v3/orders/{order_id}/packages/{package_id}/plates/{plate_id}`

Deletes the specified `OrderPackagePlate`.
