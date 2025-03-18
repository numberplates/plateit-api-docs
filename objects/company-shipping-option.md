# CompanyShippingOption

`https://data.plateit.co.uk/v3/shipping-options`

The CompanyShippingOption object represents a shipping option the customer can choose. It references a [SystemCourierService](/objects/system-courier-service.md).

## Data References

### Attributes

* **id** `integer` The unique ID of the shipping option.
* **system_courier_service_id** `integer` The [SystemCourierService](/objects/system-courier-service.md) ID.
* **additional_options** `array` An array of courier-specific additional option strings.
* **name** `string` The name of the shipping option.
* **price** `int` The price in pence including [VAT](/objects/company-tax-rate.md).
* **is_active** `boolean` Indicates whether the resource is live or a draft.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [system_courier_service](/objects/system-courier-service.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* name
* price
* is_active
* created_at
* updated_at
* system_courier_service.id
* system_courier_service.name
* system_courier_service.priority_level
* system_courier_service.is_international

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_active *
* system_courier_services.id
* system_courier_services.name
* system_courier_service.priority_level'
* system_courier_service.is_international

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

**Plateit does not filter out inactive resources for you. It is your responsibility to honour what is shown publicly and what's not.*

## Example Requests

### Create a Shipping Option

!> Requires the `company_shipping_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **name** `string`
* **system_courier_service_id** `int`
* **price** `int`
* **additional_options** `array|null`
* **is_active** `boolean`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/shipping-options`
* Method: `POST`

```json
{
  "system_courier_service_id": 5,
  "name": "Special Delivery",
  "price": 999,
  "is_active": true
}
```

#### **Response**

* Status code: `201`

```json
{
  "id": 11,
  "system_courier_service_id": 5,
  "name": "Special Delivery",
  "additional_options": [],
  "price": 999,
  "is_active": true,
  "created_at": "2024-09-30T13:44:02.000000Z",
  "updated_at": "2024-09-30T13:44:02.000000Z",
  "href": "/shipping-options/11"
}
```

<!-- tabs:end -->

### Retrieve a Shipping Option

!> Requires the `company_shipping_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/shipping-options/{shipping_id}`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 11,
  "system_courier_service_id": 5,
  "name": "Special Delivery",
  "additional_options": [],
  "price": 999,
  "is_active": true,
  "created_at": "2024-09-30T13:44:02.000000Z",
  "updated_at": "2024-09-30T13:44:02.000000Z",
  "href": "/shipping-options/11"
}
```

<!-- tabs:end -->

### List Shipping Options

!> Requires the `company_shipping_read` permission.

> The following example includes relationships. 

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/shipping-options`
* Method: `GET`
* Query:
  * with: `system_courier_service`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 10,
      "system_courier_service_id": 4,
      "name": "First Class Signed For",
      "additional_options": [],
      "price": 500,
      "is_active": true,
      "created_at": "2024-09-30T13:43:21.000000Z",
      "updated_at": "2024-09-30T13:43:21.000000Z",
      "href": "/shipping-options/10",
      "system_courier_service": {
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
      }
    },
    {
      "id": 11,
      "system_courier_service_id": 5,
      "name": "Special Delivery",
      "additional_options": [],
      "price": 999,
      "is_active": true,
      "created_at": "2024-09-30T13:44:02.000000Z",
      "updated_at": "2024-09-30T13:44:02.000000Z",
      "href": "/shipping-options/11",
      "system_courier_service": {
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
      }
    }
  ]
}
```

<!-- tabs:end -->

### Update a Shipping Option

!> Requires the `company_shipping_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **name** `string|null`
* **system_courier_service_id** `int|null`
* **price** `int|null`
* **additional_options** `array|null`
* **is_active** `boolean|null`

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/shipping-options/{shipping_id}`
* Method: `PATCH`

```json
{
  "is_active": false
}
```

#### **Response**

* Status code: `200`

```json
{
  "id": 11,
  "system_courier_service_id": 5,
  "name": "Special Delivery",
  "additional_options": [],
  "price": 999,
  "is_active": false,
  "created_at": "2024-09-30T13:44:02.000000Z",
  "updated_at": "2024-09-30T13:46:35.000000Z",
  "href": "/shipping-options/11"
}
```

<!-- tabs:end -->

### Delete a Shipping Option

!> Requires the `company_shipping_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/shipping-options/{shipping_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->