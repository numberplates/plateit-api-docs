# Delegations

Multiple companies use Plateit to process their number plate orders. If there is a plate type you would like to sell but don't have the means to manufacture it, it can be delegated to another company to fufil on your behalf automatically.

!>First, a delegator/delegatee relationship needs to be established. This can only be created by the Plateit administrator. Once set up, you will be able utilise this feature. You can have multiple delegatees for different products and plate types if required.

# Configuring a Plate or Product to be Delegated

When a delegator/delegatee relationship exists between two companies, you will be able to delegate specific [plate types](/objects/company-plate-type.md) and [products](/objects/company-product.md) to be fulfilled on your behalf by another company.

# Using the Build Order Endpoint

The [build order](/actions/build-order.md) endpoint is used by your customer-facing application to create an entire order in a single `post` request.

Upon receiving the request, Plateit will take care of any delegateions automatically.

TBC...