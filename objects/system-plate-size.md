# SystemPlateSize

`https://data.plateit.co.uk/v3/system-plate-sizes`

!> Read only

System plate sizes consist of all supported number plate sizes. You do not have to support every size, but each [CompanyPlate](/objects/company-plate.md) references one of these resources.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/system-plate-sizes`
* Method: `GET`

#### **Response**

* Status code: `200`

> Note: the following results have been condensed for illustrative purposes.

```json
{
  "data": [
    {
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
    {
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
    {
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
    {
      "id": 4,
      "width": 520,
      "height": 121,
      "line_span": 1,
      "vehicle": "car",
      "category": "oversized",
      "is_legal": true,
      "suggested_side_badge_width": 45,
      "href": "/system-plate-sizes/4"
    },
    {
      "id": 5,
      "width": 520,
      "height": 127,
      "line_span": 1,
      "vehicle": "car",
      "category": "oversized",
      "is_legal": true,
      "suggested_side_badge_width": 45,
      "href": "/system-plate-sizes/5"
    },
    {
      "id": 6,
      "width": 520,
      "height": 140,
      "line_span": 1,
      "vehicle": "car",
      "category": "oversized",
      "is_legal": true,
      "suggested_side_badge_width": 45,
      "href": "/system-plate-sizes/6"
    },
    {
      "id": 7,
      "width": 520,
      "height": 152,
      "line_span": 1,
      "vehicle": "car",
      "category": "oversized",
      "is_legal": true,
      "suggested_side_badge_width": 45,
      "href": "/system-plate-sizes/7"
    },
    {
      "id": 8,
      "width": 520,
      "height": 165,
      "line_span": 1,
      "vehicle": "car",
      "category": "oversized",
      "is_legal": true,
      "suggested_side_badge_width": 45,
      "href": "/system-plate-sizes/8"
    },
    {
      "id": 9,
      "width": 533,
      "height": 152,
      "line_span": 1,
      "vehicle": "car",
      "category": "oversized",
      "is_legal": true,
      "suggested_side_badge_width": 45,
      "href": "/system-plate-sizes/9"
    },
    {
      "id": 10,
      "width": 559,
      "height": 152,
      "line_span": 1,
      "vehicle": "car",
      "category": "oversized",
      "is_legal": true,
      "suggested_side_badge_width": 50,
      "href": "/system-plate-sizes/10"
    }
  ]
}
```

<!-- tabs:end -->