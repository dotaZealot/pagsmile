---
description: How to use Pago46 to submit a payin in Chile.
---

# Pago46

## Payin by Pago46

<mark style="color:green;">`POST`</mark> `https://gateway-test.pagsmile.com/trade/pay`

This endpoint allows you to submit a payin by Pago46 in Chile.

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
| customer.identify.number<mark style="color:red;">\*</mark> | string | <p>User's identification number<br>- 9 digts -</p>                    |
| method<mark style="color:red;">\*</mark>                   | string | Fixed value: Pago46                                                   |
| out\_trade\_no<mark style="color:red;">\*</mark>           | string | <p>ID given by the merchant in their system<br>- Max. 64 chars - </p> |
| notify\_url<mark style="color:red;">\*</mark>              | string | Where Pagsmile will send notification to                              |
| customer.identify.type<mark style="color:red;">\*</mark>   | string | <p>User's identification type</p><p>- RUT or RUN -</p>                |
| customer.name<mark style="color:red;">\*</mark>            | string | User's name                                                           |
| timestamp<mark style="color:red;">\*</mark>                | string | <p>yyyy-MM-dd HH:mm:ss<br>- Max. 19 chars -</p>                       |
| subject<mark style="color:red;">\*</mark>                  | string | <p>payment reason or item title</p><p>- Max. 128 chars -</p>          |
| order\_amount<mark style="color:red;">\*</mark>            | string | <p>payment amount<br>- 1500 - 999,999 CLP -</p>                       |
| order\_currency<mark style="color:red;">\*</mark>          | string | Fixed value: CLP                                                      |
| content<mark style="color:red;">\*</mark>                  | string | <p>payment reason detail or item detail</p><p>- Max. 255 chars -</p>  |
| buyer\_id<mark style="color:red;">\*</mark>                | string | merchant user's id                                                    |
| address.zip\_code                                          | string | <p>zip code<br>- 7 digits -</p>                                       |
| website\_url                                               | string | <p>merchant website URL</p><p>- Max. 128 chars -</p>                  |
| address.street                                             | string | street                                                                |
| address.street\_number                                     | string | street number                                                         |
| address.city                                               | string | city                                                                  |
| address.state                                              | string | state                                                                 |
| return\_url                                                | string | Redirect to Merchant's url when user finished checkout                |

{% tabs %}
{% tab title="200 submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354006",
    "web_url": "",
    "pay_url": "https://app.payku.cl/gateway/",
    "trade_status": "PROCESSING"
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

## Example of identify

{% hint style="info" %}
* RUT / RUN numbers have eight digits, plus a verification digit, and are generally written in this format: xxxxxxxx-z. Z can be a digit or the letter K. For example 3\*\*\*\*\*\*7-K,  7\*\*\*\*\*\*8-5. **Only send alphanumeric values in the API**, like 3\*\*\*\*\*\*7K.
* For individuals, RUT is the same as RUN. For businesses, they only have RUT.
{% endhint %}

<table><thead><tr><th width="154">Identify Type</th><th width="160">Identify Number</th><th width="135">Description</th><th width="405"></th><th></th></tr></thead><tbody><tr><td>RUN</td><td>7******85</td><td>9 digits</td><td>A RUN <em>(Rol Único Nacional)</em> is a unique identification number given to every Chilean resident, foreign resident, and anyone who stays in Chile on anything other than a tourist visa</td><td></td></tr><tr><td>RUT</td><td>7******85</td><td>9 digits</td><td>A RUT <em>(Rol Único Tributario)</em> is the individual tax ID number</td><td></td></tr></tbody></table>

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354006",
    * "method": "Pago46",
    * "order_amount": "2500",
    * "order_currency": "CLP",
    * "subject": "trade pay test",
    * "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "customer" : {
    *     "identify": {
    *         "type": "RUT/RUN",
    *         "number": "220604497"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com",
    *     "phone": "56233145118"
      },
      "address" : {
          "zip_code": "3007601",
      }
      }'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
