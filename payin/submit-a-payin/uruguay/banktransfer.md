---
description: How to use BankTransfer to submit a payin in Uruguay.
---

# ❌ Bank Transfer

## Payin by BankTransfer

<mark style="color:green;">`POST`</mark> `https://gateway-test.pagsmile.com/trade/pay`

This endpoint allows you to submit a payin by BankTransfer in Uruguay.

#### Headers

| Name                                            | Type   | Description                           |
| ----------------------------------------------- | ------ | ------------------------------------- |
| Content-Type<mark style="color:red;">\*</mark>  | string | application/json; chartset=UTF-8      |
| Authorization<mark style="color:red;">\*</mark> | string | Basic Base($app\__id:$security\__key) |

#### Request Body

| Name                                                       | Type   | Description                                                                      |
| ---------------------------------------------------------- | ------ | -------------------------------------------------------------------------------- |
| app\_id<mark style="color:red;">\*</mark>                  | string | <p>created app's id at dashboard</p><p>- Max. 32 chars -</p>                     |
| customer.phone                                             | string | User's phone                                                                     |
| customer.email<mark style="color:red;">\*</mark>           | string | User's email                                                                     |
| customer.identify.number<mark style="color:red;">\*</mark> | string | <p>User's identification number<br>- CI: 8 digits </p><p>   RUT: 12 digits -</p> |
| method<mark style="color:red;">\*</mark>                   | string | Fixed value: BankTransfer                                                        |
| out\_trade\_no<mark style="color:red;">\*</mark>           | string | <p>ID given by the merchant in their system<br>- Max. 64 chars - </p>            |
| notify\_url<mark style="color:red;">\*</mark>              | string | Where Pagsmile will send notification to                                         |
| customer.identify.type<mark style="color:red;">\*</mark>   | string | <p>User's identification type</p><p>- CI, RUT -</p>                              |
| customer.name<mark style="color:red;">\*</mark>            | string | User's name                                                                      |
| timestamp<mark style="color:red;">\*</mark>                | string | <p>yyyy-MM-dd HH:mm:ss<br>- Max. 19 chars -</p>                                  |
| subject<mark style="color:red;">\*</mark>                  | string | <p>payment reason or item title</p><p>- Max. 128 chars -</p>                     |
| order\_amount<mark style="color:red;">\*</mark>            | string | <p>payment amount<br>- 1 - 5,000,000 UYU -</p>                                   |
| order\_currency<mark style="color:red;">\*</mark>          | string | Fixed value: UYU                                                                 |
| content                                                    | string | <p>payment reason detail or item detail</p><p>- Max. 255 chars -</p>             |
| buyer\_id<mark style="color:red;">\*</mark>                | string | merchant user's id                                                               |
| address.zip\_code                                          | string | <p>zip code<br>- 5 digits -</p>                                                  |
| website\_url                                               | string | <p>merchant website URL</p><p>- Max. 128 chars -</p>                             |
| address.street                                             | string | street                                                                           |
| address.street\_number                                     | string | street number                                                                    |
| address.city                                               | string | city                                                                             |
| address.state                                              | string | state                                                                            |
| return\_url                                                | string | Redirect to Merchant's url when user finished checkout                           |
| account\_number<mark style="color:red;">\*</mark>          | string | User's bank account number                                                       |
| bank<mark style="color:red;">\*</mark>                     | string | Use [API](../../tools/supported-bank-list-query.md) to get bank code             |
| account\_type<mark style="color:red;">\*</mark>            | string | <p>User's bank account type</p><p>- One of: SAVINGS, CHECKING - </p>             |

{% tabs %}
{% tab title="200 submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010106532400030",
    "out_trade_no": "202201010354008",
    "web_url": "",
    "pay_url":"https://checkout-test.pagsmile.com/checkout?prepay_id=",
    "trade_status": "PROCESSING",
    "reference": "2901004200",
    "instruction":"{\"beneficiary\":{\"bank\":{\"code\":\"0013\",\"name\":\"BROU\",\"branch\":{\"code\":\"null\"},\"account\":{\"number\":\"110309016-00001\",\"type\":\"C\"}},\"document\":{\"id\":\"218730880015\",\"type\":\"RUT\"},\"name\":\"Pagsmile\",\"type\":\"INDIVIDUAL\"},\"referenceCode\":\"2209004197\"}"
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

* Take the recipient's bank details from the response parameter - "instruction" and present to users
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354008",
    * "method": "BankTransfer",
    * "order_amount": "50",
    * "order_currency": "UYU",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "bank":"1001",
    * "account_number":"11111111122222",
    * "account_type":CHECKING",
    * "customer" : {
    *    "identify": {
    *         "type": "CI",
    *         "number": "87417771"
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
