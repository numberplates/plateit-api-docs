# NewEditSessionPlateUpdate

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/plates/{plate_id/new-edit-session`

Generates a JSON Web Token (JWT) that can be decrypted by your application to help assist with editing an existing number plate design.

It requires the `external_editor_endpoint` to be set in your company's General Settings.

For more information please see the [Editing Existing Plate Designs](/fundamentals/editing-existing-plate-designs.md) article.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/plates/{plate_id/new-edit-session`
* Method: `POST`

#### **Response**

* Status code: `200`

```json
{
  "url": "http://localhost:3000/staff-edit?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE3NDI0Njc4OTgsImNpZCI6MSwiZGlkIjoxLCJvaWQiOjMwMywicGlkIjo1NDgsInhpZCI6MTE5N30.ljY1mk1M3UhfHW89-PMIMhuSO-LqDoW46YiuTbiMyXQ"
}
```

#### **Decoded Token**

```json
{
  "exp": 1742467898,
  "cid": 1,
  "did": 1,
  "oid": 303,
  "pid": 548,
  "xid": 1197
}
```

<!-- tabs:end -->