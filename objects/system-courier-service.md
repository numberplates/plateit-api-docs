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
      "service_reference": "n/a",
      "additional_options": [],
      "is_international": false,
      "max_width": 1000000,
      "max_height": 1000000,
      "max_depth": 1000000,
      "max_weight": 1000000,
      "position": 1,
      "is_active": 1,
      "href": "/system-courier-services/1"
    },
    {
      "id": 2,
      "courier_key": "manual",
      "name": "Manual Post",
      "priority_level": 3,
      "service_reference": "n/a",
      "additional_options": [],
      "is_international": false,
      "max_width": 1000000,
      "max_height": 1000000,
      "max_depth": 1000000,
      "max_weight": 1000000,
      "position": 2,
      "is_active": 1,
      "href": "/system-courier-services/2"
    },
    {
      "id": 3,
      "courier_key": "jersey_post",
      "name": "Jersey Post / Royal Mail 1st Class",
      "priority_level": 2,
      "service_reference": "RM|FIRST",
      "additional_options": [],
      "is_international": false,
      "max_width": 610,
      "max_height": 460,
      "max_depth": 460,
      "max_weight": 20000,
      "position": 3,
      "is_active": 1,
      "href": "/system-courier-services/3"
    },
    {
      "id": 4,
      "courier_key": "jersey_post",
      "name": "Jersey Post / Royal Mail 1st Class Signed",
      "priority_level": 2,
      "service_reference": "RM|FIRSTSIGNED",
      "additional_options": [],
      "is_international": false,
      "max_width": 610,
      "max_height": 460,
      "max_depth": 460,
      "max_weight": 20000,
      "position": 4,
      "is_active": 1,
      "href": "/system-courier-services/4"
    },
    {
      "id": 5,
      "courier_key": "jersey_post",
      "name": "Jersey Post / Royal Mail Special Delivery",
      "priority_level": 1,
      "service_reference": "RM|SPECIALPM",
      "additional_options": [],
      "is_international": false,
      "max_width": 610,
      "max_height": 460,
      "max_depth": 460,
      "max_weight": 20000,
      "position": 5,
      "is_active": 1,
      "href": "/system-courier-services/5"
    },
    {
      "id": 6,
      "courier_key": "jersey_post",
      "name": "Jersey Post / International UPU",
      "priority_level": 2,
      "service_reference": "UPU|TRACKED",
      "additional_options": [
        "SIG"
      ],
      "is_international": true,
      "max_width": 610,
      "max_height": 460,
      "max_depth": 460,
      "max_weight": 20000,
      "position": 6,
      "is_active": 1,
      "href": "/system-courier-services/6"
    },
    {
      "id": 7,
      "courier_key": "jersey_post",
      "name": "Jersey Post / International UPU Express",
      "priority_level": 2,
      "service_reference": "UPU|EMS",
      "additional_options": [],
      "is_international": true,
      "max_width": 610,
      "max_height": 460,
      "max_depth": 460,
      "max_weight": 20000,
      "position": 7,
      "is_active": 1,
      "href": "/system-courier-services/7"
    },
    {
      "id": 8,
      "courier_key": "hub_europe",
      "name": "Hub Europe / Evri",
      "priority_level": 2,
      "service_reference": "HermesCorporate|Hermes 24 POD",
      "additional_options": [],
      "is_international": false,
      "max_width": 1200,
      "max_height": 620,
      "max_depth": 620,
      "max_weight": 15000,
      "position": 8,
      "is_active": 1,
      "href": "/system-courier-services/8"
    }
  ]
}
```

<!-- tabs:end -->