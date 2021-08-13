# Spinner 구성하기
### 1) Spinner란?
- Spinner는 여러개의 값 중에서 하나를 선택할 수 있도록 해주는 위젯
- array.xml을 만들어 spinner내부에 들어갈 내용을 적을 수 있음

### 2) Array.xml만듥
```
<resources>
    <string-array name="test">
        <item>앱개발</item>
        <item>코딩</item>
        <item>존잘</item>
        <item>귀요미</item>
    </string-array>
</resources>
```
- res>value 에서 array.xml을 만들 수 있음
- array.xml내부에는 spinner에 들어갈 여러개의 내용을 만들어 줌

### 3) 화면 구성하기
```
<Spinner
        android:id="@+id/spinner"
        android:layout_width="150dp"
        android:layout_height="40dp"
        android:entries="@array/test">
</Spinner>

<TextView
        android:id="@+id/tv_result"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="드롭다운 결과" />
```
- Spinner 위젯을 사용해서 위젯의 크기를 지정함
- entries를 이용해 array.xml과 연결을 해줌
- TextView를 Spinner 오른쪽에 위치시켜줌

### 4) Spinner와 TextView 선언하기
```
private Spinner spinner;
private TextView tv_reuslt;
...
spinner=(Spinner)findViewById(R.id.spinner);
tv_reuslt=(TextView)findViewById(R.id.tv_result);
```
- Spinner와 TextView를 선언하고 onCreate 내에 findViewbyId를 이용해 각각 찾아줌

### 5) setOnItemSelectionListener 메소드 구현하기
```
spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> adapterView, View view, int position, long l) {
                tv_reuslt.setText(adapterView.getItemAtPosition(position).toString());
            }

            @Override
            public void onNothingSelected(AdapterView<?> adapterView) {

            }
        });
```
- setOnItemSelectedListener리스너는 onItemSelected 메소드와 onNothingSelected 리스너는 만들어냄
- onItemSelected메소드는  보기의 항복이 선택되었을 때 호출하는 메소드
- onNothingSelected 메소드는 선택한 항목이 사라질 때 호출되는 메소드
- tv_result에서 text를 선택된 spinner의 요소중 하나를 문자열로 반환해서 setText할 수 있도록 하는 부분
