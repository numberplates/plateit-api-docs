# UpdateOrderPackageStatuses (Bulk)

`https://data.plateit.co.uk/v3/actions/update-package-statuses`

This helper endpoint is the *only* way to update the [SystemPackageStatus](/objects/system-package-status.md) of an [OrderPackage](/objects/order-package.md). It can be used to batch update the statuses of many packages at the same time.

## Data References

### Request Attributes

* **packages** `array` An array of objects.
    * **id** `integer` The ID of the [OrderPackage](/objects/order-package.md) to update.
    * **system_package_status_id** `integer` The ID of the desired [SystemPackageStatus](/objects/system-package-status.md).
    * **contact_hint** `boolean|null` Sends a contact hint to your webhook endpoint if configured to receive the `order-package:status-update` event. Please read the [Webhooks Guide](/fundamentals/webhooks.md) for more information.

> If performing a bulk update, the desired status can be different for each package if you wish; they don't all have to be updated to the same status.

### Response Attributes

The response body contains extra data pertaining to the results of the request:

* **packages** `array` An array of objects.
    * **id** `integer` The ID of the [OrderPackage](/objects/order-package.md) that may or may not have updated.
    * **order_id** `integer` The ID of the package's corresponding [Order](/objects/order.md).
    * **system_package_status_id** `integer` The ID of the [SystemPackageStatus](/objects/system-package-status.md) after the request was made.
    * **previous_system_package_status_id** `integer` The ID of the [SystemPackageStatus](/objects/system-package-status.md) before the request was made.
    * **has_package_updated** `boolean` This will be `true` if an update to the package's status occurred.
    * **has_contact_hint** `boolean` This will be `true` if a webhook `contact_hint` was requested and an update to the package's status occurred.
    * **has_order_updated** `boolean` This will be `true` if the package's corresponding [Order](/objects/order.md) was also updated with the request. For example, if its [SystemOrderFulfilmentStatus](/objects/system-order-fulfilment-status.md) changed as a result of the request.

## Example Requests

### Update

!> Requires the `orders_fulfil` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **packages** `array`
    * **id** `integer`
    * **system_package_status_id** `integer`
    * **contact_hint** `boolean|null` (defaults to `false`)

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/actions/update-package-statuses`
* Method: `POST`

```json
{
  "packages": [
    {
      "id": 12880,
      "system_package_status_id": 4,
      "contact_hint": true
    },
    {
      "id": 12881,
      "system_package_status_id": 4,
      "contact_hint": true
    }
  ]
}
```

#### **Response**

* Status code: `200`

> In the example below we can see that package ID 12881 was *not* updated because its status ID was already `4`. A contact hint was requested but the resulting `has_contact_hint` is `false` because no change to the package occurred.

```json
{
  "packages": [
    {
      "id": 12880,
      "order_id": 13129,
      "company_id": 4,
      "system_package_status_id": 4,
      "previous_system_package_status_id": 3,
      "has_package_updated": true,
      "has_contact_hint": true,
      "has_order_updated": true
    },
    {
      "id": 12881,
      "order_id": 13130,
      "company_id": 4,
      "system_package_status_id": 4,
      "previous_system_package_status_id": 4,
      "has_package_updated": false,
      "has_contact_hint": false,
      "has_order_updated": false
    }
  ]
}
```

<!-- tabs:end -->