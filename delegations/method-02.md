# Delegations - Method II

> This page assumes you have first read the [Introduction](/delegations/introduction.md) to delegations and have familiarised yourself with [Method I](/delegations/method-01.md).

## Automatic Delegated Packages

The [Build Order](/actions/build-order.md) endpoint is used to build an entire order, including its contents (plates, products, customer details and a shipping option) in a single request. It is designed to be used at a customer-facing checkout.

Any [CompanyPlateType](/objects/company-plate-type.md) or [CompanyProduct](/objects/company-product.md) that has been explicitly set to be delegated to another company will be handled automatically (see the above links to learn how to set the delegation intents).

If the [Build Order](/actions/build-order.md) request is successful, a new `External Draft` order will be created with a separate [Package](/objects/order-package.md) assigned to each delegated company.

## Important Differences to Method I

### Item IDs

Unlike [Method I](/delegations/method-01.md), you need to reference your *own* company's `local` item IDs in the [Build Order](/actions/build-order.md) payload. Plateit will see that an item has an explicit delegation instruction and will take care of ensuring the correct delegated package is created for it.

!> A validation error will occur if you reference a `local`, delegated item ID that the delegated company does not have. When fetching your available items, pass the `?exclude_unmatched_delegations=1` query paramter to avoid this pitfall. See the [suggested integration guide](/fundamentals/suggested-integration.md) for examples.

### Shipping Option ID

Again, unlike [Method I](/delegations/method-01.md), you need to reference your *own* company's `local` shipping option ID in the [Build Order](/actions/build-order.md) payload. When Plateit automatically creates the delegated package/s, it will attempt to assign a matching shipping option to the `foreign` (delegated) package. If the `foreign` company doesn't have the requested shipping option in common, it will assign the delegated company's closest match.

For example, if you specify the ID for your next-day shipping option with Royal Mail, but the delegated company only uses Evri, their next-day Evri shipping option will be assigned to the delegated package because that's their closest match.

## "Dangling" Products

Let's say Pressed Plates are delegated to another company to fulfil.

Now let's say the [Build Order](/actions/build-order.md) endpoint has been used to allow a customer to puchase a pair of Pressed Plates (delegated) and a Fixing Kit (not delegated).

If Plateit detects the delegated company *also* sells Fixing Kits with a matching SKU, it will assign the Fixing Kit to the same delegated package. This is done to reduce shipping costs, packaging waste, and delivery delays, but only if it would prevent a single item from being shipped separately.