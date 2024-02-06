---
description: Data for auto process payout in sandbox environment
---

# Data for test

### Argentina

#### Banktransfer

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name":"test name",
    "phone": "91111111111",
    "email": "test@test.com",
    "bank_code": "072",
    "account_type": "SAVINGS",
    "account": "0721111111111111111111", //test PAID. Process in 1 day
    "document_type" : "CUIT",
    "document_id": "22222222222",
    "fee_bear": "merchant",
    "amount": "100",
    "source_currency": "USD",
    "arrival_currency": "ARS",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "custom_code31195387357700_t04N",
    "additional_remark": "banktransfer payout request",
    "country": "ARG",
    "method": "BANKTRANSFER"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
}
```
{% endtab %}
{% endtabs %}

***

### Brazil

#### PIX

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "account_type": "Email",
    "account": "pagsmile_test_paid@pagsmile.com", //test PAID.
    "document_type": "CPF",
    "document_id": "11032341882",
    "fee_bear": "merchant",
    "amount": "10",
    "source_currency": "USD",
    "arrival_currency": "BRL",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "custom_code31195387357700_t04N",
    "additional_remark": "pix payout request",
    "country": "BRA",
    "method": "PIX"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name",
    "account_type": "Email",
    "account": "pagsmile_test_reject@pagsmile.com", //test REJECTED.
    "document_type": "CPF",
    "document_id": "11032341882",
    "fee_bear": "merchant",
    "amount": "10",
    "source_currency": "USD",
    "arrival_currency": "BRL",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "custom_code31195387357700_t04N",
    "additional_remark": "pix payout request",
    "country": "BRA",
    "method": "PIX"
}
```
{% endtab %}
{% endtabs %}

#### BankTransfer

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "bank_code": "001",
    "branch": "0002",
    "account_type": "CHECKING",
    "account": "22222222", //test PAID. Process in 10 minutes
    "document_type": "CPF",
    "document_id": "50284414727",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "BRL",
    "account_digit": "1",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "custom_code31195387357700_t04N",
    "additional_remark": "banktransfer payout request",
    "country": "BRA",
    "method": "BANKTRANSFER"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name",
    "bank_code": "001",
    "branch": "0002",
    "account_type": "CHECKING",
    "account": "11111111", //test REJECTED. Process in 10 minutes
    "document_type": "CPF",
    "document_id": "50284414727",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "BRL",
    "account_digit": "1",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "custom_code31195387357700_t04N",
    "additional_remark": "banktransfer payout request",
    "country": "BRA",
    "method": "BANKTRANSFER"
}
```
{% endtab %}
{% endtabs %}

***

### Mexico

#### SPEI

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "phone": "111111111111",
    "email": "test@pagsmile.com",
    "bank_code": "90646",
    "account": "646020146401877826", //test PAID. Process in 10 minutes
    "account_type": "clabe",
    "document_id": "MAMB780915969",
    "document_type": "RFC",
    "method": "SPEI",
    "custom_code" : "31443964215700_bqSE",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "MXN",
    "notify_url" : "https://sandbox.transfersmile.com/api/notify/demo",
    "additional_remark": "test",
    "country": "MEX"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name",
    "phone": "111111111111",
    "email": "test@pagsmile.com",
    "bank_code": "40138",
    "account": "138580000007439590", //test REJECTED. Process in 10 minutes
    "account_type": "clabe",
    "document_id" : "MAMB780915969",
    "document_type": "RFC",
    "method": "SPEI",
    "custom_code" : "31443964215700_bqSE",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "MXN",
    "notify_url" : "https://sandbox.transfersmile.com/api/notify/demo",
    "additional_remark": "test",
    "country": "MEX"
}
```
{% endtab %}
{% endtabs %}

***

### Chile

#### Banktransfer

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "bank_code": "001",
    "account_type": "Checking",
    "account": "222222222222", //test PAID. Process in 1 day
    "document_type": "Rut",
    "document_id": "111111111",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "CLP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "CHL",
    "method": "BANKTRANSFER"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name",
    "bank_code": "001",
    "account_type": "Checking",
    "account": "111111111111", //test REJECTED. Process in 1 day
    "document_type": "Rut",
    "document_id": "111111111",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "CLP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "CHL",
    "method": "BANKTRANSFER"
}
```
{% endtab %}
{% endtabs %}

#### Wallet

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "account_type": "EMAIL",
    "account": "paid@pagsmile.com", //test PAID.
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "CLP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "CHL",
    "method": "WALLET",
    "channel": "Vita"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "account_type": "EMAIL",
    "account": "rejected@pagsmile.com", //test REJECTED.
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "CLP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "CHL",
    "method": "WALLET",
    "channel": "Vita"
}
```
{% endtab %}
{% endtabs %}

***

### Colombia

#### Banktransfer

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "phone": "573020481705",
    "email": "test@pagsmile.com",
    "bank_code": "007",
    "account_type": "CHECKING",
    "account": "222222222222",//test PAID. Process in 3 days
    "document_type": "CC",
    "document_id": "123456789",
    "fee_bear": "merchant",
    "amount": "100",
    "source_currency": "USD",
    "arrival_currency": "COP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "custom_code0301",
    "additional_remark": "test",
    "country": "COL",
    "method": "BANKTRANSFER"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name",
    "phone": "573020481705",
    "email": "test@pagsmile.com",
    "bank_code": "007",
    "account_type": "CHECKING",
    "account": "111111111111",//test REJECTED. Process in 3 days
    "document_type": "CC",
    "document_id": "123456789",
    "fee_bear": "merchant",
    "amount": "100",
    "source_currency": "USD",
    "arrival_currency": "COP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "custom_code0301",
    "additional_remark": "test",
    "country": "COL",
    "method": "BANKTRANSFER"
}
```
{% endtab %}
{% endtabs %}

#### Wallet

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "account_type": "PHONE",
    "account": "+57322222222", //test PAID.
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "COP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "COL",
    "method": "WALLET",
    "channel": "Tpaga"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "account_type": "PHONE",
    "account": "+57311111111", //test PAID.
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "COP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "COL",
    "method": "WALLET",
    "channel": "Tpaga"
}
```
{% endtab %}
{% endtabs %}

#### Transfiya

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name"
    "account_type": "PHONE",
    "account": "572222222222", //test PAID.
    "document_id": "123456789",
    "document_type": "CC",
    "method": "Transfiya",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "COP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "COL"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name"
    "account_type": "PHONE",
    "account": "571111111111", //test REJECTED.
    "document_id": "123456789",
    "document_type": "CC",
    "method": "Transfiya",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "COP",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "COL"
}
```
{% endtab %}
{% endtabs %}

***

### Peru

#### Banktransfer

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "bank_code": "0001",
    "account_type": "Savings",
    "account": "2222222222222", //test PAID. Process in 1 day
    "document_type": "DNI",
    "document_id": "11111111",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "PEN",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "PER",
    "method": "BANKTRANSFER",
    "region": "La Libertad"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name",
    "bank_code": "0001",
    "account_type": "Savings",
    "account": "1111111111111", //test REJECTED. Process in 1 day
    "document_type": "DNI",
    "document_id": "11111111",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "PEN",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test",
    "country": "PER",
    "method": "BANKTRANSFER",
    "region": "La Libertad"
}
```
{% endtab %}
{% endtabs %}

***

### Ecuador

#### Banktransfer

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "bank_code": "0001",
    "account_type": "Checking",
    "account": "2222222222", //test PAID. Process in 1 day
    "document_type" : "CEDULA",
    "document_id": "1111111111",
    "fee_bear": "merchant",
    "amount": "0.5",
    "source_currency": "USD",
    "arrival_currency": "USD",
    "notify_url" : "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test22031801",
    "country": "ECU",
    "method": "BANKTRANSFER"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
    "name": "test name",
    "bank_code": "0001",
    "account_type": "Checking",
    "account": "1111111111", //test REJECTED. Process in 1 day
    "document_type": "CEDULA",
    "document_id": "1111111111",
    "fee_bear": "merchant",
    "amount": "0.5",
    "source_currency": "USD",
    "arrival_currency": "USD",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test22031801",
    "country": "ECU",
    "method": "BANKTRANSFER"
}
```
{% endtab %}
{% endtabs %}

***

### Uruguay

#### Banktransfer

{% tabs %}
{% tab title="Test PAID" %}
```
{
    "name": "test name",
    "phone": "91111111111",
    "email": "test@test.com",
    "bank_code": "1137",
    "account_type": "SAVINGS",
    "account": "000001111111", //test PAID. Process in 1 day
    "document_type": "CI",
    "document_id": "66666666",
    "fee_bear": "merchant",
    "amount": "1",
    "source_currency": "USD",
    "arrival_currency": "UYU",
    "notify_url": "https://sandbox.transfersmile.com/api/notify/demo",
    "custom_code": "test${timestamp}",
    "additional_remark": "test22031801",
    "country": "URY",
    "method": "BANKTRANSFER"
}
```
{% endtab %}

{% tab title="Test REJECTED" %}
```
{
}
```
{% endtab %}
{% endtabs %}

