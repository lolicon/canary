# WebView Canary

> Webview Canary helps discover vulnerable / improper `WebChromeClient` / `WebViewClient` / `WebSettings` implementation within Android WebView context

tips: you may employ `https://lolicon.github.io/canary/` to get rid of the hassle https deployment

1. User-Agent

   dump user-agent of current webview implementation

2. JavaScriptInterface

   dump _all_ ~~possible~~ JavascriptInterfaces implementation injected into current WebView context, which can be called by js immediately

3. LaunchIntent

   generate a link with specified component name & data uri, automatically filled with grant flags / send actions / `HTML_TEXT` extra / selector to increase the possibility of exploiting

4. Clipboard

   page invoke `read / readText / write / writeText` in js, the WebView implementation may involve in an active confirm process to avoid sensitive data leak to webpage

5. WebChromeClient

   - onJsAlert / onJsConfirm / onJsPrompt / onConsoleMessage

     page calls `alert/confirm/prompt`, `console.log/warn/debug/info/error`, the WebView client MUST NOT rely on the parameter for danger actions
   - onGeolocationPermissionsShowPrompt

     page requests for user location , WebView client should implement `onGeolocationPermissionsShowPrompt` with caution to avoid personal information disclosure to unwanted sites
   - onPermissionRequest

     page requests for audio/video streaming, WebView client should implement `onPermissionRequest` with caution to avoid data leakage
