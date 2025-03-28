# CompanyTaxRate

`https://data.plateit.co.uk/v3/tax-rates`

VAT may be applied to orders for specific countries at your discretion. The calculation will be based on the order's destination shipping address. VAT will be collected for all plates, products and shipping options. It will be incorporated into the listed prices (not added on top).

!> This page is a stub. To set tax rates it is recommended to use the [Plateit admin area](https://admin.plateit.co.uk) at this time.

## Data References

### Available Relationships

* [system_country](/objects/system-country.md)

*Learn more about including relationships [here](fundamentals/conventions.md#including-relationships).*

### Available Order Bys

* id
* rate
* is_active
* created_at
* updated_at
* system_country.name
* system_country.iso_code

*Learn more about ordering results [here](fundamentals/conventions.md#ordering-results).*

### Available Filter Bys

* is_active *

*Learn more about filtering results [here](fundamentals/conventions.md#filtering-results).*

**Plateit does not filter out inactive resources for you. It is your responsibility to honour what is shown publicly and what's not.*

### Available Search Bys

* system_country.name
* system_country.iso_code

*Learn more about searching results [here](fundamentals/conventions.md#searching).*