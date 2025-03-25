# SystemPackageStatus

`https://data.plateit.co.uk/v3/system-package-statuses`

!> Read only

Each [OrderPackage](/objects/order-package.md) has an associated SystemPackageStatus. It is used to categorise and filter the packages.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/system-package-statuses`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "name": "Unprocessed",
      "description": "The contents of the package are waiting to be processed.",
      "href": "/system-package-statuses/1"
    },
    {
      "id": 2,
      "name": "Processing",
      "description": "The contents of the package are actively being processed.",
      "href": "/system-package-statuses/2"
    },
    {
      "id": 3,
      "name": "Processed",
      "description": "The contents of the package have been processed.",
      "href": "/system-package-statuses/3"
    },
    {
      "id": 4,
      "name": "Held",
      "description": "The package is in a held state, awaiting further action.",
      "href": "/system-package-statuses/4"
    },
    {
      "id": 5,
      "name": "Cancelled",
      "description": "The fulfillment of the package has been cancelled.",
      "href": "/system-package-statuses/5"
    }
  ]
}
```

<!-- tabs:end -->