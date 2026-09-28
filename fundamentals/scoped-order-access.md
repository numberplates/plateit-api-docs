# Scoped Order Access

Scoped order access provides a safer alternative to [general application authentication](/fundamentals/authentication.md) by granting temporary access to a single order only. It is intended to be used for public order tracking pages, where a customer may need to view the status and contents of their order and/or upload supporting documents.

## Requesting a Scoped Token

* Endpoint: `https://api.plateit.co.uk/v3/auth/scoped`
* Method: `POST`

### Request Attributes

* **company_id** `integer` Your company ID.
* **order_id** `integer` The ID of the order the customer wishes to access.
* **email** `string` The email address associated with the order.

### Example Request

```json
{
  "company_id": 1,
  "order_id": 123,
  "email": "customer@example.com"
}
```

### Example Response

```json
{
  "company_id": 1,
  "order_id": 123,
  "email": "customer@example.com",
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
  "expires_at": "2026-09-30T08:12:15.357157Z"
}
```

The returned `token` is a temporary JWT that should be supplied as a Bearer token when making subsequent API requests.

## Access Scope

A scoped token only grants access to the order it was issued for.

For a token issued for order `123`, read-only access is permitted to:

* `/v3/orders/123`
* `/v3/orders/123/*`

For example:

* `GET /v3/orders/123`
* `GET /v3/orders/123/packages`
* `GET /v3/orders/123/documents`

Requests outside of this order scope will be forbidden.

## Write Access

Scoped tokens are read-only with the exception of [supporting document uploads](/fundamentals/documents.md).

The following actions are permitted:

* `POST /v3/orders/123/documents/upload`
* `POST /v3/orders/123/documents`

The first endpoint returns a presigned upload URL.

The second finalises the upload by creating the document record and promoting the temporary asset.

!> All other write actions are forbidden.

## Expiry

Scoped tokens are temporary - they expire in 30 minutes.

The `expires_at` value returned when the token is created indicates when the token will stop being accepted by the API.

Once expired, a new scoped token must be requested.