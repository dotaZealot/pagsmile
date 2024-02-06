---
description: How to submit a payout use Pagsmile Payout API.
---

# Submit a payout

{% swagger baseUrl="https://sandbox.transfersmile.com" path="/api/payout" method="post" summary="Request a payout" %}
{% swagger-description %}
This is the base method used to request a payout. Please note each country may have its own additional requirements and will have its own payment schedules, see below for more detailed examples.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="AppId" type="string" required="true" %}
Your App ID in payout platform
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
SHA256($sorted\_params + $merchant\_key)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
Beneficiary's name\
\- Max. 100 chars -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="string" %}
Beneficiary's phone
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Beneficiary's email
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="string" required="true" %}
Beneficiary's bank account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account_type" type="string" required="true" %}
Beneficiary's bank account type
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_id" type="string" required="true" %}
Beneficiary's personal identification number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="document_type" type="string" required="true" %}
Beneficiary's personal identification type
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" required="true" %}
Payout method
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channel" type="string" required="true" %}
Payout channel
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom_code" type="string" required="true" %}
Merchant Payout Id\
\- Max. 50 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fee_bear" type="string" required="true" %}
Processing fee charges to merchant or beneficiary.\
\- One of: merchant beneficiary -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" required="true" %}
Payout Amount\
\- Max. 2 decimal numbers -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="source_currency" type="string" required="true" %}
Merchant Account Currency\
\- Length: 3 chars -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="arrival_currency" type="string" required="true" %}
Local currency\
\- Length: 3 chars -&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notify_url" type="string" required="true" %}
Where pagsmile will send Notification to.\
\- Max. 128 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="additional_remark" type="string" required="true" %}
Additional Remark\
\- Max. 40(MEX) or 80(BRA) chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="country" type="string" required="true" %}
The user's country. ISO 3166-1 alpha-3 code\
\- Length: 3 chars -&#x20;
{% endswagger-parameter %}

{% swagger-response status="200" description="Request ok" %}
```
{
    "code": 200,
    "msg": "success",
    "time": 1628580845,
    "data": {
        "id": "S202108100734054iRiUZFPXfQM",
        "custom_code": "custom_code9982674851738108",
        "arrival_amount": "0.51",
        "arrival_currency": "MXN",
        "source_amount": "0.07",
        "source_currency": "USD",
        "status": "IN_PROCESSING"
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Countries

* [**Pagsmile Wallet**](pagsmile-wallet/)
  * More detailed examples for submitting a payout using Pagsmile Wallet.
* [**PayPal**](paypal/)
  * More detailed examples for submitting a payout using PayPal.
* [**Argentina**](../../payin/submit-a-payin/argentina/)
  * More detailed examples for submitting a payout in Argentina.
* [**Brazil**](brazil/)
  * More detailed examples for submitting a payout in Brazil.
* [**Chile**](../../payin/submit-a-payin/chile/)
  * More detailed examples for submitting a payout in Chile.
* [**Colombia**](colombia/wallet.md)
  * More detailed examples for submitting a payout in Colombia.
* [**Ecuador**](../../payin/submit-a-payin/ecuador/)
  * More detailed examples for submitting a payout in Ecuador.
* [**Mexico**](mexico/spei.md)
  * More detailed examples for submitting a payout in Mexico.
* [**Peru**](../../payin/submit-a-payin/peru/)
  * More detailed examples for submitting a payout in Peru.
* [<mark style="color:blue;">**Russia**</mark>](russia/)
  * More detailed examples for submitting a payout in Russia.
* [**Turkey**](turkey/)
  * More detailed examples for submitting a payout in Turkey.
* [**Uruguay**](uruguay/)
  * More detailed examples for submitting a payout in Uruguay.

