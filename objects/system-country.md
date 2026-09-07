# SystemCountry

`https://api.plateit.co.uk/v3/system-countries`

!> Read only

A `SystemCountry` represents a supported country and its associated ISO and telephone dialling codes.

## Data References

### Attributes

* **id** `integer` The unique ID of the country.
* **iso_code** `string` The two-character ISO country code.
* **name** `string` The country name.
* **dialling_code** `string` The international telephone dialling code.
* **href** `string` The path to the resource.

## Example Values

The following examples illustrate some of the supported countries:

```json
[
    {
      "id": 1,
      "iso_code": "AD",
      "name": "ANDORRA",
      "dialling_code": "376",
    },
    {
      "id": 2,
      "iso_code": "AE",
      "name": "UNITED ARAB EMIRATES",
      "dialling_code": "971"
    },
    {
      "id": 3,
      "iso_code": "AF",
      "name": "AFGHANISTAN",
      "dialling_code": "93"
    }
]
```

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-countries/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-countries`

Returns a collection of `SystemCountry` resources.
