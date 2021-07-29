# 자바를 이용한 안드로이드 앱 개발 2_1
### 1) activity_main.xml에 EditText 생성하기
```
<EditText
        android:id="@+id/et_text"
        android:layout_width="250dp"
        android:layout_height="wrap_content"/>
```
- 텍스트를 쓰고 지울 수 있는 EditText 위젯을 추가해줌
- id를 지정하여 java파일에서 사용하기 편리하도록 만들어줌
- 텍스트의 길이를 250dp로 따로 설정해줌

### 2) MainActivity.java에 EditText 선언하기 
```
private EditText et_text;
...
et_text=findViewById((R.id.et_text));
```
- 위에서 만든 id를 이용해서 선언
- findViewById로 et_text가 어디에 있는지 알려주는 부분

### 3) onClick으로 클릭 시에 text가 다른 화면으로 이동하도록 함
```
private String str;
...
@Override
    public void onClick(View view) {
            str= et_text.getText().toString();
            Intent intent = new Intent(MainActivity.this,SubActivity.class);
            intent.putExtra(name:"str",str);
            startActivity(intent);
            }
        });
    }
```    
- 자바를 이용한 안드로이드 앱 개발2의 OnCLick부분에 Text를 위한 부분 추가
- text를 이동시킬 것이기 때문에 문자열 String클래스를 이용해서 str을 선언해줌
- et_text에 쓰여진 문자열을 getText()로 받고 String 클래스로 만들어주기 위해 toString()을 사용해줌
- putExtra(key,value)는 key,value값으로 다양한 값을 넘길 수 있음  

### 4) Intent로 넘어온 text를 보여주는 TextView 생성
```
<TextView
        android:id="@+id/tv_sub"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="30sp"
        android:text="서브"/>
```
- activity_sub.xml에 intent로 넘어올 text가 보여질 부분을 만들어줌
- textSize를 이용해서 30sp크기로 글자 크기를지정해줌

### 5) TextView를 SubActivity.java에 선언
```
private TextView tv_sub;
...
tv_sub = findViewById(R.id.tv_sub);
```
- TextView id를 이용해서 private로 선언
- findViewById로 tv_sub가 어디에 있는지 보여줌

### 6) onCreate를 이용해 넘어온 Text 보이도록 실행하기
```
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sub);

        tv_sub = findViewById(R.id.tv_sub);

        Intent intent = getIntent();
        String str = intent.getStringExtra("str");

        tv_sub.setText(str);
    }
```
- onCreate란 처음 onCreate가 실행될 때 안의 내용을 모두 한번씩 실행하도록 하는 부분
- 위에서 Intent로 전달한 데이터가 문자열이므로 String 클래스를 이용해서 getStringExtra로 ("가져올 데이터명")을 받아오는 것
- setText는 기존에 지정해둔 "서브" 대신 MainActivity에서 다른 값을 입력하면 그 값을 쓰도록 하는 기능을 함

