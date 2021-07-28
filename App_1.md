## 자바를 이용한 안드로이드 앱 개발
### _Android Studio_

- MainActivity.java는 화면을 뜻함  
- activity_main.xml은 화면을 꾸밀 수 있도록 도와주는 부분

### _activity_main.xml_
LinearLayout을 이용한 화면 구성
```
android:layout_width="match_parent"  
android:layout_height="match_parent"  
- match_parent = 레이아웃을 취하는 컨테이너의 길이를 모두 가지는 것
```

> - 사용이 간편하고 표시 형태가 직관적임  
> - 사각형 박스 형태의 디스플레이 화면에 UI 요소들을 일렬로 배치할 수 있음  
> - 안정적인 화면 구성이 가능함  
> - LinearLayout 태그 안에 Button, TextView등의 다양한 기능을 넣을 수 있음  
> - 이 태그들의 가로, 세로 배열은 Orietantion으로 설정
```
android:orientation = "horizontal"
- 위젯들을 가로로 배열
android:orientation = "vertical"
- 위젯들을 세로로 배열
```

