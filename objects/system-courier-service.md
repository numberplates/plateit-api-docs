# SystemCourierService

`https://api.plateit.co.uk/v3/system-courier-services`

!> Read only

A `SystemCourierService` represents a supported courier service. Each [CompanyShippingOption](/objects/company-shipping-option.md) references one of these resources.

## Data References

### Attributes

* **id** `integer` The unique ID of the courier service.
* **courier_key** `string` The service-provider's identifier, for example "parcelhub".
* **name** `string` The name of the delivery service, for example "Royal Mail 24".
* **priority_level** `integer` A number between 1 (fast service) and 3 (slow service).
* **is_international** `boolean` Indicates whether the service is intended for international shipping.
* **is_active** `boolean` Indicates whether the courier service is currently active.
* **href** `string` The path to the resource.

## Example Values

The following examples illustrate some of the supported services:

```json
[
    {
      "id": 1,
      "courier_key": "manual",
      "name": "Manual Collection",
      "priority_level": 3,
      "is_international": false,
      "is_active": true
},
    {
      "id": 2,
      "courier_key": "manual",
      "name": "Manual Post",
      "priority_level": 3,
      "is_international": false,
      "is_active": true
    },
    {
      "id": 3,
      "courier_key": "atlas",
      "name": "Atlas / Royal Mail 1st Class",
      "priority_level": 2,
      "is_international": false,
      "is_active": true
    }
]
```

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-courier-services/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-courier-services`

Returns a collection of `SystemCourierService` resources.
