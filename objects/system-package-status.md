# System Package Status

`https://plateit-api.co.uk/v3/system-package-statuses`

!> Read only

Each [package](/objects/order-package.md) has an associated system package status. It is used to categorise and filter the packages.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://plateit-api.co.uk/v3/system-package-statuses`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "name": "Unprocessed",
      "description": "The contents of the package are awaiting manufacture.",
      "href": "/system-package-statuses/1"
    },
    {
      "id": 2,
      "name": "Processing",
      "description": "The contents of the package are in the manufacture queue.",
      "href": "/system-package-statuses/2"
    },
    {
      "id": 3,
      "name": "Processed",
      "description": "The contents of the package have been printed and/or picked.",
      "href": "/system-package-statuses/3"
    },
    {
      "id": 4,
      "name": "Held",
      "description": "The package has been placed on hold.",
      "href": "/system-package-statuses/4"
    }
  ]
}
```

<!-- tabs:end -->