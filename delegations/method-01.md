# Delegations - Method I

> This page assumes you have first read the [Introduction](/delegations/introduction.md) to delegations.

## Creating a Delegated Package

A [Package](/objects/order-package.md) is assigned a company to fulfil it upon its creation by declaring a `delegate_to_company_id` value in the `POST` request. Once the delegated package has been created, items can be assigned to it.

!> A delegation can only be set up upon the creation of a new package. The delegated company ID cannot be updated at a later time using a `PATCH` request.

On this page assignable "items" may refer to any of the below:

* [CompanyPlate](/objects/company-plate.md)
* [CompanyProduct](/objects/company-product.md)
* [CompanyShippingOption](/objects/company-shipping-option.md)

## Assigning Items to a Delegated Package

!>**Important:** only `foreign` items can be assigned to a delegated package - i.e *their* item IDs and *not* yours. This is because they are responsible for fulfilling the package and therefore the shipping provider will need *their* dimensions and weights, which may be different to yours.

The steps are identical to assigning your own items to your own (undelegated) packages. See here:

* [Package Plate](/objects/order-package-plate.md)
* [Package Product](/objects/order-package-product.md)
* [Package Shipping](/objects/order-package-shipping.md)

The only difference is you will receieve a validation error if you attempt to assign one of your own `local` item IDs to a `foreign` (delegated) package.

Typically you cannot access other companies' data. However, if a delegation relationship exists, you can access the delegatee's available items as outlined in the next section.

> Think of a delegated package as if it belongs to the delegated company; they can only be assigned items that belong to them.

### Retrieving Available Foreign Items

#### Company Plates

As outlined on the [CompanyPlate](/objects/company-plate.md) page, to retrieve your own company's plates, a `GET` request can be sent to: `https://data.plateit.co.uk/v3/plates`.

To retrieve the plates of a `foreign` (delegated) company, a `GET` request can be sent to the following, alternative endpoint: `https://data.plateit.co.uk/v3/delegatees/{delegated_company_id}/plates`.

This will return an array of [CompanyPlate](/objects/company-plate.md) objects belonging to the `foreign` (delegated) company with the same properties as if you were retrieving your own company's **with three additional fields**:

* `_id_local`
* `_price_local`
* `_is_active_local`

The extra fields are data that correspond to *your company's* matching plates.

They are matched using the following properties:

* `company_plate.colour`
* `company_plate_type.reference`
* `system_plate_size.id`

!> Only `foreign` plates you have in common with your `local` plates will be returned in the collection. You can only assign `foreign` plates that also exist in your own catalogue. When assigned to the package, it will assign *your* price and not theirs.

#### Company Products

To retrieve the additional products of a `foreign` (delegated) company, a `GET` request can be sent to: `https://data.plateit.co.uk/v3/delegatees/{delegated_company_id}/products`.

This will return an array of [CompanyProduct](/objects/company-product.md) objects belonging to the `foreign` (delegated) company with the same properties as if you were retrieving your own company's **with four additional fields**:

* `_id_local`
* `_name_local`
* `_price_local`
* `_is_active_local`

The extra fields are data that correspond to *your company's* matching products.

They are matched using the following property:

* `company_product.sku`

!> Only `foreign` products you have in common with your `local` plates will be returned in the collection. You can only assign `foreign` products that also exist in your own catalogue. When assigned to the package, it will assign *your* price and *your* product name (if different) and not theirs.

#### Company Shipping Options

To retrieve the additional shipping options of a `foreign` (delegated) company, a `GET` request can be sent to: `https://data.plateit.co.uk/v3/delegatees/{delegated_company_id}/shipping-options`.

This will return an array of [CompanyShippingOption](/objects/company-shipping-option.md) objects belonging to the `foreign` (delegated) company with the same properties as if you were retrieving your own company's **with three additional fields**:

* `_id_local`
* `_price_local`
* `_is_active_local`

The extra fields are data that correspond to *your company's* matching shipping options.

They are matched using the following property:

* `system_courier_service.id`

!> **Important difference:** Unlike plates and products, *all* `foreign` shipping options will be returned in the collection, not just the ones you have in common. This is because the delegated company is responsible for shipping the order and they may use different courier services to you. When a `foreign` shipping option is assigned to a package, it will use *your* price if a match is found, or their price if no match is found. The price can be manually overridden if you wish, as explained on the [Package Shipping](/objects/order-package-shipping.md) page.
