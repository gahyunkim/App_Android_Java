# Loading Animation -Github 사용하기
### 1) loading Animation 찾기
- 인터넷에 'android loading animation github'을 쳐서 원하는 사이트로 들어감
- 사이트에서 사용하고 싶은 로딩화면을 골라 사용하기
- 쓰여져 있는 대로 사용법을 이용해 안드로이드 스튜디오에서 화면 구성하기

### 2) gradle에 사용하고자 하는 애니메이션 github 연결하기
```
implementation 'com.github.ybq:Android-SpinKit:1.4.0'
```
- ybq님이 만든 SpinKit을 사용하기 위해 gradle에 이를 implements해줌

### 3) 화면 구성하기
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:background="#D32020"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    tools:context=".MainActivity">

    <com.github.ybq.android.spinkit.SpinKitView
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:id="@+id/spin_kit"
        style="@style/SpinKitView.Large.CubeGrid"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        app:SpinKit_Color="#9EFFFFFF" />

</LinearLayout>
```
- <com.github.ybq.android.spinkit.SpinKitView 를 넣어주고 style에서 원하는 로딩 화면을 적어줌
- SpinKit_Color에서 색상을 새로 정할 수 있음
- gravity를 center로 해주어 로딩 이미지가 가운데에 위치할 수 있도록 함
