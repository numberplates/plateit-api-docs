# Company

`https://api.plateit.co.uk/v3/companies/current`

This object primarily consists of your company's contact information. **It can be fetched and updated only**.

## Data References

### Attributes

* **id** `integer` The unique ID of the company.
* **name** `string` The name of the company.
* **email** `string` The company's main email address.
* **phone_number** `string` The company's phone number.
* **website_url** `string` The company's website address.
* **address_line_1** `string` The first line of the address.
* **address_line_2** `string` The second line of the address (optional).
* **address_line_3** `string` The city.
* **address_postcode** `string` The postcode.
* **address_country_code** `string` The two-character ISO country code, such as "GB".
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Example Requests

### Retrieve

!> Requires the `company_settings_read` permission.

<!-- tabs:start -->

#### **Body Parameters**

No parameters.

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/companies/current`
* Method: `GET`

#### **Response**

* Status code: `200`

```json
{
  "id": 12,
  "name": "Acme Plates",
  "email": "contact@acmeplates.com",
  "phone_number": "0151 2345678",
  "website_url": "https://acmeplates.com",
  "address_line_1": "23 Cedar Street",
  "address_line_2": "Liverpool",
  "address_line_3": "Merseyside",
  "address_postcode": "L1 5IJ",
  "address_country_code": "GB",
  "created_at": "2024-10-02T11:55:01.000000Z",
  "updated_at": "2024-10-02T11:55:01.000000Z",
  "href": "/companies/12"
}
```

<!-- tabs:end -->


### Update

!> Requires the `company_settings_write` permission.

<!-- tabs:start -->

#### **Body Parameters**

* **name** `string|null`
* **email** `string|null`
* **phone_number** `string|null`
* **website_url** `string|null`
* **address_line_1** `string|null`
* **address_line_2** `string|null`
* **address_line_3** `string|null`
* **address_postcode** `string|null`
* **address_country_code** `string|null`

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/companies/current`
* Method: `PATCH`

```json
{
  "name": "Acme Plates LTD"
}
```

#### **Response**

* Status code: `200`

```json
{
  "id": 12,
  "name": "Acme Plates LTD",
  "email": "contact@acmeplates.com",
  "phone_number": "0151 2345678",
  "website_url": "https://acmeplates.com",
  "address_line_1": "23 Cedar Street",
  "address_line_2": "Liverpool",
  "address_line_3": "Merseyside",
  "address_postcode": "L1 5IJ",
  "address_country_code": "GB",
  "created_at": "2024-10-02T11:55:01.000000Z",
  "updated_at": "2024-10-04T08:51:22.000000Z",
  "href": "/companies/12"
}
```

<!-- tabs:end -->
