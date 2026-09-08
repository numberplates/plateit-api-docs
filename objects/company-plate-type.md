# CompanyPlateType

`https://api.plateit.co.uk/v3/plate-types`

A `CompanyPlateType` represents a type or style of number plate that your company can supply.

> A CompanyPlateType can be delegated to another company to fulfil on your behalf. However, the delegated company must have a CompanyPlateType with an *identical* `reference` for this relationship to be recognised. The dimensions and weight used for fulfilment will be inherited from the delegatee's settings rather than your own. See the [delegation guide](/fundamentals/delegations.md) for more information.

## Data References

### Attributes

* **id** `integer` The unique ID of the plate type.
* **name** `string` The name of the plate type.
* **reference** `string` The plate type's unique reference code.
* **depth** `integer` The depth in mm of the plate type, including any 3D lettering. Used for shipping calculations.
* **weight_std_oblong** `integer` The weight in grams of a standard oblong plate. Used for shipping calculations.
* **is_printable** `boolean` Indicates whether the plate type requires printing. Set to `false` for plate types such as pressed plates.
* **is_active** `boolean` Indicates whether the plate type is currently active.
* **delegate_to_company_id** `integer|null` The ID of the [Company](/objects/company.md) delegated to fulfil the plate type, if applicable.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [delegate_to_company](/objects/company.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/plate-types/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

> Plateit does not automatically exclude inactive resources. API consumers are responsible for deciding which resources should be shown publicly.

## Create

!> Requires the `company_plate_types_write` permission.

**POST** `/v3/plate-types`

### Body Parameters

* **name** `string`
* **reference** `string`
* **depth** `integer`
* **weight_std_oblong** `integer`
* **is_printable** `boolean`
* **is_active** `boolean`
* **delegate_to_company_id** `integer|null`

### Example Payload

```json
{
  "name": "Pressed Metal Black",
  "reference": "pressedmetalblack",
  "depth": 4,
  "weight_std_oblong": 220,
  "is_printable": false,
  "is_active": true
}
```

Returns the created `CompanyPlateType` with status `201`.

## Retrieve

!> Requires the `company_plate_types_read` permission.

**GET** `/v3/plate-types/{plate_type_id}`

Returns the requested `CompanyPlateType`.

## List

!> Requires the `company_plate_types_read` permission.

**GET** `/v3/plate-types`

Returns a paginated collection of `CompanyPlateType` resources.

## Update

!> Requires the `company_plate_types_write` permission.

**PATCH** `/v3/plate-types/{plate_type_id}`

### Body Parameters

All fields are optional when updating this resource type.

* **name** `string`
* **reference** `string`
* **depth** `integer`
* **weight_std_oblong** `integer`
* **is_printable** `boolean`
* **is_active** `boolean`
* **delegate_to_company_id** `integer|null`

### Example Payload

```json
{
  "name": "Pressed Metal Black (Updated Name)"
}
```

Returns the updated `CompanyPlateType`.

## Delete

!> Requires the `company_plate_types_write` permission.

**DELETE** `/v3/plate-types/{plate_type_id}`

Deletes the specified `CompanyPlateType`.
