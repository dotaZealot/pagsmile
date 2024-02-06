---
description: How to use PSE to submit a payin in Colombia.
---

# PSE (Expired)

{% swagger baseUrl="https://gateway-test.pagsmile.com" path="/trade/pay" method="post" summary="Payin by PSE" %}
{% swagger-description %}
This endpoint allows you to submit a payin by PSE in Colombia.
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
Fixed value: PSE
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_currency" required="true" type="string" %}
Fixed value: COP
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_amount" required="true" type="string" %}
payment amount\
\- 2,000\~3,000,000 COP -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="subject" required="true" type="string" %}
payment reason or item title

\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="string" %}
payment reason detail or item detail

\- Max. 255 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where Pagsmile will send notification to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="return_url" type="string" %}
Redirect to Merchant's url when user finished checkout. **Doesn't work on provider's page.**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buyer_id" required="true" type="string" %}
merchant user's id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.name" type="string" required="true" %}
User's name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.phone" type="string" required="true" %}
User's phone
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.email" type="string" required="true" %}
User's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.number" type="string" required="true" %}
User's identification number\
\- 9 digits -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customer.identify.type" type="string" required="true" %}
User's identification type

\- NIT or CC -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address.zip_code" required="false" type="string" %}
zip code

\- 6 digits -
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
    "out_trade_no": "202201010354005",
    "web_url": "",
    "pay_url": "https://secure.payty.com/vads-payment/",
    "trade_status": "PROCESSING",
    "form_date": {
        "vads_payment_cards": "VISA;PSE",
        "signature": "tOqEo5HHvjnMk0Z+w2ROGNSKWY1uid5avqHoN6JF8MU=",
        "vads_trans_date": "20220101035405",
        "vads_ctx_mode": "TEST",
        "vads_action_mode": "INTERACTIVE",
        "vads_page_action": "PAYMENT",
        "vads_order_description": "trade pay test conent",
        "vads_order_id": "2022010110293900083",
        "vads_currency": "170",
        "vads_version": "V2",
        "vads_trans_id": "10rbcg",
        "vads_amount": 200000,
        "vads_payment_config": "SINGLE",
        "vads_site_id": "10454805"
    }
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

{% hint style="danger" %}
This integration process is expired. Please check the [updated page](pse.md).
{% endhint %}

#### Merchant need to use the data in the response to redirect users to payment page

```
<input type="button" id="button1" onclick="pay()" value="Test" />

<script type="text/javascript">
    function pay() {
        var pay_url = "https://secure.payty.com/vads-payment/";
        var form_date = {
            "vads_payment_cards": "VISA;PSE",
            "signature": "tOqEo5HHvjnMk0Z+w2ROGNSKWY1uid5avqHoN6JF8MU=",
            "vads_trans_date": "20220101035405",
            "vads_ctx_mode": "TEST",
            "vads_action_mode": "INTERACTIVE",
            "vads_page_action": "PAYMENT",
            "vads_order_description": "trade pay test conent",
            "vads_order_id": "2022010110293900083",
            "vads_currency": "170",
            "vads_version": "V2",
            "vads_trans_id": "10rbcg",
            "vads_amount": 200000,
            "vads_payment_config": "SINGLE",
            "vads_site_id": "10454805"
        }
        
        location.href = pay_url + "?" + Object.keys(form_date)?.map((k) => `${encodeURIComponent(k)}=${encodeURIComponent(form_date[k])}`).join("&");
    }
</script> 
```

{% hint style="info" %}
**User payment tips**

When the user submitted the payment on the redirected page, the money will be transferred and the payment will be confirmed instantly.
{% endhint %}

## Example

```
curl --location --request POST 'https://gateway-test.pagsmile.com/trade/pay' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "out_trade_no": "202201010354005",
    * "method": "PSE",
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
    *         "number": "502844147"
          },
    *     "name": "Test User Name",
    *     "email": "test@pagsmile.com",
    *     "phone": "3007654321"
      },
      "address" : {
          "zip_code": "300760",
      }
      }'
```

![User payment page](<../../../.gitbook/assets/image (14).png>)

![Success payment page](<../../../.gitbook/assets/image (4).png>)

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
