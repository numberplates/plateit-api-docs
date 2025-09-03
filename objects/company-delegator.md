# CompanyDelegator

`https://api.plateit.co.uk/v3/delegators`

!> Read only

If your company is an fulfilment delegatee, this is how you can access your delegators.

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

This request returns a collection of companies that are permitted to delegate their fulfilment to you.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/delegators`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "data": [
    {
      "id": 7,
      "name": "Top Plates",
      "email": "info@topplates.xyz",
      "phone_number": "0113 9876543",
      "website_url": "https://topplates.xyz",
      "address_line_1": "186 Top Road",
      "address_line_2": "Leeds",
      "address_line_3": "West Yorkshire",
      "address_postcode": "LS1 5YD",
      "address_country_code": "GB",
      "created_at": "2025-04-03T16:00:08.000000Z",
      "updated_at": "2025-05-25T11:10:11.000000Z",
      "href": "/companies/7",
      "is_approved": true
    }
  ]
}
```
<!-- tabs:end -->
