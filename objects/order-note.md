# OrderNote

`https://data.plateit.co.uk/v3/orders/{order_id}/notes`

An [Order](/objects/order.md) can have many notes. Notes are intended to be written by staff members but may be seen by the customer.

!> This page is a stub. However, the handling is almost idential to the [OrderPackageNote](/objects/order-package-note.md) documentation.

## Data References

### Attributes

* **id** `integer` The unique ID of the note.
* **order_id** `integer` The [Order](/objects/order.md) ID.
* **company_user_id** `integer|null` The ID of the [CompanyUser](/objects/company-user.md) who wrote the note.
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

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_private *

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

**Plateit does not filter out private notes for you. It is your responsibility to honour what is shown publicly and what's not.*