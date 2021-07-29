# 자바를 이용한 안드로이드 앱 개발
## _Android Studio_

- MainActivity.java는 화면을 뜻함  
- activity_main.xml은 화면을 꾸밀 수 있도록 도와주는 부분

## _activity_main.xml_
### 1) LinearLayout을 이용한 화면 구성
```
android:layout_width="match_parent"  
android:layout_height="match_parent"  
```
> match_parent = 레이아웃을 취하는 컨테이너의 길이를 모두 가지는 것

- 사용이 간편하고 표시 형태가 직관적임  
- 사각형 박스 형태의 디스플레이 화면에 UI 요소들을 일렬로 배치할 수 있음  
- 안정적인 화면 구성이 가능함  
- LinearLayout 태그 안에 Button, TextView등의 다양한 기능을 넣을 수 있음  
- 이 태그들의 가로, 세로 배열은 Orietantion으로 설정
```
android:orientation = "horizontal"
- 위젯들을 가로로 배열
android:orientation = "vertical"
- 위젯들을 세로로 배열
```
### 2) TextView  
**입력한 Text가 보여지는 부분**  
![image](https://user-images.githubusercontent.com/68581876/127285043-67446fee-9767-406d-92b7-bfb7d827fc64.png)

- match_parent를 TextView에서 사용하면 TextView의 너비가 LinearLayout의 너비에 맞게 늘어남
- wrap_content는 사용하는 영역 만큼만 차지함
- textColor를 이용해서 원하는 색상으로 변경 가능
- textSize에서 sp단위를 이용해 원하는 크기로 글자크기 조절 가능
- text에서는 ""안에 원하는 단어나 문장을 넣으면 화면에서 나타나게 됨

### 3) EditText
**Text가 쓰여질 수 있는 부분**  
![image](https://user-images.githubusercontent.com/68581876/127288353-e035d34d-0aea-4266-a4d8-32e0f3b775e3.png)

- id를 이용해서 MainActivity에서 간단하게 표시할 수 있도록 하는 이름을 만들어 줌
- layout_width를 wrap_content나 match_parent가 아닌 특정한 크기(dp)로 지정할 수 있음 
  (dp는 크기를 지정하는 단위)
- hint는 텍스트가 쓰여질 부분에 어떤 내용을 써야하는지 미리 보여주는 부분

### 4) Button
![image](https://user-images.githubusercontent.com/68581876/127289331-151a1f19-34a6-41c2-8de2-7bf4d179d10e.png)

- id를 이용해서 MainActivity에서 간단하게 표시할 수 있도록 하는 이름을 만들어 줌
- width, height 모두 차지하는 만큼만 사용하는 wrap_contetn사용
- text를 이용해 버튼 내부에 들어가는 text를 써줌

## _MainActivity.java_

### 1) MainActivity클래스 안에 activity_main에서 만든 위젯 선언
```
EditText et_id;
Button btn_test;
```
- activity_main에서 id로 만들어놓은 간단한 id들을 이용해서 MainActivity에 선언함

### 2) onCreate 함수 
- MainActivity가 처음 실행될 때 안에 있는 구문들을 한번씩 다 실행시키도록 하는 함수

### 3) findViewById 함수 
- 위에서 선언한 id들을 찾는 함수
```
et_id = findViewById(R.id.et_id);
btn_test = findViewById(R.id.btn_test);
```
- activity_main에서 만든 id와 MainActivity에서 선언한 id들을 서로 연결하는 장치
- 접두어 R.id.을 이용해서 코드로 생성됨

### 4) setOnClickListener
> 익명 클래스를 이용한 이벤트 리스너 사용 방법
```
btn_test.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        et_id.setText("...");
        }
    });
}
```
- onClick(View view) view 파라미터에는 사용자가 클릭한 위젯이 들어가게 됨
- setText()는 기존에 있던 내용을 지우고 새롭게 설정해주는 메소드임
