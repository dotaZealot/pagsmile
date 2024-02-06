# API Code

## Success

<table><thead><tr><th width="156.33333333333331">Code(String)</th><th width="157">Message(String)</th><th>SubCode(String)</th><th>SubMessage(String)</th><th>Description/ How to solve</th></tr></thead><tbody><tr><td>10000</td><td>Success</td><td></td><td></td><td></td></tr></tbody></table>

## Failed

### **General Error Code (Part 1)**

{% hint style="danger" %}
If you received the below errors, you can assume the transaction is **failed**. The transaction is created but the status is **REFUSED**.
{% endhint %}

<table><thead><tr><th width="134.33333333333331">Code(String)</th><th width="182">Message(String)</th><th width="198">SubCode(String)</th><th width="268">SubMessage(String)</th><th width="266">Description</th><th></th></tr></thead><tbody><tr><td>40002</td><td>Business Failed</td><td>gen-card-token-fail</td><td>Gen card token fail</td><td></td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>card-token-expired</td><td>Card token expired</td><td></td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>bank-side-busy</td><td>Bank side busy</td><td>Timeout at the bank side</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>SYS-0001</td><td>other reason</td><td>Failed at the bank side</td><td></td></tr><tr><td>70001</td><td>Reject by high risk</td><td>10001</td><td>Verify Failed</td><td>User document id not exist</td><td></td></tr><tr><td>70001</td><td>Reject by high risk</td><td>10002</td><td>Document Fail</td><td>User's KYC failed</td><td></td></tr><tr><td>70001</td><td>Reject by high risk</td><td>10003</td><td>Legal Purpose</td><td>Legal risks</td><td></td></tr><tr><td>70001</td><td>Reject by high risk</td><td>10004</td><td>Fraud Suspect</td><td></td><td></td></tr><tr><td>70001</td><td>Reject by high risk</td><td>20001</td><td>Exceed total Transaction Limit</td><td>User exceeds regulated transaction amount</td><td></td></tr><tr><td>70001</td><td>Reject by high risk</td><td>20002</td><td>Exceed Total Frequency Limit</td><td>User exceeds regulated transaction frequency</td><td></td></tr><tr><td>90001</td><td>Bank Request Fail</td><td>71012</td><td>Invalid ID Number</td><td>customer.identify info invalid</td><td></td></tr></tbody></table>

### **General Error Code (Part 2)**

{% hint style="danger" %}
If you received the below errors, you can assume the transaction is **failed**. This transaction will **not** be created on our side.
{% endhint %}

<table><thead><tr><th width="139">Code(String)</th><th width="167">Message(String)</th><th width="248">SubCode(String)</th><th width="292">SubMessage(String)</th><th width="332">Description/ How to solve</th><th></th></tr></thead><tbody><tr><td>20000</td><td>Service Currently Unavailable</td><td></td><td></td><td>Temporary issue. Check with Pagsmile if keep receiving this error</td><td></td></tr><tr><td>40001</td><td>Missing Required Arguments</td><td></td><td></td><td>Check if all required parameters are included</td><td></td></tr><tr><td>40004</td><td>Method not supported</td><td></td><td></td><td>Check parameter "method"</td><td></td></tr><tr><td>40005</td><td>MediaType not supported</td><td></td><td></td><td></td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>missing-signature-config</td><td>Signature configuration missing</td><td>Check Authorization in header, or check if the request API URL is correct.</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>merchant-status-abnormal</td><td>Merchant is now invalid</td><td>Contact Pagsmile to enable the account</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>app-status-abnormal</td><td>App is invalid</td><td>Contact Pagsmile to enable the app</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>app-not-match</td><td>App not match</td><td>The app_id in Authorization doesn't match with the app_id in the request</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>invalid-signature</td><td>Signature is invalid</td><td>check the signature in Authorization</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>no-method-supported</td><td>Method not supported</td><td>Check parameter "method"</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>currency-not-supported</td><td>Currency not supported</td><td>Check parameter "method"</td><td></td></tr><tr><td>40002</td><td>Business Failed</td><td>duplicate-out_trade_no</td><td>out_trade_no is duplicate</td><td>out_trade_no should be unique for each transaction</td><td></td></tr></tbody></table>

### **CreditCard Error Code**

| Code(String) | Message(String)   | SubCode(String) | SubMessage(String)                    |
| ------------ | ----------------- | --------------- | ------------------------------------- |
| 90001        | Bank Request Fail | 101             | Invalid authorization                 |
| 90001        | Bank Request Fail | 102             | Invalid card number                   |
| 90001        | Bank Request Fail | 103             | Invalid cvv                           |
| 90001        | Bank Request Fail | 104             | Invalid amount                        |
| 90001        | Bank Request Fail | 105             | SCA required                          |
| 90001        | Bank Request Fail | 106             | Expired card                          |
| 90001        | Bank Request Fail | 107             | Credit exceeded                       |
| 90001        | Bank Request Fail | 108             | Invalid issuer                        |
| 90001        | Bank Request Fail | 109             | Suspicion of fraud                    |
| 90001        | Bank Request Fail | 110             | Restricted card                       |
| 90001        | Bank Request Fail | 111             | Transaction not permitted to issuer   |
| 90001        | Bank Request Fail | 112             | Transaction not permitted to acquirer |
| 90001        | Bank Request Fail | 113             | Invalid transaction                   |
| 90001        | Bank Request Fail | 114             | Lost card                             |
| 90001        | Bank Request Fail | 115             | Stolen card                           |
| 90001        | Bank Request Fail | 116             | Insufficient funds                    |
| 90001        | Bank Request Fail | 117             | Do not honor                          |
| 90001        | Bank Request Fail | 118             | Contact issuer                        |
| 90001        | Bank Request Fail | 119             | Duplicate transaction                 |
| 90001        | Bank Request Fail | 190             | Not allowed for unknown reason        |
| 90001        | Bank Request Fail | 201             | Validation error                      |
| 90001        | Bank Request Fail | 202             | Invalid request data                  |
| 90001        | Bank Request Fail | 203             | Invalid card data                     |
| 90001        | Bank Request Fail | 204             | Duplicate request                     |
| 90001        | Bank Request Fail | 205             | Card brand not supported              |
| 90001        | Bank Request Fail | 206             | ID cannot be empty or invalid         |
| 90001        | Bank Request Fail | 207             | Name cannot be empty or invalid       |
| 90001        | Bank Request Fail | 401             | Provider internal error               |
| 90001        | Bank Request Fail | 402             | Connection error                      |
| 90001        | Bank Request Fail | 403             | Authentication error                  |
