# DuplicateOrderPackage

`https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/duplicate`

An [OrderPackage](/objects/order-package.md) can be easily duplicated by sending a `POST` request to this helper endpoint.

It will also duplicate its child resources.

## Example Request

!> Requires the `orders_packages_write` permission.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/duplicate`
* Method: `POST`

#### **Response**

* Status code: `201`

```json
{
  "id": 94423
}
```

> The returned ID is that of the duplicated package.

<!-- tabs:end -->