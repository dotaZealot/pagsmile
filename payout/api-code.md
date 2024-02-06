---
description: >-
  This section includes a description of every API code used in the Pagsmile
  Payouts API.
---

# API Code

## Success

| API Code | HTTP Code | Message(msg) |
| -------- | --------- | ------------ |
| 0        | 200       | success      |

### Rejected

{% hint style="danger" %}
"status":"REJECTED" means the transaction was created but couldn't be processed.&#x20;
{% endhint %}

<table><thead><tr><th width="287.3333333333333">Reject Reason (Remark)</th><th width="459">Description</th></tr></thead><tbody><tr><td>CPF Verify Failed</td><td>User document id illegal</td></tr><tr><td>Legal Purpose</td><td>Legal risks</td></tr><tr><td>Fraud Suspect</td><td></td></tr><tr><td>Bank Control</td><td>Bank's risk control</td></tr><tr><td>Minor Control</td><td></td></tr><tr><td>Document Fail</td><td>User's KYC failed</td></tr><tr><td>Exceed Total Transaction Limit</td><td>User exceeds regulated transaction amount</td></tr><tr><td>Exceed Total Frequency Limit</td><td>User exceeds regulated transaction frequency</td></tr><tr><td>Exceed Single Limit</td><td>User exceeds regulated transaction amount</td></tr><tr><td>Invalid PIX Key</td><td>The PIX key is invalid or unregistered</td></tr><tr><td>Other</td><td></td></tr></tbody></table>

## Failed

{% hint style="danger" %}
If you received the below errors, you can assume the transaction is failed. This transaction will not be created on our side.
{% endhint %}

### Param Error Part 1

| API Code | HTTP Code | Message(msg)                    |
| -------- | --------- | ------------------------------- |
| 4004001  | 401       | invalid token                   |
| 4004002  | 401       | token expired                   |
| 4004003  | 401       | permission denied               |
| 4004100  | 401       | MerchantId or AppId is required |
| 4004101  | 401       | Authorization is required       |
| 4004103  | 401       | IP address has no permission    |
| 4004004  | 404       | not found                       |
| 4004029  | 429       | too many requests               |

### Param Error Part 2

| API Code | HTTP Code | Message(msg)                                                                               |
| -------- | --------- | ------------------------------------------------------------------------------------------ |
| 4001000  | 400       | invalid parameter                                                                          |
| 4001001  | 400       | invalid document\_id                                                                       |
| 4001002  | 400       | invalid account                                                                            |
| 4001003  | 400       | invalid account type                                                                       |
| 4001004  | 400       | invalid amount                                                                             |
| 4001005  | 400       | invalid amount type                                                                        |
| 4001006  | 400       | invalid amount range                                                                       |
| 4001007  | 400       | invalid fee\_bear                                                                          |
| 4001008  | 400       | invalid start\_time                                                                        |
| 4001009  | 400       | <p>invalid additional_remark</p><p>- should be less than 40 characters - </p>              |
| 4001010  | 400       | <p>invalid additional_remark</p><p>- only alphabets, numbers and underline supported -</p> |
| 4001011  | 400       | request has expired                                                                        |
| 4001012  | 400       | time range must in 31 days                                                                 |
| 4001013  | 400       | amount reached monthly limit                                                               |
| 4001014  | 400       | account err                                                                                |
| 4001020  | 400       | order already existed                                                                      |
| 4001021  | 400       | order not existed                                                                          |
| 4001022  | 400       | order is closed                                                                            |
| 4001023  | 400       | order is finished                                                                          |
| 4001100  | 400       | country not supported                                                                      |
| 4001101  | 400       | arrival\_currency not supported                                                            |
| 4001102  | 400       | method not supported in country                                                            |
| 4001103  | 400       | method or channel is inactive                                                              |
| 4001104  | 400       | method not supported                                                                       |
| 4001105  | 400       | channel not supported                                                                      |
| 4001106  | 400       | currency not supported                                                                     |
| 4001107  | 400       | not supported payout method                                                                |
| 4001108  | 400       | payout currency not supported                                                              |
| 4001110  | 400       | Don't support payouts from source\__currency to payout\_currency_                          |
| 4001111  | 400       | Don't support payouts from source\__currency to arrival\_currency_                         |
| 4001200  | 400       | merchant not existed                                                                       |
| 4001201  | 400       | merchant is inactive                                                                       |
| 4001202  | 400       | app is inactive                                                                            |
| 4001203  | 400       | app not existed                                                                            |
| 4001302  | 400       | bank account error                                                                         |

### System Error

| API Code | HTTP Code | Message(msg)                     |
| -------- | --------- | -------------------------------- |
| 5001000  | 500       | system error                     |
| 5001001  | 500       | fee config error                 |
| 5001002  | 500       | fee config error                 |
| 5001003  | 500       | fee not configured               |
| 5001004  | 500       | arrival amount is less than zero |
| 5001005  | 500       | channel config error             |
| 5001100  | 500       | account is not available         |
| 5001101  | 500       | account balance error            |
| 5001102  | 500       | balance insufficient             |
| 5001103  | 500       | checkout token error             |

