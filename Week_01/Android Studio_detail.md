# Android Studio의 기본구성 알아보기
## AndroidManifest.xml 탐구 + app 파일 탐구
### 1) application
```
<application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.IntentExample">
        ...
</application>
```
- application 부분은 안드로이드 기본 앱 설정들을 세팅해줄 수 있음
- icond이 minmap에서 기본으로 설정되어있는데 바꿔줄 수 있음
- app_name은 처음에 프로젝트를 생성할 때 만들어지는 이름이고 이 부분에서 다르게 변경할 수 있음
- roundIcon은 아이콘 이미지를 둥글게 처리해주는 부분
- theme는 앱의 테마 기본 색상들을 변경하기도 함

### 2) activity
```
<activity android:name=".SubActivity"></activity>
<activity android:name=".MainActivity"
            android:exported="true">
            ...
</activity>
```
- activity는 항상 java라는 폴더에서 activity를 extends하는 부분이 있으면 manifest로 와서 activity를 선언해주어야 함
- 여기서는 MainActicvity와 SubActivity를 activity로 선언해주었음

### 3) Intent-filter
```
<activity android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"
                    android:exported="true"/>

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
</activity>
```       
- Intentfilter는 메인 액티비티에만 적용되어 있음
- Intentfilter를 통해서 어디화면이 먼저 실행되는지를 직접적으로 관리한다고 볼 수 있음  
  (즉, MainActivity에만 Intentfilter가 포함되고 MainActivity 화면이 제일 먼저 실행됨을 알 수 있음)

### 4) res > drawable
- drawable은 주로 이미지 폴더 담당
- 밖에서 이미지를 가지고 와서 넣거나 이미지들을 모아두는 폴더

### 5) res > layout
- layout은 레이아웃파일들을 모아놓는 곳
- 미리 빌드를 하지 않아도 액티비티 preview에서 보면서 수정도 가능

### 6) res > minmap
- minmap은 ic_launcher등, 기본적으로 제공하는 아이콘들을 모아놓은 곳
        
