---
description: How to use Baloto to submit a payin in Colombia.
---

# ❌ Baloto

{% hint style="danger" %}
Baloto no longer supported
{% endhint %}

## Payin by Baloto

<mark style="color:green;">`POST`</mark> `https://gateway-test.pagsmile.com/trade/pay`

This endpoint allows you to submit a payin by Baloto in Colombia.

#### Headers

| Name                                            | Type   | Description                           |
| ----------------------------------------------- | ------ | ------------------------------------- |
| Content-Type<mark style="color:red;">\*</mark>  | string | application/json; chartset=UTF-8      |
| Authorization<mark style="color:red;">\*</mark> | string | Basic Base($app\__id:$security\__key) |

#### Request Body

| Name                                                       | Type   | Description                                                           |
| ---------------------------------------------------------- | ------ | --------------------------------------------------------------------- |
| app\_id<mark style="color:red;">\*</mark>                  | string | <p>created app's id at dashboard</p><p>- Max. 32 chars -</p>          |
| customer.phone<mark style="color:red;">\*</mark>           | string | User's phone                                                          |
| customer.email<mark style="color:red;">\*</mark>           | string | User's email                                                          |
| customer.identify.number<mark style="color:red;">\*</mark> | string | <p>User's identification number<br>- 9 digits -</p>                   |
| method<mark style="color:red;">\*</mark>                   | string | Fixed value: Baloto                                                   |
| out\_trade\_no<mark style="color:red;">\*</mark>           | string | <p>ID given by the merchant in their system<br>- Max. 64 chars - </p> |
| notify\_url<mark style="color:red;">\*</mark>              | string | Where Pagsmile will send notification to                              |
| customer.identify.type<mark style="color:red;">\*</mark>   | string | <p>User's identification type</p><p>- NIT or CC -</p>                 |
| customer.name<mark style="color:red;">\*</mark>            | string | User's name                                                           |
| timestamp<mark style="color:red;">\*</mark>                | string | <p>yyyy-MM-dd HH:mm:ss<br>- Max. 19 chars -</p>                       |
| subject<mark style="color:red;">\*</mark>                  | string | <p>payment reason or item title</p><p>- Max. 128 chars -</p>          |
| order\_amount<mark style="color:red;">\*</mark>            | string | <p>payment amount<br>- 5,000~1,000,000 COP -</p>                      |
| order\_currency<mark style="color:red;">\*</mark>          | string | Fixed value: COP                                                      |
| content                                                    | string | <p>payment reason detail or item detail</p><p>- Max. 255 chars -</p>  |
| buyer\_id<mark style="color:red;">\*</mark>                | string | merchant user's id                                                    |
| address.zip\_code<mark style="color:red;">\*</mark>        | string | <p>zip code</p><p>- 6 digits -</p>                                    |
| website\_url                                               | string | <p>merchant website URL</p><p>- Max. 128 chars -</p>                  |
| address.street                                             | string | <p>street</p><p>- Required if zip_code not provide -</p>              |
| address.street\_number                                     | string | <p>street number</p><p>- Required if zip_code not provide -</p>       |
| address.city                                               | string | <p>city</p><p>- Required if zip_code not provide -</p>                |
| address.state                                              | string | <p>state<br>- Required if zip_code not provide -</p>                  |
| return\_url                                                | string | Redirect to Merchant's url when user finished checkout                |

{% tabs %}
{% tab title="200 submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id":"QVUvcG00ZDl6MFVsWkZsTk1IwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354005",
    "web_url": "",
    "pay_url": "https://checkout-testv2.pagsmile.com/checkout?prepay_id=QVUvcG0k1IUWVRVkxwRDlTZEdnVThOUGxyeHVnZkROND0=-D161Bae8",
    "trade_status": "PROCESSING",
    "reference":"85367736"
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

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    "app_id": "162************38",
    "out_trade_no": "202201010354005",
    "method": "Baloto",
    "order_amount": "5100",
    "order_currency": "COP",
    "subject": "trade pay test",
    "content": "trade pay test conent",
    "notify_url": "http://merchant/callback/success",
    "return_url": "https://www.merchant.com",
    "buyer_id": "buyer_0101_0001",
    "timestamp": "2022-01-01 03:54:01",
    "timeout_express":"1c",
    "customer" : {
        "identify": {
            "type": "NIT",
            "number": "502844147"
        },
        "name": "Test User Name",
        "email": "test@pagsmile.com",
        "phone": "3007654321"
    },
    "address" : {
        "zip_code": "300760",
    }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
