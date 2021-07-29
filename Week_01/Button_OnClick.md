# 자바를 이용한 안드로이드 앱 개발 2
### 1) 버튼을 이용해 다른 화면으로 이동하기
- java 파일에서 오른쪽 마우스를 통해 new > activity를 새롭게 생성해줌 (다른 화면 생성)
- MainActivity와 SubActivity 생성

### 2) 이동 가능한 버튼 생성
```
<Button
        android:id="@+id/btn_move"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="이동"/>
```
- Button의 width,height 모두 wrap_content로 설정 (wrap_content는 필요한 만큼만 차지함)
- id 설정을 통해 MainActivity.java에서 간단하게 사용하도록 함
- text를 이용해 버튼 내부에 들어갈 내용 입력

### 3) MainActivity.java 에 Button 선언
```
private Button btn_move;
...
btn_move = findViewById(R.id.btn_move);
```
- 위에서 설정한 id를 이용해서 Button btn_move로 선언해줌
- onCreate() 내부에서는 findViewById를 이용해서 버튼의 위치가 이곳에 있다는 것을 알려줌
 
### 4) setOnClickListener를 이용한 클릭 연결
```
 btn_move.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(MainActivity.this,SubActivity.class);
                startActivity(intent);
            }
        });
    }
```
- setOnClickListener를 이용해서 버튼을 누르면 아래의 Intent를 실행할 수 있도록 함
- Intent는 안드로이드에서 페이지 전환과 데이터 전달을 구현하도록 도와주는 객체
- new Intent() 파라미터 부분에는 어떤 화면에서 어디 화면으로 이동할 것인지 적어줌  
  (MainActivity.this에서 SubActivity.class로 이동)
- startActivity는 intent가 실제적으로 이동할 수 있도록 도와줌 

### 5) SubActivity.java 에 내용 전달
```
Intent intent = getIntent();
```
- getIntent()를 이용해 넘어온 데이터들을 받아내는 것, Intent를 받는 것
