---
description: How to use Pagsmile Checkoutpage to submit a payin.
---

# Checkout Page (E-com)

## Payin by using Pagsmile checkout page

<mark style="color:green;">`POST`</mark> `https://gateway-test.pagsmile.com/trade/create`

This endpoint allows you to submit a payin by using Pagsmile checkout page

#### Headers

| Name                                            | Type   | Description                           |
| ----------------------------------------------- | ------ | ------------------------------------- |
| Content-Type<mark style="color:red;">\*</mark>  | string | application/json; chartset=UTF-8      |
| Authorization<mark style="color:red;">\*</mark> | string | Basic Base($app\__id:$security\__key) |

#### Request Body

| Name                                                              | Type   | Description                                                                                                                                                                                                                                |
| ----------------------------------------------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| app\_id<mark style="color:red;">\*</mark>                         | string | <p>created app's id at dashboard</p><p>- Max. 32 chars -</p>                                                                                                                                                                               |
| customer.identify.number<mark style="color:red;">\*</mark>        | string | User's identification number                                                                                                                                                                                                               |
| method                                                            | string | Add this object to show only the selected method. For instance, “method”: “PIX” will only show the PIX method. To show all the methods do not add this object in the request body. Check [here](../data/payment-method.md) for all methods |
| out\_trade\_no<mark style="color:red;">\*</mark>                  | string | <p>ID given by the merchant in their system<br>- Max. 64 chars - </p>                                                                                                                                                                      |
| notify\_url<mark style="color:red;">\*</mark>                     | string | Where Pagsmile will send notification to                                                                                                                                                                                                   |
| customer.identify.type<mark style="color:red;">\*</mark>          | string | <p>User's identification type</p><p>- check <a href="../data/data-for-test-sandbox.md#user-data">here</a> to check identify type for different countries -</p>                                                                             |
| timestamp<mark style="color:red;">\*</mark>                       | string | <p>yyyy-MM-dd HH:mm:ss<br>- Max. 19 chars -</p>                                                                                                                                                                                            |
| subject<mark style="color:red;">\*</mark>                         | string | <p>payment reason or item title</p><p>- Max. 128 chars -</p>                                                                                                                                                                               |
| order\_amount<mark style="color:red;">\*</mark>                   | string | <p>order amount<br>- 0.01 ~ 999999999 -</p><p>(refer to amount limit for different <a href="../data/payment-method.md">methods</a>)</p>                                                                                                    |
| order\_currency<mark style="color:red;">\*</mark>                 | string | <p>order currency<br>- Max. 3 chars -<br>Check <a href="../data/payment-method.md">here</a> for all methods.</p>                                                                                                                           |
| content<mark style="color:red;">\*</mark>                         | string | <p>payment reason detail or item detail. This will be shown on the bank bill.</p><p>- Max. 255 chars -</p>                                                                                                                                 |
| buyer\_id<mark style="color:red;">\*</mark>                       | string | merchant user's id                                                                                                                                                                                                                         |
| address.postal\_code<mark style="color:red;">\*</mark>            | string | zip code                                                                                                                                                                                                                                   |
| address.street<mark style="color:red;">\*</mark>                  | string | street                                                                                                                                                                                                                                     |
| address.street\_number<mark style="color:red;">\*</mark>          | string | street number                                                                                                                                                                                                                              |
| address.city<mark style="color:red;">\*</mark>                    | string | city                                                                                                                                                                                                                                       |
| address.state<mark style="color:red;">\*</mark>                   | string | state                                                                                                                                                                                                                                      |
| channel                                                           | string | only use when method = Wallet                                                                                                                                                                                                              |
| customer.phone<mark style="color:red;">\*</mark>                  | string | User's phone                                                                                                                                                                                                                               |
| customer.email<mark style="color:red;">\*</mark>                  | string | User's email                                                                                                                                                                                                                               |
| customer.name<mark style="color:red;">\*</mark>                   | string | User's name                                                                                                                                                                                                                                |
| address.country<mark style="color:red;">\*</mark>                 | string | country                                                                                                                                                                                                                                    |
| trade\_type<mark style="color:red;">\*</mark>                     | string | fixed value: WEB                                                                                                                                                                                                                           |
| billing.address.postal\_code<mark style="color:red;">\*</mark>    | string | billing zip code                                                                                                                                                                                                                           |
| billing.address.country<mark style="color:red;">\*</mark>         | string | billing country                                                                                                                                                                                                                            |
| billing.address.state<mark style="color:red;">\*</mark>           | string | billing state                                                                                                                                                                                                                              |
| billing.address.city<mark style="color:red;">\*</mark>            | string | billing city                                                                                                                                                                                                                               |
| billing.address.street<mark style="color:red;">\*</mark>          | string | billing street                                                                                                                                                                                                                             |
| billing.address.street\_number<mark style="color:red;">\*</mark>  | string | billing street number                                                                                                                                                                                                                      |
| billing.address.neighborhood<mark style="color:red;">\*</mark>    | string | billing neighborhood                                                                                                                                                                                                                       |
| billing.identification.number<mark style="color:red;">\*</mark>   | string | billing identify number                                                                                                                                                                                                                    |
| billing.identification.type<mark style="color:red;">\*</mark>     | string | billing identify type                                                                                                                                                                                                                      |
| address.neighborhood<mark style="color:red;">\*</mark>            | string | neighborhood                                                                                                                                                                                                                               |
| billing.phone<mark style="color:red;">\*</mark>                   | string | billing phone                                                                                                                                                                                                                              |
| billing.email<mark style="color:red;">\*</mark>                   | string | billing email                                                                                                                                                                                                                              |
| billing.name<mark style="color:red;">\*</mark>                    | string | billing name                                                                                                                                                                                                                               |
| shipping.address.street\_number<mark style="color:red;">\*</mark> | string | shipping street number                                                                                                                                                                                                                     |
| shipping.idenification.type<mark style="color:red;">\*</mark>     | string | shipping identify type                                                                                                                                                                                                                     |
| shipping.identification.number<mark style="color:red;">\*</mark>  | string | shipping identify number                                                                                                                                                                                                                   |
| shipping.address.neiborhood<mark style="color:red;">\*</mark>     | string | shipping neighborhood                                                                                                                                                                                                                      |
| shipping.address.street<mark style="color:red;">\*</mark>         | string | shipping street                                                                                                                                                                                                                            |
| shipping.address.city<mark style="color:red;">\*</mark>           | string | shipping city                                                                                                                                                                                                                              |
| shipping.address.state<mark style="color:red;">\*</mark>          | string | shipping state                                                                                                                                                                                                                             |
| shipping.address.country<mark style="color:red;">\*</mark>        | string | shipping country                                                                                                                                                                                                                           |
| shipping.address.postal\_code<mark style="color:red;">\*</mark>   | string | shipping zip code                                                                                                                                                                                                                          |
| shipping.phone<mark style="color:red;">\*</mark>                  | string | shipping phone                                                                                                                                                                                                                             |
| shipping.email<mark style="color:red;">\*</mark>                  | string | shipping email                                                                                                                                                                                                                             |
| shipping.name<mark style="color:red;">\*</mark>                   | string | shipping name                                                                                                                                                                                                                              |
| products.quanity<mark style="color:red;">\*</mark>                | string | product quantity                                                                                                                                                                                                                           |
| products.name<mark style="color:red;">\*</mark>                   | string | <p>product name<br>- Max. 200 chars -</p>                                                                                                                                                                                                  |
| products.url<mark style="color:red;">\*</mark>                    | string | <p>product url<br>- Max. 2000 chars -</p>                                                                                                                                                                                                  |
| products.description<mark style="color:red;">\*</mark>            | string | <p>product description<br>- Max. 1000 chars -</p>                                                                                                                                                                                          |
| return\_url                                                       | sring  | web redirect url when payment is finish                                                                                                                                                                                                    |
| timeout\_express                                                  | string | <p>m(minutes), h(hours), d(days), c(always end in current day). </p><p>Used to control the expiration time of <strong>submitting</strong> an order (from initial to processing).  (90m in default, max 15d)</p>                            |
| version<mark style="color:red;">\*</mark>                         | string | fixed value: 2.0                                                                                                                                                                                                                           |
| cancellation\_express                                             | string | <p>m(minutes), h(hours), d(days). The value must be an integer. </p><p>Used to cancel an order. Ex: 90m Used to control the expiration time of a processing order.</p>                                                                     |

{% tabs %}
{% tab title="200 submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354003",
    "web_url": "http://checkout.pagsmile.com?prepay_id=123456"
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
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/create' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
      "charset": "UTF-8",
    * "app_id": "162************38",
    * "out_trade_no": "202201010354002",
    * "order_currency": "BRL",
    * "order_amount": "12.01",
    * "subject": "item name",
    * "content": "20 item description",
    * "trade_type": "WEB",
      "timeout_express": "15d",
    * "timestamp": "2022-01-01 03:54:01",
    * "notify_url": "http://merchant/callback/success",
    * "buyer_id": "buyer_0101_0001",
    * "version": "2.0",
    * "customer" : {
    *     "identification": {
    *         "type": "CPF",
    *         "number": "50284414001"
        },
    *     "name": "customer user name",
    *     "email": "test@gmail.com",
    *     "phone": "5511987654321",
    * 	"buyer_id": "buyer_0101_0001",
        "ip": "127.0.0.1"
      },
    * "address":{
    * 	         "postal_code":"38082365",
    *            "country":"address test country",
    *            "state":"address state123",
    *            "city":"address city123",
    *            "street":"address streetqqq",
    *            "street_number":"4567",
    *            "neighborhood":"neighbor address222"
   			 },
    * "billing": {
    *     "address": {
    *            "postal_code":"38082365",
    *            "country":"billingtest country001",
    *            "state":"billingstate123",
    *            "city":"billingcity123",
    *            "street":"billingstreetqqq",
    *            "street_number":"22222",
    *            "neighborhood":"billingneighborhood222"
          },
    *     "identification": {
    *         "type": "cpf",
    *         "number": "50284414727"
        },
    *     "email": "email@test.com",
    *     "name": "test",
    *     "phone": "5511987654321"
      },
    * "shipping": {
    *     "address": {
    *            "postal_code":"38082365",
    *            "country":"Brazil",
    *            "state":"shipping state123",
    *            "city":"shipping city123",
    *            "street":"shipping streetqqq",
    *            "street_number":"4567",
    *            "neighborhood":"shipping hood222"
          },
    *     "identification": {
    *         "type": "cpf",
    *         "number": "50284414727"
          },
    *     "email": "email@test.com",
    *     "name": "test",
    *     "phone": "5511987654321"
      },
    * "products": [
          {
    *         "quantity": "1",
    *         "name": "product 1",
    *         "url": "https://www.pagsmile.com/product/1",
    *         "description": "this is a product"
          },
          {
           "quantity": "1",
           "name": "product 2",
           "url": "https://www.pagsmile.com/product/2",
           "description": "this is a product"
          },
          {
           "quantity": "3",
           "name": "product 3",
           "url": "https://www.pagsmile.com/product/3",
           "description": "this is a product"
        },
        {
           "quantity": "4",
            "name": "product 4",
            "url": "https://www.pagsmile.com/product/4",
            "description": "this is a product"
        }
    ]
}'
```

{% hint style="danger" %}
Return_url is not required in the request parameters. However if needed, you can overwrite it by appending the return\__url after the web\_url when redirect.&#x20;



`http://checkout.pagsmile.com?prepay_id={$prepay_id}`

↓↓↓

`http://checkout.pagsmile.com?prepay_id={$prepay_id}&return_url=encodeURIComponent({$return_url})`
{% endhint %}

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
