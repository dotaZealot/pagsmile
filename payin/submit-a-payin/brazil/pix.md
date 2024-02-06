---
description: How to use Pix to submit a payin in Brazil.
---

# Pix

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by Pix" %}
{% swagger-description %}
This endpoint allows you to submit a payin by Pix in Brazil.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic Base($app\__id:$security\__key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="app_id" type="string" required="true" %}
created app's id at dashboard

\- Max. 32 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" required="true" type="string" %}
yyyy-MM-dd HH:mm:ss\
\- Max. 19 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="out_trade_no" type="string" required="true" %}
ID given by the merchant in their system\
\- Max. 64 chars -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Fixed value: PIX
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
Fixed value: BRL&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 0.1\~50,000 BRL -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="subject" required="true" type="string" %}
payment reason or item title

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="string" required="false" %}
payment reason detail or item detail.&#x20;

\- Max. 255 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where Pagsmile will send notification to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="return_url" type="string" %}
Redirect to Merchant's url when user finished checkout
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancellation_express" type="string" %}
m(minutes), h(hours), d(days).\
The value must be an integer. Ex: 90m\
Used to control the expiration of QR code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_id" required="true" type="string" %}
merchant user's id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.name" type="string" required="true" %}
User's name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.phone" type="string" required="false" %}
User's phone
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" required="true" %}
User's identification number

\- 11 digits if CPF or 14 digits if CNPJ -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- CPF or CNPJ -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" required="false" type="string" %}
zip code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.state" type="string" %}
state
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.city" type="string" %}
city
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.street_number" type="string" %}
street number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.street" type="string" %}
street
{% endswagger-parameter %}

{% swagger-parameter in="body" name="website_url" type="string" %}
merchant website URL

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-response status="200" description="submit successfully" %}
```
{
    "code": "10000",
    "msg": "Success",
    "trade_no": "2022010110293900083",
    "out_trade_no": "202201010354003",
    "web_url": "",
    "pay_url": "https://checkout.pagsmile.com/checkout?prepay_id=TTd5Y1JJbDhKbi9Rd1NPNkZTUVIyNGNsOEFyRWZ4SWw1czd2UE00bmszOD0=-79697e50",
    "trade_status": "PROCESSING",
    "qr_code": "00020126580014br.gov.bcb.pix013627a44d0a-0736-4bbf-a4a4-6e11063973315204000053039865406100.005802BR5908PAGSMILE6008So Paulo62230519mpqrinter123742074363049E0B",
    "qr_code_url": "https://gateway.pagsmile.com/api/trade/qrcode-img?prepay_id=Y1N5dHVPOFJ4Ky9lZVVKVXBrdFFieWttVlhwSGZWMnJYRXBkWW9OaE8wRT0=-9036acF1",
    "qr_code_img": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAADIAQAAAACFI5MzAAACwUlEQVR42u2XPc7jIBCGx6Kgsy+AxDXouFJyAf9cIL4SHdewxAXsjgJ59p2sFPsrtlhodqVEkQs/UcDz8zAm/tOHvuRL/hkSqOM0O375tLttiES6gUQ+ouky76RWpoe2uNNA6IkbntdQiNKpTddIglpyOr3ibHrfTDKf3s5kd+KVGwliUKasFjYT4wl+RudvCfITzfP6/sjcXxN88jY6i3UelN6LNJBAD8JOcVXMZaT08g0kq5cncrzm8gyld6qJBLtkM2q7e1SiGeKVnxqSFbY8ZPtyW68RA+p1Awlbxxa1c8T0Dqrdm4g6tV0RV512jXDa2TcQ5pm2Ea0mG8c6/KnEGpKRYYW9P6hIwjOvLQQyIJoQ1IAtl1Gro4VEmoLdYT69PXxa81U7NQT7deLRI0gM0HNDbCAiA6wAKxsxn6OBWwjvkpx0hHRw6aK9YlBBsl3f5ns5XvImBe4bSICcTMdqFh+YZ7hFp4JAn0Ht6BLxMfqvNBE4Xm7ApsgzbiNFDSRvKEO4Cu37ZBR1uUxRQcJG2r7PH6xjukBjE+FTo5ztEjco4dQ40BpI5vcxa6Vxc3m4W+1UEDY9mQE5l14po1OXqyoIKpqxcRyzcsV88cl2DWFp3En6WHpuDTcnVpDIs5eEwwq7Q6rhrQbC+G8FuzA6OIpE1yaidpcWZIkhPzl/Zt1AcnoRH4wr+gM/KR9X1RBG725w1RLTu3Zu9q8gQbp29HYJCG3p/W12qSDy9DRxQmhhwdnfqqqG4Nw2MosFaC8tIX1msRqCo0wGOiJSJ85Got43EIHmt6vkFNJlbCGYYQOOa2gASoBTb1NaBcF8DX3CVQwxpx+OryF4k8BOZfY/3TYFerYShVkMj35keQP7OL6WWARywDjAmGSvab2KYDZRiCXiitqZ8eYUG4jkR2pniHCVIXSJbiDfN/4v+T/JL/qJUR2nh9cdAAAAAElFTkSuQmCC"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="duplicate out_trade_no" %}
```
{
    "code": "40002",
    "msg": "Business Failed",
    "sub_code": "duplicate-out_trade_no",
    "sub_msg": "out_trade_no is duplicate"
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
**User payment tips**

* Users only need to scan the QR code to finish the payment. QR code can be generated with **qr\_code** value.
* Add a Copy QRCODE button. For mobile users, they can copy the string of **qr\_code** and paste it into their wallet app to finish the payment. Adding a copy button could help to improve the user's payment experience.&#x20;
* **qr\_code\_url** and **qr\_code\_img** are system generated images of qr code which can be used directly on merchant website depending on needs.
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354002",
    * "method": "PIX",
    * "order_amount": "12.01",
    * "order_currency": "BRL",
    * "subject": "trade pay test",
    * "content": "trade pay test conent",
    * "notify_url": "http://merchant/callback/success",
      "return_url": "https://www.merchant.com",
    * "buyer_id": "buyer_0101_0001",
    * "timestamp": "2022-01-01 03:54:01",
      "timeout_express":"1c",
    * "customer" : {
    *     "identify": {
    *         "type": "CPF",
    *         "number": "11032341882"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com"
      }
      }'
```

![Example of payment page](<../../../.gitbook/assets/image (7).png>)

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
