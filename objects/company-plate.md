# CompanyPlate

`https://api.plateit.co.uk/v3/plates`

A `CompanyPlate` represents a plate configuration that a customer can purchase. It references a [CompanyPlateType](/objects/company-plate-type.md) and a [SystemPlateSize](/objects/system-plate-size.md).

> A CompanyPlate can be delegated to another company to fulfil at the [CompanyPlateType](/objects/company-plate-type.md) level. However, the delegatee may not have every plate size you have configured for that type in stock. Problems can be avoided by passing the `exclude_unmatched_delegations=true` query parameter when listing the available plates for the customer. This will filter out any delegated CompanyPlate objects the delegatee cannot support. An example of this can be seen on the [suggested integration](/fundamentals/suggested-integration.md) page.

## Data References

### Attributes

* **id** `integer` The unique ID of the plate.
* **company_plate_type_id** `integer` The ID of the associated [CompanyPlateType](/objects/company-plate-type.md).
* **system_plate_size_id** `integer` The ID of the associated [SystemPlateSize](/objects/system-plate-size.md).
* **colour** `string` The primary colour of the plate, normally the colour of the reflective backing.
* **price** `integer` The price in pence, including [VAT](/objects/company-tax-rate.md).
* **is_front** `boolean` Indicates whether the plate is intended for the front of a vehicle.
* **is_rear** `boolean` Indicates whether the plate is intended for the rear of a vehicle.
* **is_legal** `boolean` Indicates whether the plate type and size combination is legal for road use.
* **is_active** `boolean` Indicates whether the plate is currently active.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [system_plate_size](/objects/system-plate-size.md)
* [company_plate_type](/objects/company-plate-type.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/plates/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

> Plateit does not automatically exclude inactive resources. API consumers are responsible for deciding which resources should be shown publicly.

## Create

!> Requires the `company_plates_write` permission.

**POST** `/v3/plates`

### Body Parameters

* **company_plate_type_id** `integer`
* **system_plate_size_id** `integer`
* **colour** `string`
* **price** `integer`
* **is_front** `boolean`
* **is_rear** `boolean`
* **is_legal** `boolean`
* **is_active** `boolean`

### Example Payload

```json
{
  "company_plate_type_id": 15,
  "system_plate_size_id": 1,
  "colour": "yellow",
  "price": 1999,
  "is_front": false,
  "is_rear": true,
  "is_legal": true,
  "is_active": true
}
```

Returns the created `CompanyPlate` with status `201`.

## Retrieve

!> Requires the `company_plates_read` permission.

**GET** `/v3/plates/{plate_id}`

Returns the requested `CompanyPlate`.

## List

!> Requires the `company_plates_read` permission.

**GET** `/v3/plates`

Returns a paginated collection of `CompanyPlate` resources.

## Update

!> Requires the `company_plates_write` permission.

**PATCH** `/v3/plates/{plate_id}`

### Body Parameters

All fields are optional:

* **company_plate_type_id** `integer`
* **system_plate_size_id** `integer`
* **colour** `string`
* **price** `integer`
* **is_front** `boolean`
* **is_rear** `boolean`
* **is_legal** `boolean`
* **is_active** `boolean`

### Example Payload

```json
{
  "price": 2400
}
```

Returns the updated `CompanyPlate`.

## Delete

!> Requires the `company_plates_write` permission.

**DELETE** `/v3/plates/{plate_id}`

Deletes the specified `CompanyPlate`.
