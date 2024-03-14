---
description: How to get token to create CreditCard orders in Brazil.
---

# Tokenization

{% swagger method="post" path="/card/token/" baseUrl="https://security-test.pagsmile.com" summary="Tokenization" %}
{% swagger-description %}
This endpoint allows you to get token to create CreditCard orders.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; chartset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="app_id" required="true" %}
created app's id at dashboard

\- Max. 32 chars -
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="string" required="true" %}
yyyy-MM-dd HH:mm:ss\
\- Max. 19 chars -
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="string" %}
Basic Base($app\__id:$security\__key)
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="card.card_no" required="true" %}
card number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card.holder.name" required="true" type="string" %}
holder name
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="card.issuer" required="false" %}
visa, mastercard...
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card.holder.identification.type" required="false" type="string" %}
holder id type
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card.holder.identification.number" required="false" type="string" %}
holder id number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card.cvv" required="true" type="string" %}
security code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card.valid_thru_year" required="true" type="string" %}
expiration year (4 digits)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card.valid_thru_month" required="true" type="string" %}
expiration month (2 digits)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="submit successfully" %}
```json
{
    "code": "10000",
    "msg": "Success",
    "token": "psct_1bd2****73c91",
    "valid_thru_year": "2***",
    "valid_thru_month": "09",
    "card_number_length": 16,
    "first_six_digits": "5***2",
    "last_four_digits": "***4",
    "security_code_length": 3,
    "holder": {
        "identification": {} //The identification will be returned when it was sent in the request
    },
    "created": 1710313784,
    "card_number": "51**94",
    "security_code": "****"
}

```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="invalid signature" %}
```json
{
    "code":"40002",
    "msg":"Business Failed",
    "sub_code":"invalid-signature",
    "sub_msg":"invalid signature"
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="success" %}
The URL for production is: [https://security.pagsmile.com/card/token/](https://security.pagsmile.com/card/token/)
{% endhint %}

### Example

```
curl --location --request POST 'https://security-test.pagsmile.com/card/token' \
--header 'Authorization: Basic MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "app_id": "162************38",
    * "timestamp": "2022-01-01 03:54:01",
    * "card": {
    *     "card_no": "",
          "issuer": "visa", 
          "holder": {
              "name": "Test User Name",
              "identification": {
                  "type": "CPF",
                  "number": "50284414727"
              }
          },
    *     "cvv": "",
    *     "valid_thru_year": "",
    *     "valid_thru_month": ""
      }
}'
```

{% hint style="info" %}
Note:  **162\*\*\*\*\*\*\*\*\*\*\*\*38** is pagsmile's test app id for sandbox, and **MTYyNTgyOTIxNDUzMTY2Mzg6UGFnc21pbGVfc2tfZDUwMWQ1ZGNkNTI5OGQ5N2MwNmUzYjI4YjA2OWZjZmY3NDU5ZjY2NzNiMjFjMTFlYTY3NDM5MDgzOTZkOTYxNQ==** is authorization token associated with the test app id.&#x20;
{% endhint %}

{% hint style="danger" %}
Please use your own **app\_id** and generate your own **authorization token** when testing.
{% endhint %}
