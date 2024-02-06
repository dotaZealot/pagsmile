---
description: Native application get user authorization
---

# Native App Authorization

1. Provide the authorization link to users.

The authorization link is concatenated with Basic URL+_source_

| Parameter | Explaination                              | Example value |
| --------- | ----------------------------------------- | ------------- |
| source    | a string which can recognize the merchant | pagsmile      |

{% hint style="danger" %}
Don't put # sign in the URL
{% endhint %}

{% tabs %}
{% tab title="Test environment" %}
Basic URL

```
https://sandbox-wallet.pagsmile.com/authenticationYS?
```



Example:

```
https://sandbox-wallet.pagsmile.com/authenticationYS?source=pagsmile
```
{% endtab %}

{% tab title="Live environment" %}
Basic URL

```
https://wallet.pagsmile.com/authenticationYS?
```



Example:

```
https://wallet.pagsmile.com/authenticationYS?source=pagsmile
```
{% endtab %}
{% endtabs %}

Users will be redirected to this page to authorize.

![](<../../../.gitbook/assets/image (15).png>)



2\. Users authorize and the merchant gets UUID. Then the merchant needs Interactive development through android and js, then callback with web view.



3\. Within web view callback, the merchant needs to link user ID with UUID of Pagsmile wallet. Then the authorization page can be closed.&#x20;

```
android:

String url = "https://wallet.pagsmile.com/authenticationYS?source="+merchant_app;

webView.loadUrl(url);

//add js monitor so html can call the app
webView.addJavascriptInterface(this, "PWA");
webView.setWebChromeClient(webChromeClient);
webView.setWebViewClient(webViewClient);
WebSettings webSettings = webView.getSettings();
webSettings.setJavaScriptEnabled(true);
webView.setWebContentsDebuggingEnabled(true);
webSettings.setSupportMultipleWindows(true);
webSettings.setJavaScriptCanOpenWindowsAutomatically(true);//allow popup window
webSettings.setSupportMultipleWindows(true);
webSettings.setDomStorageEnabled(true);
webSettings.setDatabaseEnabled(true);
webSettings.setAllowFileAccess(true);
webSettings.setBlockNetworkLoads(false); //whether get the resource from network

/**
* LOAD_CACHE_ONLY: only read local data from cache
* LOAD_DEFAULT: （default）according to cache-control, decide whether get data from network
* LOAD_NO_CACHE: Only get data from network without using cache
* LOAD_CACHE_ELSE_NETWORK，use data from cache whatever if expired, whatever there is cache or not
webSettings.setCacheMode(WebSettings.LOAD_NO_CACHE);
//support screen zoom
webSettings.setSupportZoom(true);
webSettings.setBuiltInZoomControls(true);
//hide webview zoom button
webSettings.setDisplayZoomControls(false);
webSettings.setUseWideViewPort(true); //adjust photo size to fit webview
webSettings.setLoadWithOverviewMode(true); // zoom size to fit screen
  
@JavascriptInterface
public void bindSuc(String uuid) {
    Log.i(TAG, "bindSuc: uuid = "+uuid);
    //bound logic code {}
    finish();
}


OC:
[self.webView.userContentController addScriptMessageHandler:self name:@"bindSuc"];

```
