# Editing Existing Plate Designs

!> This page is a stub. To be continued...

Plateit is design agnostic - it doesn't care what your plates look like. It will print whatever it recieves. Because of this, if a plate design needs editing at a later date, a round-trip needs to occur from Plateit to your application (where it is edited) and back again.

To achieve this, Plateit will send the user to a URL of your choosing with a JSON Web Token (JWT) appended in a query string. For example:

`https://example.com/make-changes?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NDI5MzAxMTksImNpZCI6MiwiZGlkIjoyLCJvaWQiOjM1NDYsInBpZCI6NDUzNCwieGlkIjoxMDM3Mn0.daf_6Ml_baiHC2OFcvaGIwrq61WunKeuTxDsVHAhrsY`

The token has encoded into it the following data:

* **exp** `integer` The expiry time of the token in Unix time (seconds from the epoch).
* **cid** `integer` The company ID the order belongs to.
* **did** `integer` The company ID responsible for manufacturing the plate/s (may be a delegated company ID).
* **oid** `integer` The related order ID.
* **pid** `integer` The related package ID.
* **xid**: `integer|null` The plate ID if the token corresponds to the editing of a specific plate, or null if creating a new plate.

The authenticity of the token can be verified against a shared secret known only to Plateit and your application. Your secret key can be set in your company's General Settings, available at [admin.plateit.co.uk](https://admin.plateit.co.uk).

### Token Verification

To verify the authenticity of the JWT, your application should follow these steps:

1. **Decode the JWT**: Use a JWT library compatible with your programming language to decode the token in the query string. This will allow you to access the payload data.

2. **Check the Signature**: Validate the token's signature using the shared secret. This step ensures that the token was issued by Plateit and has not been altered.

3. **Validate the Expiry**: Check the `exp` claim to ensure that the token has not expired. If the current time exceeds the expiry time, the token should be considered invalid.

4. **Extract Data**: Once the token is verified, extract the relevant data from the payload, such as the company, order and package IDs.

### Example Token Decoding

Here's an example PHP function to illustrate the decoding of the token using the [Firebase JWT Package](https://github.com/firebase/php-jwt). The equivalent package exists for most popular programming languages.

```php
use \Firebase\JWT\JWT;

/**
 * Decodes a JSON web token. It returns a stdClass and throws an Exception if
 * the token has expired.
 */
function decodeJwt($token, $secretKey)
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

} catch (\Exception $e) {
    echo 'Error: ' . $e->getMessage();
}
```

Once the data has been extracted, you can use a combination of your application's designer and the Plateit API to make the changes you require. Examples below.

### Creating a New Plate

Upon decoding the token, if the `xid` property is `null` (no existing plate ID), you know the user is intending to create a new [OrderPackagePlate](/objects/order-package-plate.md).

TBC...

### Editing an Exiting Plate

Upon decoding the token, if the `xid` (plate ID) property *is* set, you know the user is intending to edit an existing [OrderPackagePlate](/objects/order-package-plate.md).

TBC...