---
description: How to use SuRed to submit a payin in Colombia.
---

# SuRed

## Payin by SuRed

<mark style="color:green;">`POST`</mark> `https://gateway-test.pagsmile.com/trade/pay`

This endpoint allows you to submit a payin by SuRed in Colombia.

#### Headers

| Name                                            | Type   | Description                           |
| ----------------------------------------------- | ------ | ------------------------------------- |
| Content-Type<mark style="color:red;">\*</mark>  | string | application/json; chartset=UTF-8      |
| Authorization<mark style="color:red;">\*</mark> | string | Basic Base($app\__id:$security\__key) |

#### Request Body

| Name                                                       | Type   | Description                                                                   |
| ---------------------------------------------------------- | ------ | ----------------------------------------------------------------------------- |
| app\_id<mark style="color:red;">\*</mark>                  | string | <p>created app's id at dashboard</p><p>- Max. 32 chars -</p>                  |
| customer.phone                                             | string | User's phone                                                                  |
| customer.email<mark style="color:red;">\*</mark>           | string | User's email                                                                  |
| customer.identify.number<mark style="color:red;">\*</mark> | string | <p>User's identification number</p><p>- NIT: 10 digits, CC: 6~10 digits -</p> |
| method<mark style="color:red;">\*</mark>                   | string | Fixed value: SuRed                                                            |
| out\_trade\_no<mark style="color:red;">\*</mark>           | string | <p>ID given by the merchant in their system<br>- Max. 64 chars - </p>         |
| notify\_url<mark style="color:red;">\*</mark>              | string | Where Pagsmile will send notification to                                      |
| customer.identify.type<mark style="color:red;">\*</mark>   | string | <p>User's identification type</p><p>- NIT or CC -</p>                         |
| customer.name<mark style="color:red;">\*</mark>            | string | User's name                                                                   |
| timestamp<mark style="color:red;">\*</mark>                | string | <p>yyyy-MM-dd HH:mm:ss<br>- Max. 19 chars -</p>                               |
| subject<mark style="color:red;">\*</mark>                  | string | <p>payment reason or item title</p><p>- Max. 128 chars -</p>                  |
| order\_amount<mark style="color:red;">\*</mark>            | string | <p>payment amount<br>- 1,000~3,000,000 COP -</p>                              |
| order\_currency<mark style="color:red;">\*</mark>          | string | Fixed value: COP                                                              |
| content                                                    | string | <p>payment reason detail or item detail</p><p>- Max. 255 chars -</p>          |
| buyer\_id<mark style="color:red;">\*</mark>                | string | merchant user's id                                                            |
| address.zip\_code                                          | string | <p>zip code</p><p>- 6 digits -</p>                                            |
| website\_url                                               | string | <p>merchant website URL</p><p>- Max. 128 chars -</p>                          |
| address.street                                             | string | street                                                                        |
| address.street\_number                                     | string | street number                                                                 |
| address.city                                               | string | city                                                                          |
| address.state                                              | string | state                                                                         |
| return\_url                                                | string | Redirect to Merchant's url when user finished checkout                        |

{% tabs %}
{% tab title="200 submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id":"eG1HTm5PQm10TnBiWk5nd2MycjdNZXlZS282OWN0OEpmNXBXN2V1aTFzOD0=-48aB24cB",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354004",
    "web_url": "",
    "pay_url": "https://checkoutv2.pagsmile.com/checkout?prepay_id=eG1HTm5PQm10TnBiWk5nd2MycjdNZXlZS282OWN0OEpmNXBXN2V1aTFzOD0=-48aB24cB",
    "trade_status": "PROCESSING",
    "partner_code":"PAYVALIDA",
    "reference":"35972550"
}
```
{% endtab %}

{% tab title="400 duplicate out_trade_no" %}
```
{
    "code": "40002",
    "msg": "Business Failed",
    "sub_code": "duplicate-out_trade_no",
    "sub_msg": "out_trade_no is duplicate"
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**User payment tips**

Users need to use the **partner\_code** and **reference** to make payment at local store.
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354004",
    * "method": "SuRed",
    * "order_amount": "3000",
    * "order_currency": "COP",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "customer" : {
    *     "identify": {
    *         "type": "NIT",
    *         "number": "1234123121"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com"
      }
      }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
