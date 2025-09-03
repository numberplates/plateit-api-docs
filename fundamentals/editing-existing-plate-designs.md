# Editing Existing Plate Designs

Plateit is design agnostic - it doesn't care what your plates look like. It will print whatever it recieves. Because of this, if a plate design needs editing at a later date, a round-trip needs to occur from Plateit to your application (where it is edited) and back again.

!> This can only be achieved if you are saving your number plate designer's `design_object` (design metadata) to your [OrderPackagePlate](/objects/order-package-plate.md) objects.

You will need a [CompanyAccessToken](/objects/company-access-token.md) with the following permissions:

* `orders_read`
* `company_plate_types_read`
* `orders_packages_plates_write`

You will also need the `external_editor_endpoint` to be set in your company's General Settings.

## How it Works

When you want to edit an existing [OrderPackagePlate](/objects/order-package-plate.md) (or create a new one for an existing package), Plateit will send the user to a URL of your choosing with a JSON Web Token (JWT) included in a query string under the `token` key. For example:

`https://example.com/make-changes?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NDI5MzAxMTksImNpZCI6MiwiZGlkIjoyLCJvaWQiOjM1NDYsInBpZCI6NDUzNCwieGlkIjoxMDM3Mn0.daf_6Ml_baiHC2OFcvaGIwrq61WunKeuTxDsVHAhrsY`

A token can be generated with either of the following helper endpoints, depending on your intention:

* [NewEditSessionPlateCreate](/helpers/new-edit-session-plate-create.md)
* [NewEditSessionPlateUpdate](/helpers/new-edit-session-plate-update.md)

The token has encoded into it the following data:

* **exp** `integer` The expiry time of the token in Unix time (seconds from the epoch).
* **cid** `integer` The company ID the order belongs to.
* **did** `integer` The company ID responsible for manufacturing the plate/s (may be the same as the company ID or a different, delegated, company ID).
* **oid** `integer` The related order ID.
* **pid** `integer` The related package ID.
* **xid**: `integer|null` The plate ID if the token corresponds to the editing of a specific plate, or null if creating a new plate.

The data encoded into the token can be used to create new plates for an existing package or to edit an existing plate.

!> Each JWT is valid for 30 minutes.

> The authenticity of the token can be verified against a shared secret known only to Plateit and your application. Your secret key can be set in your company's General Settings, available at [admin.plateit.co.uk](https://admin.plateit.co.uk).

## Token Verification

To verify the authenticity of the JWT, your application should follow these steps:

1. **Decode the JWT**: Use a JWT library compatible with your programming language to decode the token in the query string. This will allow you to access the payload data.

2. **Check the Signature**: Validate the token's signature using the shared secret. This step ensures that the token was issued by Plateit and has not been altered.

3. **Validate the Expiry**: Check the `exp` claim to ensure that the token has not expired. If the current time exceeds the expiry time, the token should be considered invalid.

4. **Extract Data**: Once the token is verified, extract the relevant data from the payload, such as the company, order and package IDs.

## Example Token Decoding

!> Always decode the JWT on the server to avoid leaking the secret key.

Here's an example PHP function to illustrate the decoding of the token using the [Firebase JWT Package](https://github.com/firebase/php-jwt). (Equivalent packages exist for most popular programming languages.)

```php
use \Firebase\JWT\JWT;

/**
 * Decodes a JSON web token. It returns a stdClass and throws an Exception if
 * the token has expired.
 */
function decodeJwt($token, $secretKey) : stdClass
{
    try {
        $decoded = JWT::decode($token, $secretKey, ['HS256']);
        $exp = $decoded->exp;
        $currentTime = time();

        if ($exp < $currentTime) {
            throw new \Exception('Token has expired');
        }
        
        return $decoded;

    } catch (\Exception $e) {
        throw new \Exception('Error decoding token: ' . $e->getMessage());
    }
}
```

Using the above function you can extract the pertinent data from the token like so:

```php
// Define the secret key set in your Plateit company settings.
$secretKey = 'your-shared-secret-key';

// Obtain the token from the query params.
$token = $_GET['token'];

// Decode the token and grab the pertinent data from it.
try {
    $tokenData = decodeJwt($token, $secretKey);

    $companyId          = $tokenData->cid;
    $delegatedCompanyId = $tokenData->did;
    $orderId            = $tokenData->oid;
    $packageId          = $tokenData->pid;
    $plateId            = $tokenData->xid;

    // Do something with data here...

} catch (\Exception $e) {
    echo 'Error: ' . $e->getMessage();
}
```

Once the data has been extracted, you can use a combination of your application's graphical number plate designer and the Plateit API to make the changes you require. Instructions below.

## Creating a New Plate

Upon decoding the JWT, if the `xid` property is `null` (no existing plate ID), you know the user is intending to create a new [OrderPackagePlate](/objects/order-package-plate.md) for a specific package.

From here you would:

1. Fetch the available [CompanyPlate](/objects/company-plate.md) objects with their relationships (as per [this example](/fundamentals/suggested-integration.md?id=fetching-available-plates)). *
2. Use the fetched data to dynamically build your graphical number plate designer.
3. Create the new plate by sending the finished payload in a `POST` request to the [OrderPackagePlate](/objects/order-package-plate.md) (creation) endpoint constructed using the data obtained from the decoded JWT.

> *If the `did` property (delegated company ID) differs from the `cid` property (the company ID), you will need to fetch the delegated company's CompanyPlate objects and not yours. See [this section](/fundamentals/delegations?id=retrieving-available-foreign-items) of the delegations guide for more information.

## Editing an Existing Plate

Upon decoding the token, if the `xid` (plate ID) property is set, you know the user is intending to edit an existing [OrderPackagePlate](/objects/order-package-plate.md).

From here you would:

1. Fetch the available [CompanyPlate](/objects/company-plate.md) objects with their relationships (as per [this example](/fundamentals/suggested-integration.md?id=fetching-available-plates)). *
2. Use the fetched data to dynamically build your graphical number plate designer.
3. Fetch the [OrderPackagePlate](/objects/order-package-plate.md) the user intends to edit.
4. Extract the plate's `design_object` (design metadata).
5. Import the `design_object` into your designer, allowing the user to make their changes.
6. Update the plate by sending the finished payload in a `PATCH` request to the [OrderPackagePlate](/objects/order-package-plate.md) (update) endpoint constructed using the data obtained from the decoded JWT.

> *If the `did` property (delegated company ID) differs from the `cid` property (the company ID), you will need to fetch the delegated company's CompanyPlate objects and not yours. See [this section](/fundamentals/delegations?id=retrieving-available-foreign-items) of the delegations guide for more information.