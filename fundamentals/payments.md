# Payments

Plateit is able to keep track of payments and refunds made using PayPal and/or Stripe providing it is set up correctly to do so.

It does this using webhooks.

1. A payment is made pertaining to a Plateit order ID using a supported payment provider.
2. The payment provider sends a webhook to Plateit with details of the payment.
3. The payment is recorded in the system after the authenticity of the webhook is verified.

> Note: Plateit only supports payments made in GBP.

## PayPal

To integrate PayPal please follow the steps below:

1. Log into [https://developer.paypal.com](https://developer.paypal.com) and create a new REST API application.
2. Create a new Webhook for your application and point it to: `https://api.plateit.co.uk/v3/webhooks/paypal` ensuring the event types `PAYMENT.CAPTURE.COMPLETED` and `PAYMENT.CAPTURE.REFUNDED` are selected.
3. Save the application's *Client ID* and *Secret Key* inside your company settings along with your newly created PayPal *Webhook ID*.

The next thing you need to ensure is that your front-end application (website) utilises the same PayPal API keys to create and capture payments from your customers.

PayPal payments can take an `invoice_id` parameter. **Ensure this is populated with the order ID returned from the [BuildOrder](/helpers/build-order.md) endpoint.**

When a PayPal order has been successfully created and captured, a webhook will be sent to Plateit by PayPal. Plateit will know which order the payment pertains to because the `invoice_id` value holds the Plateit order ID.

The payment will be logged accordingly and if all supporting-document requirements have been satisfied, the order will become Open; otherwise, it will remain in a draft state until those requirements have been completed.

> Note: If you create a page where customers can pay an outstanding balance at a later date, you will get a PayPal error if a previous payment has already been made with PayPal pertaining to that order. This is because the `invoice_id` (Plateit's order ID) has already been used. This catch can be turned off inside PayPal under *account settings -> payment preferences -> block payments*. Select *"allow multiple payments per invoice id"*. 

## Stripe

To integrate Stripe please follow the steps below:

1. Log into https://dashboard.stripe.com and obtain your Stripe API keys.
2. Create a new webhook endpoint pointing to: `https://api.plateit.co.uk/v3/webhooks/stripe` ensuring the event types `payment_intent.succeeded` and `refund.created` are selected.
3. Save your Stripe *Publishable Key*, *Secret Key* and *Webhook Signing Secret* inside your company settings.

The next thing you need to ensure is that your front-end application (website) uses the same Stripe account to create and confirm payments from your customers.

A Stripe `PaymentIntent` object can take custom metadata values. **Ensure the `order_id` value is populated with the order ID returned from the [BuildOrder](/helpers/build-order.md) endpoint.**

For example:

```text
metadata[order_id] = 12345
```

When a Stripe `PaymentIntent` has successfully completed, a `payment_intent.succeeded` webhook will be sent to Plateit. Plateit will know which order the payment pertains to because the `metadata.order_id` value holds the Plateit order ID.

The payment will be logged accordingly and if all supporting-document requirements have been satisfied, the order will become Open; otherwise, it will remain in a draft state until those requirements have been completed.