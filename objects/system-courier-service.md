# SystemCourierService

`https://api.plateit.co.uk/v3/system-courier-services`

!> Read only

All supported courier services. Each [CompanyShippingOption](/objects/company-shipping-option.md) references one of these resources.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/system-courier-services`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "courier_key": "manual",
      "name": "Manual Collection",
      "priority_level": 3,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/1"
    },
    {
      "id": 2,
      "courier_key": "manual",
      "name": "Manual Post",
      "priority_level": 3,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/2"
    },
    {
      "id": 3,
      "courier_key": "atlas",
      "name": "Atlas / Royal Mail 1st Class",
      "priority_level": 2,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/3"
    },
    {
      "id": 4,
      "courier_key": "atlas",
      "name": "Atlas / Royal Mail 1st Class Signed",
      "priority_level": 2,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/4"
    },
    {
      "id": 5,
      "courier_key": "atlas",
      "name": "Atlas / Royal Mail Special Delivery",
      "priority_level": 1,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/5"
    },
    {
      "id": 6,
      "courier_key": "atlas",
      "name": "Atlas / International UPU Tracked",
      "priority_level": 2,
      "is_international": true,
      "is_active": true,
      "href": "/system-courier-services/6"
    },
    {
      "id": 7,
      "courier_key": "atlas",
      "name": "Atlas / International UPU Express",
      "priority_level": 2,
      "is_international": true,
      "is_active": true,
      "href": "/system-courier-services/7"
    },
    {
      "id": 8,
      "courier_key": "hub_europe",
      "name": "Hub Europe / Evri 24",
      "priority_level": 1,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/8"
    },
    {
      "id": 9,
      "courier_key": "hub_europe",
      "name": "Hub Europe / Evri 24 POD",
      "priority_level": 1,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/9"
    },
    {
      "id": 10,
      "courier_key": "hub_europe",
      "name": "Hub Europe / Evri 48",
      "priority_level": 2,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/10"
    },
    {
      "id": 11,
      "courier_key": "hub_europe",
      "name": "Hub Europe / Evri 48 POD",
      "priority_level": 2,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/11"
    },
    {
      "id": 12,
      "courier_key": "parcelhub",
      "name": "Parcelhub / Royal Mail 24",
      "priority_level": 2,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/12"
    },
    {
      "id": 13,
      "courier_key": "parcelhub",
      "name": "Parcelhub / Royal Mail 24 POD",
      "priority_level": 2,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/13"
    },
    {
      "id": 14,
      "courier_key": "parcelhub",
      "name": "Parcelhub / Royal Mail 48",
      "priority_level": 3,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/14"
    },
    {
      "id": 15,
      "courier_key": "parcelhub",
      "name": "Parcelhub / Royal Mail 48 POD",
      "priority_level": 3,
      "is_international": false,
      "is_active": true,
      "href": "/system-courier-services/15"
    }
  ]
}
```

<!-- tabs:end -->