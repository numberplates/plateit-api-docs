# Conventions

This page outlines the core API conventions, including how to order and filter collections and include relationships.

## System vs Company Resources

"System" resources such as [SystemOrderStatus](/objects/system-order-status.md) or [SystemPlateSize](/objects/system-plate-size.md) are *read-only*. Consider them constants that provide a backbone to the application.

All other resources are company-specific. This means they are under your control and unique to the company they belong to. Examples include [CompanyPlate](/objects/company-plate.md) and [CompanyProduct](/objects/company-product.md) objects.

Some company resources will reference system resources.

## Collections

### Response Body

Here is a fictional example of a typical collection response. There will be an array of objects nested within the `data` key, and metadata nested within the `meta` key.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/people`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 123,
      "name": "John",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:11.000000Z",
      "updated_at": "2024-05-24T09:14:11.000000Z",
      "href": "/people/123"
    },
    {
      "id": 124,
      "name": "Charlotte",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:22.000000Z",
      "updated_at": "2024-05-24T09:14:22.000000Z",
      "href": "/people/124"
    },
    {
      "id": 125,
      "name": "Abigail",
      "eye_colour_id": 3,
      "is_active": false,
      "created_at": "2024-05-24T09:14:33.000000Z",
      "updated_at": "2024-05-24T09:14:33.000000Z",
      "href": "/people/125"
    }
  ],
  "links": {
    "first": "/people?page=1",
    "last": "/people?page=1",
    "prev": null,
    "next": null
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "/people?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": null,
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "/people",
    "per_page": 25,
    "to": 3,
    "total": 3
  }
}
```

<!-- tabs:end -->

### Results Per Page

By default, collections return 25 objects per page. This can be increased by passing the following query: `?per_page=75`. Most collection allow for up to 100 items per page but some allow for up to 1000.

### Ordering Results

Results can be ordered using query parameters. The available `order_by` keys can be found on each object type's documenation page.

In the fictional example below, the collection is being ordered by `name` in ascending order.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/people`
* Method: `GET`
* Query:
  * order_by: `name:asc`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 125,
      "name": "Abigail",
      "eye_colour_id": 3,
      "is_active": false,
      "created_at": "2024-05-24T09:14:33.000000Z",
      "updated_at": "2024-05-24T09:14:33.000000Z",
      "href": "/people/125"
    },
    {
      "id": 124,
      "name": "Charlotte",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:22.000000Z",
      "updated_at": "2024-05-24T09:14:22.000000Z",
      "href": "/people/124"
    },
    {
      "id": 123,
      "name": "John",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:11.000000Z",
      "updated_at": "2024-05-24T09:14:11.000000Z",
      "href": "/people/123"
    }
  ],
  "links": {
    "first": "/people?order_by=name%3Aasc&page=1",
    "last": "/people?order_by=name%3Aasc&page=1",
    "prev": null,
    "next": null
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "/people?order_by=name%3Aasc&page=1",
        "label": "1",
        "active": true
      },
      {
        "url": null,
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "/people",
    "per_page": 25,
    "to": 3,
    "total": 3
  }
}
```

<!-- tabs:end -->

### Filtering Results

Results can be filtered using query parameters. The available `filter_by` keys can be found on each object type's documenation page.

In the fictional example below, the collection is being refined to return all "active" people. Note the query parameters.

> You can filter by multiple critera by passing an array like so: `?filter_by=something:foo&filter_by[]=something_else:bar`

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/people`
* Method: `GET`
* Query:
  * filter_by: `is_active:true`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 124,
      "name": "Charlotte",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:22.000000Z",
      "updated_at": "2024-05-24T09:14:22.000000Z",
      "href": "/people/124"
    },
    {
      "id": 123,
      "name": "John",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:11.000000Z",
      "updated_at": "2024-05-24T09:14:11.000000Z",
      "href": "/people/123"
    }
  ],
  "links": {
    "first": "/people?filter_by=is_active%3Atrue&page=1",
    "last": "/people?filter_by=is_active%3Atrue&page=1",
    "prev": null,
    "next": null
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "/people?filter_by=is_active%3Atrue&page=1",
        "label": "1",
        "active": true
      },
      {
        "url": null,
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "/people",
    "per_page": 25,
    "to": 2,
    "total": 2
  }
}
```

<!-- tabs:end -->

!> Some resources have an `is_active` key to differentiate live resources from drafts. It is your responsibility to honour this and filter out inactive resources in your public-facing production environment.

### Including Relationships

An object's relationship/s can be included in the response body. The available relationships can be found on each object type's documenation page.

> Relationships can also be included when retrieving a single resource.

In the fictional example below, the person's `eye_colour` relationship is being included.

> Multiple relationships can be included by passing an array like so: `?with[]=foo&with[]=bar&with[]=bim`

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/people`
* Method: `GET`
* Query:
  * with: `eye_colour`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 123,
      "name": "John",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:11.000000Z",
      "updated_at": "2024-05-24T09:14:11.000000Z",
      "href": "/people/123",
      "eye_colour": {
        "id": 1,
        "colour": "Blue",
        "href": "/eye-colours/1"
      }
    },
    {
      "id": 124,
      "name": "Charlotte",
      "eye_colour_id": 1,
      "is_active": true,
      "created_at": "2024-05-24T09:14:22.000000Z",
      "updated_at": "2024-05-24T09:14:22.000000Z",
      "href": "/people/124",
      "eye_colour": {
        "id": 1,
        "colour": "Blue",
        "href": "/eye-colours/1"
      }
    },
    {
      "id": 125,
      "name": "Abigail",
      "eye_colour_id": 3,
      "is_active": false,
      "created_at": "2024-05-24T09:14:33.000000Z",
      "updated_at": "2024-05-24T09:14:33.000000Z",
      "href": "/people/125",
      "eye_colour": {
        "id": 3,
        "colour": "Green",
        "href": "/eye-colours/3"
      }
    }
  ],
  "links": {
    "first": "/people?with=eye_colour&page=1",
    "last": "/people?with=eye_colour&page=1",
    "prev": null,
    "next": null
  },
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "links": [
      {
        "url": null,
        "label": "&laquo; Previous",
        "active": false
      },
      {
        "url": "/people?with=eye_colour&page=1",
        "label": "1",
        "active": true
      },
      {
        "url": null,
        "label": "Next &raquo;",
        "active": false
      }
    ],
    "path": "/people",
    "per_page": 25,
    "to": 3,
    "total": 3
  }
}
```

<!-- tabs:end -->