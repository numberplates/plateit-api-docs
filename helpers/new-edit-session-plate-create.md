# NewEditSessionPlateCreate

`https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/plates/new-edit-session`

!> This page is a stub. To be continued...

## Example Request

!> Requires the `company_plates_write` permission.

<!-- tabs:start -->

#### **Request**

* Endpoint: `https://data.plateit.co.uk/v3/orders/{order_id}/packages/{package_id}/plates/new-edit-session`
* Method: `POST`

#### **Response**

* Status code: `200`

```json
{
  "url": "https://example.com/staff-edit?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE3NDI0NjY4NTcsImNpZCI6MSwiZGlkIjoxLCJvaWQiOjMwMywicGlkIjo1NDgsInhpZCI6bnVsbH0.sc23RLHnI6uWYfD-Wi-W98HCfu_JP8Jwfo2BY14948k"
}
```

#### **Decoded Token**

```json
{
  "exp": 1742466857,
  "cid": 1,
  "did": 1,
  "oid": 303,
  "pid": 548,
  "xid": null
}
```

<!-- tabs:end -->