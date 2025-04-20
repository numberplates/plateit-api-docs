# PayPal

Plateit is able to keep track of payments and refunds made using PayPal providing it is set up correctly to do so.

1. Log into [https://developer.paypal.com](https://developer.paypal.com) and create a new REST API application.
2. Create a new Webhook for your application and point it to: `https://data.plateit.co.uk/v3/webhooks/paypal` ensuring the event types `PAYMENT.CAPTURE.COMPLETED` and `PAYMENT.CAPTURE.REFUNDED` are selected.
3. Save the application's *Client Key* and *Secret Key* inside your company settings along with your newly created PayPal *Webhook ID*.

You are now half way there to keeping Plateit in sync with your PayPal account.

The next thing you need to ensure is that your front-end application (website) utilises the same PayPal API keys to create and capture payments from your customers.

PayPal payments can take an `invoice_id` parameter. **Ensure this is populated with the order ID returned from the [BuildOrder](/helpers/build-order.md) endpoint.**

When a PayPal order has been successfully created and captured, a webhook will be sent to Plateit by PayPal. Plateit will know which order the payment pertains to because the `invoice_id` value holds the Plateit order ID.

The payment will be logged accordingly and the status of the order will be updated from `External Draft` to `Open`.

> Note: If you create a page where customers can pay an outstanding balance at a later date, you will get a PayPal error if a previous payment has already been made with PayPal pertaining to that order. This is because the `invoice_id` (Plateit's order ID) has already been used. This catch can be turned off inside PayPal under *account settings -> payment preferences -> block payments*. Select *"allow multiple payments per invoice id"*. 