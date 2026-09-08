# Order Lifecycle

An [Order](/objects/order.md) can contain one or more [OrderPackage](/objects/order-package.md) objects.

Plateit maintains three separate order-level statuses:

* [SystemOrderStatus](/objects/system-order-status.md): represents the overall lifecycle state of the order.
* [SystemOrderFulfilmentStatus](/objects/system-order-fulfilment-status.md): represents how much of the order has been despatched.
* [SystemOrderDocumentStatus](/objects/system-order-document-status.md): represents the aggregate state of any supporting documents required by the order.

These statuses are maintained automatically by Plateit and cannot be updated directly by the user.

## Order Status

An order's [SystemOrderStatus](/objects/system-order-status.md) reflects the lifecycle state of its packages.

### Draft (External or Internal)

A draft order has no committed packages.

### Open

A package is considered ready for fulfilment once it has been **committed**.

When one or more packages in an order are committed, the order becomes `Open`.

> Committing a package means that its contents and fulfilment details are complete and it is ready to be processed. Committed packages, when moved to [Processing](/objects/system-package-status.md), become available for bulk printing.

An `Open` order may contain a mixture of committed and uncommitted packages.

### Closed

An order becomes `Closed` once every package has reached either a `Despatched` or `Cancelled` [status](/objects/system-package-status.md).

At this point there are no remaining packages awaiting fulfilment. The order is now effectively archived.

## Order Fulfilment Status

An order's [SystemOrderFulfilmentStatus](/objects/system-order-fulfilment-status.md) tracks despatch progress independently of its main order status.

### Unfulfilled

An order is `Unfulfilled` when none of its packages have been despatched.

### Partially Fulfilled

An order is `Partially Fulfilled` when at least one package has been despatched but one or more other packages have not.

### Fulfilled

An order is `Fulfilled` when all of its packages have been despatched.

> The fulfilment status is based on how many packages have reached `Despatched`, while the main order status reflects the broader lifecycle state of the order's packages.

## Order Document Status

An order's [SystemOrderDocumentStatus](/objects/system-order-document-status.md) represents the aggregate state of any supporting documents required by its plate line items.

### Not Required

The order does not require any supporting documents.

### Awaiting Upload

One or more required supporting documents have not yet been supplied.

### Awaiting Approval

All required supporting documents have been supplied, but one or more are still awaiting approval.

### Approved

All required supporting documents have been approved.

> A fully paid order may remain in a draft state while its document status is `Awaiting Upload` or `Awaiting Approval`. Once all required documents have been approved, the order will become `Open` and its uncancelled packages will be committed for fulfilment.

For more information, see the [Supporting Documents](/fundamentals/documents.md) guide.
