# Company Plate

`https://plateit-api.co.uk/v3/plates`

The plate object represents a plate the customer can buy. It references a [company plate type](/objects/company-plate-type.md) and a [system plate size](/objects/system-plate-size.md).

>Plates can be delegated to another company to fulfil at the [company plate type](/objects/company-plate-type.md) level. However, the delegatee may not have every plate size you have configured in stock. Problems can be avoided by passing the `exclude_unmatched_delegations=true` query parameter when listing the available plates for the customer. This will filter out any delegated plates the delegatee cannot support. An example of this can be seen on the [suggested integration](/fundamentals/suggested-integration.md) page.

## Data References

### Attributes

* **id** `integer` The unique ID of the plate.
* **company_plate_type_id** `integer` The [company plate type](/objects/company-plate-type.md) ID.
* **system_plate_size_id** `integer` The [system plate size](/objects/system-plate-size.md) ID.
* **colour** `string` The main colour, spelt in English, of the plate (usually the colour of the reflective)backing.
* **price** `int` The price in pence.
* **is_front** `boolean` Is this plate for the front of a vehicle?
* **is_rear** `boolean` Is this plate for the rear of a vehicle?
* **is_legal** `boolean` Is this size/plate type combination legal for road use?
* **is_active** `boolean` Indicates whether the resource is live or a draft.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [company_plate_type](/objects/company-plate-type.md)
* [system_plate_size](/objects/system-plate-size.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* colour
* price
* is_front
* is_rear
* is_legal
* is_active
* created_at
* updated_at
* system_plate_size.width
* system_plate_size.height
* company_plate_type.id
* company_plate_type.name

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* colour
* is_front
* is_rear
* is_legal
* is_active *
* company_plate_type.id
* company_plate_type.name
* company_plate_type.is_printable
* company_plate_type.is_active *
* system_plate_size.width
* system_plate_size.height

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

**Plateit does not filter out inactive resources for you. It is your responsibility to honour what is shown publicly and what's not.*

## Example Requests

### Create a Plate

!> Requires the `company_plates_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **company_plate_type_id** `integer`
* **system_plate_size_id** `integer`
* **colour** `string`
* **price** `int`
* **is_front** `boolean`
* **is_rear** `boolean`
* **is_legal** `boolean`
* **is_active** `boolean`

#### **Request**

* Endpoint: `https://plateit-api.co.uk/v3/plates`
* Method: `POST`

```json
{
  "company_plate_type_id": 15,
  "system_plate_size_id": 1,
  "depth": 8,
  "colour": "yellow",
  "is_front": false,
  "is_rear": true,
  "is_active": true,
  "price": 1999,
  "is_legal": true
}
```

#### **Response**

* Status code: `201`

```json
{
  "id": 391,
  "system_plate_size_id": 1,
  "company_plate_type_id": 15,
  "colour": "yellow",
  "price": 1999,
  "is_front": false,
  "is_rear": true,
  "is_legal": true,
  "is_active": true,
  "created_at": "2024-09-30T09:56:35.000000Z",
  "updated_at": "2024-09-30T09:56:35.000000Z",
  "href": "/plates/391"
}
```

<!-- tabs:end -->

### Retrieve a Plate

!> Requires the `company_plates_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://plateit-api.co.uk/v3/plates/{plate_id}`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 391,
  "system_plate_size_id": 1,
  "company_plate_type_id": 15,
  "colour": "yellow",
  "price": 1999,
  "is_front": false,
  "is_rear": true,
  "is_legal": true,
  "is_active": true,
  "created_at": "2024-09-30T09:56:35.000000Z",
  "updated_at": "2024-09-30T09:56:35.000000Z",
  "href": "/plates/391"
}
```

<!-- tabs:end -->

### List Plates

!> Requires the `company_plates_read` permission.

> The following example includes relationships. 

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://plateit-api.co.uk/v3/plates`
* Method: `GET`
* Query:
  * with[]: `system_plate_size`
  * with[]: `company_plate_type`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 385,
      "system_plate_size_id": 1,
      "company_plate_type_id": 14,
      "colour": "white",
      "price": 1499,
      "is_front": true,
      "is_rear": false,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:53:40.000000Z",
      "updated_at": "2024-09-30T09:53:40.000000Z",
      "href": "/plates/385",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
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
      }
    },
    {
      "id": 386,
      "system_plate_size_id": 1,
      "company_plate_type_id": 14,
      "colour": "yellow",
      "price": 1499,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:54:13.000000Z",
      "updated_at": "2024-09-30T09:54:13.000000Z",
      "href": "/plates/386",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
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
      }
    },
    {
      "id": 387,
      "system_plate_size_id": 2,
      "company_plate_type_id": 14,
      "colour": "white",
      "price": 1499,
      "is_front": true,
      "is_rear": false,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:54:41.000000Z",
      "updated_at": "2024-09-30T09:54:41.000000Z",
      "href": "/plates/387",
      "system_plate_size": {
        "id": 2,
        "width": 279,
        "height": 203,
        "line_span": 2,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 40,
        "href": "/system-plate-sizes/2"
      },
      "company_plate_type": {
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
      }
    },
    {
      "id": 388,
      "system_plate_size_id": 2,
      "company_plate_type_id": 14,
      "colour": "yellow",
      "price": 1499,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:55:03.000000Z",
      "updated_at": "2024-09-30T09:55:03.000000Z",
      "href": "/plates/388",
      "system_plate_size": {
        "id": 2,
        "width": 279,
        "height": 203,
        "line_span": 2,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 40,
        "href": "/system-plate-sizes/2"
      },
      "company_plate_type": {
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
      }
    },
    {
      "id": 389,
      "system_plate_size_id": 3,
      "company_plate_type_id": 14,
      "colour": "yellow",
      "price": 1499,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:55:16.000000Z",
      "updated_at": "2024-09-30T09:55:16.000000Z",
      "href": "/plates/389",
      "system_plate_size": {
        "id": 3,
        "width": 229,
        "height": 178,
        "line_span": 2,
        "vehicle": "motorcycle",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 30,
        "href": "/system-plate-sizes/3"
      },
      "company_plate_type": {
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
      }
    },
    {
      "id": 390,
      "system_plate_size_id": 1,
      "company_plate_type_id": 15,
      "colour": "white",
      "price": 1999,
      "is_front": true,
      "is_rear": false,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:56:08.000000Z",
      "updated_at": "2024-09-30T09:56:08.000000Z",
      "href": "/plates/390",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
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
      }
    },
    {
      "id": 391,
      "system_plate_size_id": 1,
      "company_plate_type_id": 15,
      "colour": "yellow",
      "price": 1999,
      "is_front": false,
      "is_rear": true,
      "is_legal": true,
      "is_active": true,
      "created_at": "2024-09-30T09:56:35.000000Z",
      "updated_at": "2024-09-30T09:56:35.000000Z",
      "href": "/plates/391",
      "system_plate_size": {
        "id": 1,
        "width": 520,
        "height": 111,
        "line_span": 1,
        "vehicle": "car",
        "category": "standard",
        "is_legal": true,
        "suggested_side_badge_width": 45,
        "href": "/system-plate-sizes/1"
      },
      "company_plate_type": {
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
      }
    }
  ]
}
```

<!-- tabs:end -->

### Update a Plate

!> Requires the `company_plates_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **company_plate_type_id** `integer|null`
* **system_plate_size_id** `integer|null`
* **colour** `string|null`
* **price** `int|null`
* **is_front** `boolean|null`
* **is_rear** `boolean|null`
* **is_legal** `boolean|null`
* **is_active** `boolean|null`

#### **Request**

* Endpoint: `https://plateit-api.co.uk/v3/plates/{plate_id}`
* Method: `PATCH`

```json
{
  "price": 2400
}
```

#### **Response**

* Status code: `200`

```json
{
  "id": 391,
  "system_plate_size_id": 1,
  "company_plate_type_id": 15,
  "colour": "yellow",
  "price": 2400,
  "is_front": false,
  "is_rear": true,
  "is_legal": true,
  "is_active": true,
  "created_at": "2024-09-30T09:56:35.000000Z",
  "updated_at": "2024-09-30T10:09:42.000000Z",
  "href": "/plates/391"
}
```

<!-- tabs:end -->

### Delete a Plate

!> Requires the `company_plates_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://plateit-api.co.uk/v3/plates/{plate_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->