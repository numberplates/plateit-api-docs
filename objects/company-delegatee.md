# CompanyDelegatee

`https://data.plateit.co.uk/v3/delegatees`

!> Read only

If a delegator/delegatee relationship exists between your company and another, you will be able to access your delegatee's product data (the items they sell). This allows you to add their items to a package you have delegated to them to fulfil on your behalf.

> Please see the [delegation guide](/fundamentals/delegations.md) for added context.

# Data References

### Attributes

All attributes are idendtical to the [Company](/objects/company.md) object with the addition of an `is_approved` boolean. This signifies whether the delegation relationship with your company is approved and active. See the example request responses below for clarification.

### Available Order Bys

* id
* name
* is_approved

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_approved

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

## Example Requests

### Retrieve

This request returns a collection of companies that you are permitted to create delegated packages for.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/delegatees`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 2,
      "name": "Vince's Vehicle Accessories",
      "email": "contact@vincesvehicle.com",
      "phone_number": "0207 1234567",
      "website_url": "https://vincesvehicle.com",
      "address_line_1": "45 High Street",
      "address_line_2": "Birmingham",
      "address_line_3": "West Midlands",
      "address_postcode": "B1 1AA",
      "address_country_code": "GB",
      "created_at": "2025-03-03T14:10:51.000000Z",
      "updated_at": "2025-03-03T14:10:51.000000Z",
      "href": "/companies/2",
      "is_approved": true
    },
    {
      "id": 3,
      "name": "Fast Plates UK",
      "email": "info@fastplatesuk.com",
      "phone_number": "0161 9876543",
      "website_url": "https://fastplatesuk.com",
      "address_line_1": "67 Willow Way",
      "address_line_2": "Salford",
      "address_line_3": "Greater Manchester",
      "address_postcode": "M3 2JK",
      "address_country_code": "GB",
      "created_at": "2025-03-03T14:10:51.000000Z",
      "updated_at": "2025-03-03T14:10:51.000000Z",
      "href": "/companies/3",
      "is_approved": true
    }
  ]
}
```
<!-- tabs:end -->
