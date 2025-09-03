# FormatRegistration

`https://api.plateit.co.uk/v3/actions/format-registration`

This helper endpoint assists with formatting registration strings. It converts the input to uppercase and inserts a space at the correct, legal position.

Additionally, it includes a character correction feature that identifies and rectifies common confusions between similar-looking characters, such as `O` and `0`, and `I` and `1`.

!> If the registration is not legal, an HTTP error will be returned.

## Example Request

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://api.plateit.co.uk/v3/actions/format-registration`
* Method: `POST`

```json
{
  "registration": "pb79xyz"
}
```

#### **Response**

* Status code: `200`

```json
{
  "registration": "PB79 XYZ"
}
```

<!-- tabs:end -->