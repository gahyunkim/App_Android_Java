# 자바를 이용한 안드로이드 앱 개발 3
### 1) ImageView 생성 + Toast
```
<ImageView
        android:id="@+id/test"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:src="@mipmap/ic_launcher"/>
```
- ImageView를 이용해서 ic_launcher안에 있는 기본 icon을 생성해줌
- 크기는 100dp로 설정해줌
- minmap은 

### 2) ImageView gravity를 이용한 좌우 이동
```
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:gravity="right">


    <ImageView
        android:id="@+id/test"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:src="@mipmap/ic_launcher"/>
</LinearLayout>
```
- 새롭게 LinearLayout을 생성해준 뒤 width와 height는 match_parent와 wrap_content로 설정함
- gravity를 이용해서 right, left로 좌우로 이동시킬 수 있음

### 3) MainActivity에 ImageView 선언
```
private ImageView test;
...
test = (ImageView)findViewById(R.id.test);
```
- ImageView를 id로 선언하고, findViewById를 이용해 test의 위치를 알아냄

### 4) Toast메시지 만들기
```
test.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(getApplicationContext(), "안드로이드", Toast.LENGTH_SHORT).show();
            }
        });
 ```
- Toast message는 먹는 토스트처럼 밑에서 튀어나오듯이 팝업 메시지가 나오는 것
- 이미지를 클릭했을 때 Toast message가 나타나도록 만드는 것이기 떄문에 setOnClickListener를 사용함
- onCLick내부에 makeText(), show()를 사용함
- getApplicationContext()는  본인의 앱 MainActivity를 뜻하는 것
- "안드로이드"는 팝업메세지로 뜨는 내용을 넣은 부분
- Toast메시지가 얼마동안 떠있을 것인지를 하는 부분은 LengthShort로 짧은시간 나오도록 하는 것
