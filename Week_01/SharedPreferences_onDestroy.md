# 앱 종료 시 내용 저장하는 Shared 이용하기
### 1) EditText 생성
```
<EditText
        android:id="@+id/et_save"
        android:layout_width="100dp"
        android:layout_height="wrap_content"/>
```
- EditText를 생성하여 글을 쓰고 바꿀 수 있는 공간을 만듦

### 2) java 파일에 EditText 생성
```
private EditText et_save;
String shared = "file";
```
- 문자열 클래스 String을 이용해서 file이라는 문자열을 포함한 shared를 만들어줌

### 3) onCreate에 내용 추가하기
```
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        et_save=(EditText)findViewById(R.id.et_save);

        SharedPreferences sharedPreferences = getSharedPreferences(shared,0);
        String value = sharedPreferences.getString("kim","");
        et_save.setText(value);
    }
```
- et_save- ...으로 et_save의 위치를 찾아줌
- SharedPreferences는 String과 같은 간단한 데이터들을 key와 value를 저장하는 방법
- getSharedPreferences(shared,0)를 이용해서 값이 0인 shared를 가져오는 것임
- value라는 새로운 String클래스의 멤버를 만들어주고 별명이 kim이며 getString으로 value에 들어오게될 문자열을 받아줌
- setText는 EditText에 value값을 넣어주겠다는 의미

### 4) onDestoy를 생성해주기 
```
@Override
    protected void onDestroy() {
        super.onDestroy();
        
        SharedPreferences sharedPreferences = getSharedPreferences(shared,0);
        SharedPreferences.Editor editor = sharedPreferences.edit();
        String value = et_save.getText().toString();
        editor.putString("kim",value);  //받아온 값을 putString으로 저장을 해준 것
        editor.commit();
    }
```
- onDestroy는 앱이 죽었을 때 실행되는 부분
- Editor는 저장을 할때 꼭 불러 줘야함. Editor를 통해 어떤 데이터를 저장할 수 있음
- sharedPreferences와 editor를 연결해준 것
- value에서 받아온 값을 putString으로 저장해줌
- commit은 모든 작업을 최종적으로 완료하는 의미. 저장을 완료하는 의미
