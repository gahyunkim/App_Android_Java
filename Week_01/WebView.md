# WebView를 이용해 URL로 이동하기
### 1) WebView 생성하기
```
<WebView
        android:id="@+id/webView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"></WebView>
```
- 안드로이드 화면에서 원하는 인터넷 주소를 띄울 수 있도록 하는 부분이 WebView
- id로 webView를 설정해줌  
_WebView가 그래픽상에서 어떻게 되어있는지 잘 확인해야 함. 그래픽을 확인하지 않아 자꾸 하얀 배경이 떳는데 그래픽으로 해결했음_

### 2) WebView 선언 + 연결 URL 표시
```
private WebView webView;
private String url ="https://www.naver.com/";
```
- WebView에서 연결할 웹사이트가 네이버이므로 String클래스를 이용해서 URL을 만들어줌

### 3) onCreate메소드 내부에 내용 추가
```
webView = (WebView)findViewById(R.id.webView);
webView.getSettings().setJavaScriptEnabled(true);
webView.loadUrl(url);

webView.setWebChromeClient(new WebChromeClient()); 
webView.setWebViewClient(new WebViewClientClass());
```
- webView의 위치를 찾을 수 있도록 findViewById를 사용
- 웹뷰를 사용하면서 자바스크립트로 이루어져 있는 기능들을 사용하기 위해서 setJavaScriptEnabled(true)로 만들어줌
- url을 로드하기 위해서 loadUrl을 사용함 (url주소를 불러오는 함수)
- setWebChromeClient()는 웹뷰로 띄운 웹 페이지를 컨트롤하는 함수이며 크롬으로 웹을 열때 크롬에 맞춘 세팅을 하기 위한 함수
- setWebViewClient()는 페이지를 컨트롤 하기 위한 함수
_여기서 WebViewClientClass()부분에 빨간색 불이 들어오는데 이를 해결하기 위해 innerclass를 생성해주어야 함_

### 4) WebViewClientClass()의 innerClass 만들기
```
private class WebViewClientClass extends WebViewClient {
        @Override
        public boolean shouldOverrideUrlLoading(WebView view, String url) {
            view.loadUrl(url);
            return true;
        }
    }
```
- shoulOverrideUrlLoading()함수는 현재 페이지의 URL을 읽어오는 메소드
- 위와 동일하게 url을 로드하기 위해서 loadUrl을 사용함 (url주소를 불러오는 함수)

### 5) 전으로 이동하는 방법 구현
```
@Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {
        if((keyCode == KeyEvent.KEYCODE_BACK)&& webView.canGoBack()){
            webView.goBack();
            return true;
        }
        return super.onKeyDown(keyCode, event);
    }
```
- onKeyDown은 Key를 눌렀을 떄 실행되는 메소드
- 전으로 돌아가는 KEYCODE_BACK을 누르거나 webView.canGoBack 전으로 돌아갈 수 있는 상황이라면 true를 반환하도록 하여 전으로 돌아갈 수 있도록 함
- webView.goBack()은 위의 상황이 충족되면 뒤로 갈 수 있도록 하는 부분
- 만약 그렇지 않다면 onKeyDown을 다시 실행하도록 함

### 6) Internet 권한 설정
```
<uses-permission android:name="android.permission.INTERNET"/>
```
- 인터넷 권한을 설정해주어야 인터넷 권한을 허용해줬다고 인식하고 url을 연결해줌


