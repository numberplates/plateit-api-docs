# Note

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/notes`

A [package](/objects/order-package.md) can have many notes. Notes are intended to be written by staff members but may be seen by the customer.

## Data References

### Attributes

* **id** `integer` The unique ID of the note.
* **package_id** `integer` The [package](/objects/order-package.md) ID.
* **company_user_id** `integer|null` The ID of the [user](/objects/company-user.md) who wrote the note.
* **note** `string` The note.
* **is_private** `boolean` Should the note be hidden from the customer?
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

### Available Relationships

* [package](/objects/order-package.md)
* [company_user](/objects/company-user.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* is_private
* created_at
* updated_at

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_private *

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

**Plateit does not filter out private notes for you. It is your responsibility to honour what is shown publicly and what's not.*

## Example Requests

### Create a Note

!> Requires the `orders_packages_notes_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **note** `string`
* **is_private** `boolean|null` (defaults to `false`)

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/notes`
* Method: `POST`

```json
{
  "note": "This is a re-send. Original was damaged in transit."
}
```

#### **Response**

* Status code: `201`

```json
{
  "id": 897,
  "package_id": 9067,
  "company_user_id": 19,
  "note": "This is a re-send. Original was damaged in transit.",
  "is_private": false,
  "created_at": "2024-10-15T08:49:36.373862Z",
  "href": "/orders/8591/packages/9067/notes/897"
}
```

<!-- tabs:end -->

### Retrieve a Note

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/notes/{note_id}`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 897,
  "package_id": 9067,
  "company_user_id": 19,
  "note": "This is a re-send. Original was damaged in transit.",
  "is_private": false,
  "created_at": "2024-10-15T08:49:36.373862Z",
  "href": "/orders/8591/packages/9067/notes/897"
}
```

<!-- tabs:end -->

### List Products

!> Requires the `orders_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/notes`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
    "id": 897,
    "package_id": 9067,
    "company_user_id": 19,
    "note": "This is a re-send. Original was damaged in transit.",
    "is_private": false,
    "created_at": "2024-10-15T08:49:36.373862Z",
    "href": "/orders/8591/packages/9067/notes/897"
    }
  ]
}
```

<!-- tabs:end -->

### Update a Note

A note cannot be updated, only created or deleted.

### Delete a Note

!> Requires the `orders_packages_notes_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/notes/{note_id}`
* Method: `DELETE`

#### **Response**

* Status code: `200`

```json
1
```

<!-- tabs:end -->