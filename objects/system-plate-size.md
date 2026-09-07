# SystemPlateSize

`https://api.plateit.co.uk/v3/system-plate-sizes`

!> Read only

A `SystemPlateSize` represents a supported number plate size. Your company does not need to support every available size, but each [CompanyPlate](/objects/company-plate.md) references one of these resources.

## Data References

### Attributes

* **id** `integer` The unique ID of the plate size.
* **width** `integer` The plate width in mm.
* **height** `integer` The plate height in mm.
* **line_span** `integer` The number of registration lines the plate supports.
* **vehicle** `string` The vehicle type the plate size is intended for.
* **category** `string` The plate size category.
* **is_legal** `boolean` Indicates whether the plate size is legal for road use.
* **suggested_side_badge_width** `integer` The suggested side badge width in mm.
* **href** `string` The path to the resource.

## Example Values

The following examples illustrate some of the supported plate sizes:

```json
[
  {
    "id": 1,
    "width": 520,
    "height": 111,
    "line_span": 1,
    "vehicle": "car",
    "category": "standard",
    "is_legal": true,
    "suggested_side_badge_width": 45
  },
  {
    "id": 2,
    "width": 279,
    "height": 203,
    "line_span": 2,
    "vehicle": "car",
    "category": "standard",
    "is_legal": true,
    "suggested_side_badge_width": 40
  },
  {
    "id": 3,
    "width": 229,
    "height": 178,
    "line_span": 2,
    "vehicle": "motorcycle",
    "category": "standard",
    "is_legal": true,
    "suggested_side_badge_width": 30
  }
]
```

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-plate-sizes/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-plate-sizes`

Returns a collection of `SystemPlateSize` resources.
