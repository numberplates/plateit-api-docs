# SystemUserPermission

`https://data.plateit.co.uk/v3/system-user-permissions`

!> Read only

Each [CompanyUser](/objects/company-user.md) and [CompanyAccessToken](/objects/company-access-token.md) is assigned one or more of these permissions.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/system-user-permissions`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 1,
      "ability_key": "company_plate_types_read",
      "description": "Read company plate types.",
      "href": "/system-user-permissions/1"
    },
    {
      "id": 2,
      "ability_key": "company_plate_types_write",
      "description": "Write company plate types.",
      "href": "/system-user-permissions/2"
    },
    {
      "id": 3,
      "ability_key": "company_plates_read",
      "description": "Read company plates.",
      "href": "/system-user-permissions/3"
    },
    {
      "id": 4,
      "ability_key": "company_plates_write",
      "description": "Create, update and delete company plates.",
      "href": "/system-user-permissions/4"
    },
    {
      "id": 5,
      "ability_key": "company_products_read",
      "description": "Read company products (extras).",
      "href": "/system-user-permissions/5"
    },
    {
      "id": 6,
      "ability_key": "company_products_write",
      "description": "Create, update and delete company products (extras).",
      "href": "/system-user-permissions/6"
    },
    {
      "id": 7,
      "ability_key": "company_shipping_read",
      "description": "Read company shipping options.",
      "href": "/system-user-permissions/7"
    },
    {
      "id": 8,
      "ability_key": "company_shipping_write",
      "description": "Create, update and delete company shipping options.",
      "href": "/system-user-permissions/8"
    },
    {
      "id": 9,
      "ability_key": "company_users_read",
      "description": "Read company users.",
      "href": "/system-user-permissions/9"
    },
    {
      "id": 10,
      "ability_key": "company_users_write",
      "description": "Create, update and delete company users.",
      "href": "/system-user-permissions/10"
    },
    {
      "id": 11,
      "ability_key": "company_settings_read",
      "description": "Read company settings, tax rates and API keys (contains sensitive data).",
      "href": "/system-user-permissions/11"
    },
    {
      "id": 12,
      "ability_key": "company_settings_write",
      "description": "Update company settings, tax rates and API keys (contains sensitive data).",
      "href": "/system-user-permissions/12"
    },
    {
      "id": 13,
      "ability_key": "orders_read",
      "description": "Read orders and their contents.",
      "href": "/system-user-permissions/13"
    },
    {
      "id": 14,
      "ability_key": "orders_write",
      "description": "Create, update and delete orders.",
      "href": "/system-user-permissions/14"
    },
    {
      "id": 15,
      "ability_key": "orders_fulfil",
      "description": "Batch update order statuses, package statuses and print statuses.",
      "href": "/system-user-permissions/15"
    },
    {
      "id": 16,
      "ability_key": "orders_customer_write",
      "description": "Update customer contact details and shipping/billing addresses.",
      "href": "/system-user-permissions/16"
    },
    {
      "id": 17,
      "ability_key": "orders_payments_write",
      "description": "Record payments received.",
      "href": "/system-user-permissions/17"
    },
    {
      "id": 18,
      "ability_key": "orders_payments_refunds_write",
      "description": "Issue refunds.",
      "href": "/system-user-permissions/18"
    },
    {
      "id": 19,
      "ability_key": "orders_notes_write",
      "description": "Assign notes to orders.",
      "href": "/system-user-permissions/19"
    },
    {
      "id": 20,
      "ability_key": "orders_packages_write",
      "description": "Create and delete packages.",
      "href": "/system-user-permissions/20"
    },
    {
      "id": 21,
      "ability_key": "orders_packages_plates_write",
      "description": "Create, update and remove number plates.",
      "href": "/system-user-permissions/21"
    },
    {
      "id": 22,
      "ability_key": "orders_packages_products_write",
      "description": "Create, update and remove extra products.",
      "href": "/system-user-permissions/22"
    },
    {
      "id": 23,
      "ability_key": "orders_packages_shipping_write",
      "description": "Assign, update and remove shipping options.",
      "href": "/system-user-permissions/23"
    },
    {
      "id": 24,
      "ability_key": "orders_packages_notes_write",
      "description": "Assign notes to packages.",
      "href": "/system-user-permissions/24"
    },
    {
      "id": 25,
      "ability_key": "orders_build",
      "description": "Create external draft orders in their entirety (including contents) with a single request.",
      "href": "/system-user-permissions/25"
    }
  ]
}
```

<!-- tabs:end -->