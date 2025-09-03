# Delegations

Many companies use Plateit to process their number plate orders. If there is a plate type you would like to sell but don't have the means to manufacture it, it can be delegated to another company to fufil on your behalf.

!>First, a delegator/delegatee relationship needs to be established. This can only be created by the Plateit administrator. Once set up, you will be able utilise this feature. You can have multiple delegatees for different products and plate types if required.

To help understand how delegations work, think of your own company as the `local` company and the delegated company as the `foreign` company.

There are two ways to achieve a delegation:

1. By manually creating a delegated [OrderPackage](/objects/order-package.md).
2. By utilising the [BuildOrder](/helpers/build-order.md) helper endpoint to create an entire order, including its contents, in a single request.

The following section will focus on the first method because it helps better illustrate how delegations are handled. The second method will be discussed later.

## Method 1 - Manual Creation

An [OrderPackage](/objects/order-package.md) is assigned a [Company](/objects/company.md) to fulfil it upon its creation by declaring a `delegate_to_company_id` value in the `POST` request. Once the delegated [OrderPackage](/objects/order-package.md) has been created, items can be assigned to it.

!> A delegation can only be set up upon the creation of a new OrderPackage. The delegated company ID cannot be updated at a later time using a `PATCH` request.

On this page assignable "items" may refer to any of the below:

* [CompanyPlate](/objects/company-plate.md)
* [CompanyProduct](/objects/company-product.md)
* [CompanyShippingOption](/objects/company-shipping-option.md)

### Assigning Items

!>**Important:** only `foreign` items can be assigned to a delegated OrderPackage - i.e *their* item IDs and *not* yours. This is because they are responsible for fulfilling the package and therefore the shipping provider will need *their* dimensions and weights, which may be different to yours.

The steps are identical to assigning your own items to your own (undelegated) packages. See here:

* [OrderPackagePlate](/objects/order-package-plate.md)
* [OrderPackageProduct](/objects/order-package-product.md)
* [OrderPackageShipping](/objects/order-package-shipping.md)

The only difference is you will receieve a validation error if you attempt to assign one of your own `local` item IDs to a `foreign` (delegated) package.

Typically you cannot access other companies' data. However, if a delegation relationship exists, you can access the delegatee's available items as outlined in the next section.

> Think of a delegated OrderPackage as if it belongs to the delegated company; they can only be assigned items that belong to them.

### Retrieving Available Foreign Items

#### CompanyPlate Objects

As outlined on the [CompanyPlate](/objects/company-plate.md) page, to retrieve your own company's plates, a `GET` request can be sent to: `https://api.plateit.co.uk/v3/plates`.

To retrieve the plates of a `foreign` (delegated) company, a `GET` request can be sent to the following, alternative endpoint: `https://api.plateit.co.uk/v3/delegatees/{delegated_company_id}/plates`.

This will return an array of [CompanyPlate](/objects/company-plate.md) objects belonging to the `foreign` (delegated) company with the same properties as if you were retrieving your own company's **with three additional fields**:

* `_id_local`
* `_price_local`
* `_is_active_local`

The extra fields are data that correspond to *your company's* matching CompanyPlate objects.

They are matched using the following properties:

* `company_plate.colour`
* `company_plate_type.reference`
* `system_plate_size.id`

!> Only `foreign` plates you have in common with your `local` plates will be returned in the collection. You can only assign `foreign` plates that also exist in your own catalogue. When assigned to the package, it will assign *your* price and not theirs.

#### CompanyProduct Objects

To retrieve the additional products of a `foreign` (delegated) company, a `GET` request can be sent to: `https://api.plateit.co.uk/v3/delegatees/{delegated_company_id}/products`.

This will return an array of [CompanyProduct](/objects/company-product.md) objects belonging to the `foreign` (delegated) company with the same properties as if you were retrieving your own company's **with four additional fields**:

* `_id_local`
* `_name_local`
* `_price_local`
* `_is_active_local`

The extra fields are data that correspond to *your company's* matching CompanyProduct objects.

They are matched using the following property:

* `company_product.sku`

!> Only `foreign` products you have in common with your `local` products will be returned in the collection. You can only assign `foreign` products that also exist in your own catalogue. When assigned to the package, it will assign *your* price and *your* product name (if different) and not theirs.

#### CompanyShippingOption Objects

To retrieve the additional shipping options of a `foreign` (delegated) company, a `GET` request can be sent to: `https://api.plateit.co.uk/v3/delegatees/{delegated_company_id}/shipping-options`.

This will return an array of [CompanyShippingOption](/objects/company-shipping-option.md) objects belonging to the `foreign` (delegated) company with the same properties as if you were retrieving your own company's **with three additional fields**:

* `_id_local`
* `_price_local`
* `_is_active_local`

The extra fields are data that correspond to *your company's* matching CompanyShippingOption objects.

They are matched using the following property:

* `system_courier_service.id`

!> **Important difference:** Unlike plates and products, *all* `foreign` shipping options will be returned in the collection, not just the ones you have in common. This is because the delegated company is responsible for shipping the order and they may use different courier services to you. When a `foreign` shipping option is assigned to an OrderPackage, it will use *your* shipping price if a match is found, or their price if no match is found. The price can be manually overridden if you wish, as explained on the [OrderPackageShipping](/objects/order-package-shipping.md) page.

## Method 2 - Automatic Creation

The [BuildOrder](/helpers/build-order.md) helper endpoint is used to build an entire order, including its nested contents, in a single request. It is designed to be used at a customer-facing checkout.

Any [CompanyPlateType](/objects/company-plate-type.md) or [CompanyProduct](/objects/company-product.md) objects that have been *explicitly* set to be delegated to another company will be handled automatically (see the above links to learn how to set the delegation intents).

If the [BuildOrder](/helpers/build-order.md) request is successful, a new `External Draft` order will be created with a separate [OrderPackage](/objects/order-package.md) assigned to each delegated company.

### Important Differences to Method 1

#### Item IDs

Unlike Method 1, you need to reference your *own* company's `local` item IDs in the [BuildOrder](/helpers/build-order.md) payload. Plateit will see that an item has an explicit delegation instruction and will take care of ensuring the correct delegated OrderPackage is created for it.

!> A validation error will occur if you reference a `local`, delegated item ID that the delegated company does not have. When fetching your available items, pass the `?exclude_unmatched_delegations=1` query paramter to avoid this pitfall. See the [suggested integration guide](/fundamentals/suggested-integration.md) for examples.

#### Shipping Option ID

Again, unlike Method 1, you need to reference your *own* company's `local` [CompanyShippinOption](/objects/company-shipping-option.md) ID in the [BuildOrder](/helpers/build-order.md) payload. When Plateit automatically creates the delegated OrderPackage/s, it will attempt to assign a matching shipping option to the `foreign` (delegated) package. If the `foreign` company doesn't have the requested shipping option in common, it will assign the delegated company's closest match.

For example, if you specify the ID for your next-day shipping option with Royal Mail, but the delegated company only uses Evri, their next-day Evri CompanyShippingOption will be assigned to the delegated OrderPackage because that's their closest match.

### "Dangling" Products

Let's say Pressed Plates are delegated to another company to fulfil.

Now let's say the [BuildOrder](/helpers/build-order.md) endpoint has been used to allow a customer to purchase a pair of Pressed Plates (delegated) and a Fixing Kit (not delegated).

If Plateit detects the delegated company *also* sells Fixing Kits with a matching SKU, it will assign the Fixing Kit to the same delegated OrderPackage. This is done to reduce shipping costs, packaging waste, and delivery delays, but only if it would prevent a single item from being shipped separately.