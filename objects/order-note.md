# OrderNote

`https://api.plateit.co.uk/v3/orders/{order_id}/notes`

An [Order](/objects/order.md) can have multiple `OrderNote` resources. Notes are intended to be written by staff members but may also be visible to the customer.

For notes attached to a specific package, see [OrderPackageNote](/objects/order-package-note.md).

## Data References

### Attributes

* **id** `integer` The unique ID of the note.
* **order_id** `integer` The ID of the [Order](/objects/order.md) the note belongs to.
* **company_user_id** `integer|null` The ID of the [CompanyUser](/objects/company-user.md) who created the note.
* **note** `string` The note content.
* **is_private** `boolean` Indicates whether the note should be hidden from the customer.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Relationships

The following relationships may be included:

* [company_user](/objects/company-user.md)

See [Including Relationships](/fundamentals/conventions.md#including-relationships) for usage.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/orders/{order_id}/notes/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

> Plateit does not automatically exclude private notes. API consumers are responsible for deciding which notes should be shown publicly.

## Create

!> Requires the `orders_notes_write` permission.

**POST** `/v3/orders/{order_id}/notes`

### Body Parameters

* **note** `string`
* **is_private** `boolean` Optional. Defaults to `false`.

### Example Payload

```json
{
  "note": "Customer requested an update before despatch."
}
```

Returns the created `OrderNote` with status `201`.

## Retrieve

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/notes/{note_id}`

Returns the requested `OrderNote`.

## List

!> Requires the `orders_read` permission.

**GET** `/v3/orders/{order_id}/notes`

Returns a collection of `OrderNote` resources.

## Update

`OrderNote` resources cannot be updated. They can only be created or deleted.

## Delete

!> Requires the `orders_notes_write` permission.

**DELETE** `/v3/orders/{order_id}/notes/{note_id}`

Deletes the specified `OrderNote`.
