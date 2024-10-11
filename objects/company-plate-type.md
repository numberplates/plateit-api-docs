# Company Plate Type

`https://data.plateit.co.uk/v3/plate-types`

Any plate type you can think of can be catered for, as long as you can provide an appropriate print file for it.

> Plate types can be delegated to other companies to fulfil on your behalf. However, the delegated company must have a plate type with an *identical* `reference` for this relationship to be recognised. The dimensions and weight will be inherited from their settings and not yours.

## Data References

### Attributes

* **id** `integer` The unique ID of the plate type.
* **name** `string` The name of the plate type.
* **reference** `string` The plate type's unique reference code.
* **depth** `integer` The depth in mm of the plate type including any 3D letters (for shipping calculations).
* **weight_std_oblong** `integer` The weight of a standard oblong in grams (for shipping calculations).
* **is_printable** `boolean` Set to `false` for any plate type that doesn't require printing. For example, pressed plates.
* **is_active** `boolean` Indicates whether the resource is live or a draft.
* **delegate_to_company_id** `integer|null` The [company](/objects/company.md) ID to delegate the plate type to fulfil.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [delegate_to_company](/objects/company.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* name
* is_printable
* is_active
* created_at
* updated_at

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* name
* is_printable
* is_active *

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

**Plateit does not filter out inactive resources for you. It is your responsibility to honour what is shown publicly and what's not.*

## Example Requests

### Create a Plate Type

!> Requires the `company_plate_types_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **name** `string`
* **reference** `string`
* **depth** `integer`
* **weight_std_oblong** `integer`
* **is_printable** `boolean`
* **is_active** `boolean`
* **delegate_to_company_id** `integer|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/plate-types`
* Method: `POST`

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

#### **Response**

* Status code: `201`

```json
{
  "id": 16,
  "name": "Pressed Metal Black",
  "reference": "pressedmetalblack",
  "depth": 4,
  "weight_std_oblong": 220,
  "is_printable": false,
  "is_active": true,
  "delegate_to_company_id": null,
  "created_at": "2024-09-30T09:05:11.000000Z",
  "updated_at": "2024-09-30T09:05:11.000000Z",
  "href": "/plate-types/16"
}
```

<!-- tabs:end -->

### Retrieve a Plate Type

!> Requires the `company_plate_types_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/plate-types/{plate_type_id}`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 16,
  "name": "Pressed Metal Black",
  "reference": "pressedmetalblack",
  "depth": 4,
  "weight_std_oblong": 220,
  "is_printable": false,
  "is_active": true,
  "delegate_to_company_id": null,
  "created_at": "2024-09-30T09:05:11.000000Z",
  "updated_at": "2024-09-30T09:05:11.000000Z",
  "href": "/plate-types/16"
}
```

<!-- tabs:end -->

### List Plate Types

!> Requires the `company_plate_types_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/plate-types`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
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
    },
    {
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
    },
    {
      "id": 16,
      "name": "Pressed Metal Black",
      "reference": "pressedmetalblack",
      "depth": 4,
      "weight_std_oblong": 220,
      "is_printable": false,
      "is_active": true,
      "delegate_to_company_id": null,
      "created_at": "2024-09-30T09:05:11.000000Z",
      "updated_at": "2024-09-30T09:05:11.000000Z",
      "href": "/plate-types/16"
    }
  ]
}
```

<!-- tabs:end -->

### Update a Plate Type

!> Requires the `company_plate_types_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **name** `string|null`
* **reference** `string|null`
* **depth** `integer|null`
* **weight_std_oblong** `integer|null`
* **is_printable** `boolean|null`
* **is_active** `boolean|null`
* **delegate_to_company_id** `integer|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/plate-types/{plate_type_id}`
* Method: `PATCH`

```json
{
  "name": "Pressed Metal Black (Updated Name)",
}
```

#### **Response**

* Status code: `200`

```json
{
  "id": 16,
  "name": "Pressed Metal Black (Updated Name)",
  "reference": "pressedmetalblack",
  "depth": 4,
  "weight_std_oblong": 220,
  "is_printable": false,
  "is_active": true,
  "delegate_to_company_id": null,
  "created_at": "2024-09-30T09:05:11.000000Z",
  "updated_at": "2024-09-30T09:06:01.000000Z",
  "href": "/plate-types/16"
}
```

<!-- tabs:end -->

### Delete a Plate Type

!> Requires the `company_plate_types_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/plate-types/{plate_type_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->