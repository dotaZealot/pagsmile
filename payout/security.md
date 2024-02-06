---
description: How to make safe payment requests.
---

# Security

## Signature

The signature should use SHA256 as HMAC hash function.

<table data-header-hidden><thead><tr><th width="194">Header</th><th width="150">Type</th><th>Description</th></tr></thead><tbody><tr><td>Header</td><td>Type</td><td>Description</td></tr><tr><td>Content-Type</td><td>string</td><td>application/json; charset=UTF-8</td></tr><tr><td>AppId</td><td>string</td><td>Your App ID in payout platform</td></tr><tr><td>Authorization</td><td>string</td><td>SHA256(<em>$sorted_params + $app</em>_key)</td></tr></tbody></table>

{% hint style="info" %}
Find $AppId_, $app\_key_ from the merchant dashboard.
{% endhint %}

## Sign Method

* Ascendingly, sorted request params, check [examples](security.md#sign-example) below;
* Concatenate _sorted\_params with app\_key._
* Use _sha256(sorted\_params + app\_key)_ to get the Authorization.

{% hint style="info" %}
When sorting parameters, strip the ones with no value.
{% endhint %}

{% hint style="danger" %}
Letters in _<mark style="color:red;">**Authorization**</mark>_ need to be lower case.
{% endhint %}

## Sign Coding Example

{% tabs %}
{% tab title="Java" %}
```java
package com.pagsmile.ts;

import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

import java.util.Map;
import java.util.TreeMap;

public static String getSign(Map<String, String> params, String authKey) {
    String param = sortParam(params) + authKey;
    return sha256(param);
}

public static String sha256(String str) {
    String encodeStr = "";
    try {
        MessageDigest digest = MessageDigest.getInstance("SHA-256");
        byte[] encodedhash = digest.digest(str.getBytes(StandardCharsets.UTF_8));
        encodeStr = bytesToHex(encodedhash);
    } catch (NoSuchAlgorithmException e) {
        throw new RuntimeException("algorithm not supported");
    }
    return encodeStr;
}

public static String sortParam(Map<String, String> params) {
    try {
        Map<String, String> map = new TreeMap<>(params);

        StringBuilder sb = new StringBuilder();
        for (String k : map.keySet()) {
            String v = map.get(k);
            if (v != null && v.length() > 0) {
                sb.append(k).append("=").append(v).append("&");
            }
        }

        if (sb.length() <= 0) {
            return "";
        }

        return sb.subSequence(0, sb.length() - 1).toString();
    } catch (Exception e) {
        e.printStackTrace();
    }
    return "";
}

private static String bytesToHex(byte[] hash) {
    StringBuilder hexString = new StringBuilder(2 * hash.length);
    for (int i = 0; i < hash.length; i++) {
        String hex = Integer.toHexString(0xff & hash[i]);
        if (hex.length() == 1) {
            hexString.append('0');
        }
        hexString.append(hex);
    }
    return hexString.toString();
}
```
{% endtab %}

{% tab title="PHP" %}
```
<?php 
public function sign($params = array(),$merchantKey){

	ksort($params);
	
	$sign_string = '';
	
	foreach ($params as $key = > $value){
	
		if (!empty($value)){
			$sign_string.= $key.'='.$value.'&';
		}
	}
	
	$sign_string = substr($sign_string, 0, -1);
	
	$sign = hash("sha256", $sign_string.$merchantKey);
	
	return $sign;
}
?>
```
{% endtab %}

{% tab title="GoLang" %}
```go
package crypto

import (
	"crypto/sha256"
	"encoding/hex"
	"fmt"
	"io"
	"sort"
	"strings"
)

// signature based sha256
func GetSign(m map[string]interface{}, merchantKey string) string {
	var w = sha256.New()
	_, _ = io.WriteString(w, sortedAndBuild(m) + merchantKey)
	return fmt.Sprintf("%x", w.Sum(nil))
}

func sortedAndBuild(m map[string]interface{}) string {
	var b strings.Builder
	l, c := len(m), 0
	keySet := make([]string, 0, l)
	for k, v := range m {
		keySet = append(keySet, k)
		if _, ok := v.(string); ok {
			c = len(k) + len(v.(string)) + 2
		} else {
			c = len(k) + 10 + 2
		}
	}

	b.Grow(c)
	sort.Strings(keySet)
	for _, k := range keySet {
		if v, ok := m[k]; ok {
			var str string
			if s, okk := v.(string); okk {
				str = s
			} else if d, okkk := v.(decimal.Decimal); okkk {
				str = d.String()
			} else {
				str = fmt.Sprintf("%v", v)
			}

			if len(str) > 0 {
				b.WriteString(k)
				b.WriteString("=")
				b.WriteString(str)
				b.WriteString("&")
			}
		}
	}
	r := strings.TrimRight(b.String(), "&")
	return r
}
```
{% endtab %}

{% tab title="Python" %}
```python
# encoding: utf-8
import hashlib

# d is param dict
def ksort(d):
    return [(k,d[k]) for k in sorted(d.keys())]
    

# sha256
def sign(params,merchantKey):
    params = ksort(params)
    queryStr = ''
    for key, value in params:
        if value :
            queryStr += key + '=' + str(value) + '&'
    h2 = hashlib.sha256()
    h2.update((queryStr.rstrip('&') + merchantKey).encode(encoding='UTF-8', errors='strict'))

```
{% endtab %}
{% endtabs %}

## Sign Example

Sample request:

```
{
	"account_digit": "4",
	"account_number": "1234567",
	"account_type": "CHECKING",
	"additional_remark": "1234567_test",
	"amount": "10.00",
	"bankcode": "001",
	"branch": "0001",
	"custom_code": "1234567",
	"document_id": "50284414727",
	"document_type": "CPF",
	"fee": "merchant",
	"name": "Test User Name",
	"notify_url": "https://www.pagsmile.com",
	"payout_currency": "BRL",
	"source_currency": "BRL"
}
```

Sorted parameter before hash:

```
account_digit=4&account_number=1234567&account_type=CHECKING&additional_remark=1234567_test&amount=10.00&bankcode=001&branch=0001&custom_code=1234567&document_id=50284414727&document_type=CPF&fee=merchant&name=Test User Name&notify_url=https://www.pagsmile.com&payout_currency=BRL&source_currency=BRL
```

Concatenate _sorted\_params with app\_key (exmaple app key ABCDE) :_

```
account_digit=4&account_number=1234567&account_type=CHECKING&additional_remark=1234567_test&amount=10.00&bankcode=001&branch=0001&custom_code=1234567&document_id=50284414727&document_type=CPF&fee=merchant&name=Test User Name&notify_url=https://www.pagsmile.com&payout_currency=BRL&source_currency=BRLABCDE
```

sha256 hash

```
b15f900705867ecc3f66088054c14a80f9f12b1fb31c82320c4cbfe181876abb
```
