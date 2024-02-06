# WebView Example

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

```
package com.wallet.testwebview;

import android.app.Activity;
import android.content.Intent;
import android.graphics.Bitmap;
import android.net.Uri;
import android.os.Build;
import android.os.Bundle;
import android.provider.MediaStore;
import android.util.Log;
import android.view.View;
import android.webkit.JavascriptInterface;
import android.webkit.JsResult;
import android.webkit.ValueCallback;
import android.webkit.WebChromeClient;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.ProgressBar;
import android.widget.Toast;

import androidx.annotation.Nullable;
import androidx.annotation.RequiresApi;
import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

public class WebViewActivity extends AppCompatActivity {

    private static final String TAG = "WebViewActivity";
    private WebView webView;
    private ProgressBar progressBar;


    @RequiresApi(api = Build.VERSION_CODES.KITKAT)
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_web_view);
        if (Constant.second != null && !Constant.second.isFinishing()) {
            Constant.second.finish();
        }
        progressBar = (ProgressBar) findViewById(R.id.progressbar);
        webView = (WebView) findViewById(R.id.webview);
        webView.setBackgroundColor(0); 
        Intent intent = getIntent();
        String url = intent.getStringExtra("url");
//        url = "http://demo.gemini-tiger.cn/order";
        webView.loadUrl(url);
        //添加js监听 这样html就能调用客户端
        webView.addJavascriptInterface(this, "PWA");

        webView.setWebChromeClient(webChromeClient);
        webView.setWebViewClient(webViewClient);
        WebSettings webSettings = webView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        webView.setWebContentsDebuggingEnabled(true);
        webSettings.setSupportMultipleWindows(true);
        webSettings.setJavaScriptCanOpenWindowsAutomatically(true);//允许js弹出窗口
        webSettings.setSupportMultipleWindows(true);
        webSettings.setDomStorageEnabled(true);
        webSettings.setDatabaseEnabled(true);
        webSettings.setAllowFileAccess(true);
        webSettings.setBlockNetworkLoads(false); // 是否从网络获取资源

        /**
         * LOAD_CACHE_ONLY: 不使用网络，只读取本地缓存数据
         * LOAD_DEFAULT: （默认）根据cache-control决定是否从网络上取数据。
         * LOAD_NO_CACHE: 不使用缓存，只从网络获取数据.
         * LOAD_CACHE_ELSE_NETWORK，只要本地有，无论是否过期，或者no-cache，都使用缓存中的数据。
         */
        webSettings.setCacheMode(WebSettings.LOAD_NO_CACHE);
        //支持屏幕缩放
        webSettings.setSupportZoom(true);
        webSettings.setBuiltInZoomControls(true);
        //不显示webview缩放按钮
        webSettings.setDisplayZoomControls(false);
        webSettings.setUseWideViewPort(true); //将图片调整到适合webview的大小
        webSettings.setLoadWithOverviewMode(true); // 缩放至屏幕的大小
        findViewById(R.id.bt_sx).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                webView.reload();
            }
        });
    }

    //WebViewClient主要帮助WebView处理各种通知、请求事件
    private WebViewClient webViewClient = new WebViewClient() {
        @Override
        public void onPageFinished(WebView view, String url) {//页面加载完成
            Log.i(TAG, "加载完成url:" + url);
            progressBar.setVisibility(View.GONE);
        }

        @Override
        public void onPageStarted(WebView view, String url, Bitmap favicon) {//页面开始加载
            Log.i(TAG, "加载url:" + url);
            progressBar.setVisibility(View.VISIBLE);
        }

        @Override
        public boolean shouldOverrideUrlLoading(WebView view, String url) {
            Log.i(TAG, "拦截url:" + url);
            return super.shouldOverrideUrlLoading(view, url);
        }


    };

    private static ValueCallback<Uri[]> filePathCallback1;

//WebChromeClient support WebView to process Javascript dialog, web icon, web title, loading progress, etc
private WebChromeClient webChromeClient = new WebChromeClient() {

//Don't support js alert pop-up. Need to montior and pop-up through dialog.
@Override
public boolean onJsAlert(WebView webView, String url, String message, JsResult result) {
    AlertDialog.Builder localBuilder = new AlertDialog.Builder(webView.getContext());
    localBuilder.setMessage(message).setPositiveButton("Yes", null);
    localBuilder.setCancelable(false);
    localBuilder.create().show();
    //Note:
    //Must use this code: result.confirm():
    //The result is "Yes" status and wakeup WebCore thread at the same time
    //Cannot click the confirm button if not
    result.confirm();
    return true;
}

//Get web title
@Override
public void onReceivedTitle(WebView view, String title) {
    super.onReceivedTitle(view, title);
    Log.i(TAG, "web title:" + title);
}

//callback of loading progress
@Override
public void onProgressChanged(WebView view, int newProgress) {
    progressBar.setProgress(newProgress);
}


@RequiresApi(api = Build.VERSION_CODES.LOLLIPOP)
@Override
public boolean onShowFileChooser(WebView webView, ValueCallback<Uri[]> filePathCallback, FileChooserParams fileChooserParams) {
//return super.onShowFileChooser(webView, filePathCallback, fileChooserParams);

    filePathCallback1 = filePathCallback;
    //Convert the format type received by the front-end H5 into a string without a semicolon after it
    String[] acceptTypes = fileChooserParams.getAcceptTypes();
    String acceptType = "*/*";
    StringBuilder sb = new StringBuilder();
    if (acceptTypes.length > 0) {
        for (String type : acceptTypes) {
            sb.append(type).append(';');
        }
    }
    if (sb.length() > 0) {
        String typeStr = sb.toString();
        acceptType = typeStr.substring(0, typeStr.length() - 1);
    }
    //According to the judgment, trigger related operations, such as file selection, taking pictures, etc. For details, please refer to the step-3
    //Here, you can also pop up a dialog box for the user to choose. Remember to call the callback onReceiveValue method after the dialog box pops up, otherwise there will be a bug that the dialog box cannot be popped up next time.
    Intent intent = new Intent(Intent.ACTION_PICK, null);
    intent.setDataAndType(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, acceptType);
    WebViewActivity.this.startActivityForResult(intent, 15);

    return true;
}

};

@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {

    if (requestCode == 15) {
        if (resultCode == Activity.RESULT_OK) {
            Uri imgUri = data.getData();
            Uri[] result = new Uri[]{imgUri};
            filePathCallback1.onReceiveValue(result);
        } else {
            filePathCallback1.onReceiveValue(new Uri[]{});
        }
    }
    super.onActivityResult(requestCode, resultCode, data);
}

    @JavascriptInterface
    public void bindSuc(String str) {
        Log.i(TAG, "bindSuc: str = " + str);
        
        finish();
    }

    private void showToast(String str) {
        Toast.makeText(this, str, Toast.LENGTH_SHORT).show();
    }
}

```
