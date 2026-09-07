# Company

`https://api.plateit.co.uk/v3/companies/current`

The `Company` object primarily contains your company's contact and address information.

**This resource can be retrieved and updated only.**

## Data References

### Attributes

* **id** `integer` The unique ID of the company.
* **name** `string` The name of the company.
* **email** `string` The company's main email address.
* **phone_number** `string` The company's phone number.
* **website_url** `string` The company's website address.
* **address_line_1** `string` The first line of the address.
* **address_line_2** `string|null` The second line of the address.
* **address_line_3** `string` The city or locality.
* **address_postcode** `string` The postcode.
* **address_country_code** `string` The two-character ISO country code, such as `GB`.
* **created_at** `string` The creation timestamp in ISO 8601 format.
* **updated_at** `string` The last-updated timestamp in ISO 8601 format.
* **href** `string` The path to the resource.

## Retrieve

!> Requires the `company_settings_read` permission.

**GET** `/v3/companies/current`

Returns the current `Company`.

## Update

!> Requires the `company_settings_write` permission.

**PATCH** `/v3/companies/current`

### Body Parameters

All fields are optional:

* **name** `string`
* **email** `string`
* **phone_number** `string`
* **website_url** `string`
* **address_line_1** `string`
* **address_line_2** `string|null`
* **address_line_3** `string`
* **address_postcode** `string`
* **address_country_code** `string`

### Example Payload

```json
{
  "name": "Acme Plates LTD"
}
```

Returns the updated `Company`.
