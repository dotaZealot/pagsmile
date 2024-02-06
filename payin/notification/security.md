---
description: >-
  Pagsmile includes a signature in the Pagsmile-Signature header of each event.
  This allows you to verify that the event was sent by Pagsmile instead of a
  third party. You can verify the signature to en
---

# Security

### Signature

## Verifying signatures manually <a href="#verifying-signatures-manually" id="verifying-signatures-manually"></a>

The approximate content of the Pagsmile-Signature header is as follows (here with line breaks for easy viewing, the actual content is all on one line):

```
Pagsmile-Signature:
t=1577808000,
v2=5257a869e7ecebeda32affa62cdca3fa51cad7e77a0e56ff536d0ce8e108d8bd
```

The Pagsmile-Signature header contains a timestamp and a signature. The timestamp is prefixed by t=, followed by a UNIX timestamp; the signature is prefixed by v2=, followed by the signature content.

The notification sent uses the following format:

```
Content-Type: application/json
Method: POST
Header: Pagsmile-Signature
Body:
  {
    "trade_no":"",
  	"out_trade_no":"",
  	"out_request_no":"",
  	"app_id":"",
  	"trade_status":"",
  	"amount":"",
  	"method":"",
  	"currency":"",
    "timestamp":""
  }
```

#### Step 1 : Extract the timestamp and signatures from the header <a href="#step-1-extract-the-timestamp-and-signatures-from-the-header" id="step-1-extract-the-timestamp-and-signatures-from-the-header"></a>

Split the header using the \[,] character as the separator, to get a list of elements. Then split each element using the \[=] character as the separator, to get a prefix and value pair.

The value for the prefix \[t] corresponds to the timestamp, and \[v2] corresponds to the signature. You can discard all other elements.

#### Step 2 : Prepare the original RequestBody string <a href="#step-2-prepare-the-original-requestbody-string" id="step-2-prepare-the-original-requestbody-string"></a>

Get all the content in the RequestBody. Please pay attention here. Please do not use the program's self-built structure to format and/or serialize the RequestBody content. If you have similar requirements, please do it after getting the original data for verification to avoid unnecessary sorting of fields and the addition of characters affect the signature.

#### Step 3 : Determine the expected signature <a href="#step-3-determine-the-expected-signature" id="step-3-determine-the-expected-signature"></a>

Compute an HMAC with the SHA256 hash function. Use the SecretKey get from The merchant dashboard as the key(salt), and use the original RequestBody string as the message.

#### Step 4 : Compare the signatures <a href="#step-4-compare-the-signatures" id="step-4-compare-the-signatures"></a>

Compare the signature in the header to the expected signature. For an equality match, compute the difference between the current timestamp and the received timestamp, then decide if the difference is within your tolerance.

### Example of verifying codes in Java

```
String content = JSON.toJSONString(notify); 
String sign = SignHelper.macSha256(content, privateKey());

import javax.crypto.Mac; 
import javax.crypto.spec.SecretKeySpec; 
import java.nio.charset.StandardCharsets; 
import java.security.InvalidKeyException; 
import java.security.NoSuchAlgorithmException; 
import java.util.*;

/** 
 * 
 */ 
@Slf4j 
public final class SignHelper{

 /**
  * HMAC with SHA-256
  *
  * @param content 
  * @param salt
  * @return
  */
 public static String macSha256(String content, String salt) {
    StringBuilder result = new StringBuilder();
    try {

        Mac mac = Mac.getInstance("HmacSHA256");
        mac.init(new SecretKeySpec(salt.getBytes(StandardCharsets.UTF_8), "HmacSHA256"));
        byte[] hash = mac.doFinal(content.getBytes(StandardCharsets.UTF_8));
        for (byte b : hash) {
            result.append(Integer.toString((b & 0xff) + 0x100, 16).substring(1));
        }

    } catch (NoSuchAlgorithmException | InvalidKeyException e) {
        e.printStackTrace();
    }
    return result.toString();
 }
}
```

}
