# CompanyDelegatee

`https://api.plateit.co.uk/v3/delegatees`

!> Read only

A `CompanyDelegatee` represents a company that your company is permitted to delegate package fulfilment to.

If a delegator/delegatee relationship exists between your company and another company, you can access the delegatee's product data and use those items when building packages delegated to them for fulfilment.

See the [delegation guide](/fundamentals/delegations.md) for more information.

## Data References

### Attributes

The attributes are identical to the [Company](/objects/company.md) object with the addition of:

* **is_approved** `boolean` Indicates whether the delegation relationship with your company is approved and active.

## Query Capabilities

All currently supported query fields, including filters and ordering, can be retrieved from:

**GET** `/v3/delegatees/capabilities`

See the [conventions guide](/fundamentals/conventions.md) for syntax and behaviour.

## List

**GET** `/v3/delegatees`

Returns a collection of companies that your company is permitted to create delegated packages for.
