# DuplicateOrder

`https://data.plateit.co.uk/v3/orders/{order_id}/duplicate`

An [Order](/objects/order.md) can be easily duplicated by sending a `POST` request to this helper endpoint.

It will also duplicate most of its child resources but omit duplicating payments and refunds.

The corresponding (duplicated) [OrderPackage](/objects/order-package.md) and [OrderPackagePlate](/objects/order-package-plate.md) objects will have their progress markers reset: `is_committed`, `is_printed`, etc.

## Example Request

!> Requires the `orders_write` permission.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/duplicate`
* Method: `POST`

#### **Response**

* Status code: `201`

```json
{
  "id": 65749
}
```

> The returned ID is that of the duplicated order.

<!-- tabs:end -->