---
description: How to use OXXOPay to submit a payin in Mexico.
---

# OXXOPay

## Payin by OXXOPay

<mark style="color:green;">`POST`</mark> `https://gateway-test.pagsmile.com/trade/pay`

This endpoint allows you to submit a payin by OXXOPay in Mexico.

#### Headers

| Name                                            | Type   | Description                           |
| ----------------------------------------------- | ------ | ------------------------------------- |
| Content-Type<mark style="color:red;">\*</mark>  | string | application/json; chartset=UTF-8      |
| Authorization<mark style="color:red;">\*</mark> | string | Basic Base($app\__id:$security\__key) |

#### Request Body

| Name                                                       | Type   | Description                                                                                    |
| ---------------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------- |
| app\_id<mark style="color:red;">\*</mark>                  | string | <p>created app's id at dashboard</p><p>- Max. 32 chars -</p>                                   |
| customer.phone<mark style="color:red;">\*</mark>           | string | User's phone                                                                                   |
| customer.email<mark style="color:red;">\*</mark>           | string | User's email                                                                                   |
| customer.identify.number<mark style="color:red;">\*</mark> | string | <p>User's identification number</p><p>- RFC: 13 chars, ex: MAMB780915969; CURP: 18 chars -</p> |
| method<mark style="color:red;">\*</mark>                   | string | Fixed value: OXXOPay                                                                           |
| out\_trade\_no<mark style="color:red;">\*</mark>           | string | <p>ID given by the merchant in their system<br>- Max. 64 chars - </p>                          |
| notify\_url<mark style="color:red;">\*</mark>              | string | Where Pagsmile will send notification to                                                       |
| customer.identify.type<mark style="color:red;">\*</mark>   | string | <p>User's identification type</p><p>- RFC or CURP -</p>                                        |
| customer.name<mark style="color:red;">\*</mark>            | string | User's name                                                                                    |
| timestamp<mark style="color:red;">\*</mark>                | string | <p>yyyy-MM-dd HH:mm:ss<br>- Max. 19 chars -</p>                                                |
| subject<mark style="color:red;">\*</mark>                  | string | <p>payment reason or item title</p><p>- Max. 128 chars -</p>                                   |
| order\_amount<mark style="color:red;">\*</mark>            | string | <p>payment amount<br>- 10 ~ 9,999 MXN -</p>                                                    |
| order\_currency<mark style="color:red;">\*</mark>          | string | Fixed value: MXN                                                                               |
| content                                                    | string | <p>payment reason detail or item detail</p><p>- Max. 255 chars -</p>                           |
| buyer\_id<mark style="color:red;">\*</mark>                | string | merchant user's id                                                                             |
| address.zip\_code                                          | string | <p>zip code</p><p>- 5 digits -</p>                                                             |
| website\_url                                               | string | <p>merchant website URL</p><p>- Max. 128 chars -</p>                                           |
| address.street                                             | string | street                                                                                         |
| address.street\_number                                     | string | street number                                                                                  |
| address.city                                               | string | city                                                                                           |
| address.state                                              | string | state                                                                                          |
| return\_url                                                | string | Redirect to Merchant's url when user finished checkout                                         |

{% tabs %}
{% tab title="200 submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "prepay_id":"Q3hnR2hieXRxS3BrbnpmZWRPUXV2Znp3MG1xRHhxejB3VWZ6M2xLaDI5RT0=-76553c77",
    "trade_no": "2022010110293900084",
    "out_trade_no": "202201010354004",
    "web_url": "",
    "barcode": "88644659044520042000028006",
    "pay_url": "https://checkout-testv2.pagsmile.com/checkout?prepay_id=R3FmamNKOTI2bXRnNW41aHZBNUI2U0JFMitSeWlDdTVUMWN3TE5EWGF6Zz0=-8B62e5F4",
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

{% hint style="info" %}
**User payment tips**

* OXXOPay is a faster option of OXXO which can be confirmed in real-time
* **barcode** is the ticket number that the user needs to use for payment
* Providing a locator could help the user to find a store faster. Can link it to [https://www.google.com/maps/search/oxxo/](https://www.google.com/maps/search/oxxo/)
* Providing a downloadable PDF version could help mobile users to have their tickets on their phones without keeping the browser open.
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354004",
    * "method": "OXXOPay",
    * "order_amount": "12.01",
    * "order_currency": "MXN",
    * "subject": "trade pay test",
      "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "customer" : {
    *     "identify": {
    *         "type": "RFC",
    *         "number": "MAMB780915969"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com",
    *     "phone": "523135759140"
      },
      "address" : {
          "zip_code": "37900",
      }
      }'
```

![Example of payment page](<../../../.gitbook/assets/image (16).png>)

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
