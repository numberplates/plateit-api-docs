# CompanyDelegator

`https://api.plateit.co.uk/v3/delegators`

!> Read only

A `CompanyDelegator` represents a company that is permitted to delegate package fulfilment to your company.

If your company acts as a fulfilment delegatee, this endpoint allows you to access the companies that can delegate work to you.

See the [delegation guide](/fundamentals/delegations.md) for more information.

## Data References

### Attributes

The attributes are identical to the [Company](/objects/company.md) object with the addition of:

* **is_approved** `boolean` Indicates whether the delegation relationship with your company is approved and active.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/delegators/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/delegators`

Returns a collection of companies that are permitted to delegate their fulfilment to your company.
