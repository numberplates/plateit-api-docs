# SystemUserPermission

`https://api.plateit.co.uk/v3/system-user-permissions`

!> Read only

A `SystemUserPermission` represents an API permission that can be assigned to a [CompanyUser](/objects/company-user.md) or [CompanyAccessToken](/objects/company-access-token.md).

Permissions control which parts of the API a user or access token is authorised to read or modify.

## Data References

### Attributes

* **id** `integer` The unique ID of the permission.
* **ability_key** `string` The unique permission key used by the API.
* **description** `string` A description of the actions permitted by the ability.
* **href** `string` The path to the resource.

## Values

The following permissions are available:

```json
[
  {
    "id": 1,
    "ability_key": "company_plate_types_read",
    "description": "Read company plate types."
  },
  {
    "id": 2,
    "ability_key": "company_plate_types_write",
    "description": "Write company plate types."
  },
  {
    "id": 3,
    "ability_key": "company_plates_read",
    "description": "Read company plates."
  },
  {
    "id": 4,
    "ability_key": "company_plates_write",
    "description": "Create, update and delete company plates."
  },
  {
    "id": 5,
    "ability_key": "company_products_read",
    "description": "Read company products (extras)."
  },
  {
    "id": 6,
    "ability_key": "company_products_write",
    "description": "Create, update and delete company products (extras)."
  },
  {
    "id": 7,
    "ability_key": "company_shipping_options_read",
    "description": "Read company shipping options."
  },
  {
    "id": 8,
    "ability_key": "company_shipping_options_write",
    "description": "Create, update and delete company shipping options."
  },
  {
    "id": 9,
    "ability_key": "company_users_read",
    "description": "Read company users."
  },
  {
    "id": 10,
    "ability_key": "company_users_write",
    "description": "Create, update and delete company users."
  },
  {
    "id": 11,
    "ability_key": "company_settings_read",
    "description": "Read company settings and API keys (contains sensitive data)."
  },
  {
    "id": 12,
    "ability_key": "company_settings_write",
    "description": "Update company settings and API keys (contains sensitive data)."
  },
  {
    "id": 13,
    "ability_key": "orders_read",
    "description": "Read orders and their contents."
  },
  {
    "id": 14,
    "ability_key": "orders_write",
    "description": "Create, update and delete orders."
  },
  {
    "id": 15,
    "ability_key": "orders_fulfil",
    "description": "Batch update order statuses, package statuses and print statuses."
  },
  {
    "id": 16,
    "ability_key": "orders_customer_write",
    "description": "Update customer contact details and shipping/billing addresses."
  },
  {
    "id": 17,
    "ability_key": "orders_payments_write",
    "description": "Record payments received."
  },
  {
    "id": 18,
    "ability_key": "orders_payments_refunds_write",
    "description": "Issue refunds."
  },
  {
    "id": 19,
    "ability_key": "orders_notes_write",
    "description": "Assign notes to orders."
  },
  {
    "id": 20,
    "ability_key": "orders_packages_write",
    "description": "Create and delete packages."
  },
  {
    "id": 21,
    "ability_key": "orders_packages_plates_write",
    "description": "Create, update and remove number plates."
  },
  {
    "id": 22,
    "ability_key": "orders_packages_products_write",
    "description": "Create, update and remove extra products."
  },
  {
    "id": 23,
    "ability_key": "orders_packages_shipping_write",
    "description": "Assign, update and remove shipping options."
  },
  {
    "id": 24,
    "ability_key": "orders_packages_notes_write",
    "description": "Assign notes to packages."
  },
  {
    "id": 25,
    "ability_key": "orders_build",
    "description": "Create external draft orders in their entirety (including contents) with a single request."
  },
  {
    "id": 26,
    "ability_key": "company_reports_read",
    "description": "Read company sales and fulfilment reports."
  },
  {
    "id": 27,
    "ability_key": "orders_documents_write",
    "description": "Approve, reject and delete order documents."
  },
  {
    "id": 28,
    "ability_key": "orders_documents_upload",
    "description": "Upload and replace rejected order document files."
  }
]
```

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/system-user-permissions/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/system-user-permissions`

Returns a paginated collection of `SystemUserPermission` resources.
