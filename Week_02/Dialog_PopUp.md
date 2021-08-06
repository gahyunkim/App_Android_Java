# Dialog 팝업창 만들기
### 1) 화면 구성하기
```
<Button
        android:id="@+id/btn_dialog"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="다이얼로그"/>

<TextView
        android:id="@+id/tv_result"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="40sp"
        android:text="테스트"/>
```
- Button 생성을 통해 누르면 Dialog가 뜰 수 있도록 화면에 만들어 줌
- Dialog에 쓴 내용을 나타낼 수 있도록 하는 TextView 생성

### 2) MainActivity 구성하기
```
Button btn_dialog;
TextView tv_result;
...
btn_dialog = (Button)findViewById(R.id.btn_dialog);
tv_result = (TextView)findViewById(R.id.tv_result);
```
- 화면에서 만든 Button과 TextView를 자바파일에 선언해줌.
- findViewById를 이용해 두개의 위젯을 찾을 수 있도록 함

### 3) onCLickListener 구성하기
```
public void onClick(View v) {
        AlertDialog.Builder ad = new AlertDialog.Builder(MainActivity.this);
        ad.setIcon(R.mipmap.ic_launcher);
        ad.setTitle("제목");
        ad.setMessage("안드로이드가 맞습니까?");
```
- AlertDialog.Builder를 이용해서 AlertDialog를 생성함
- setTitle로 Dialog창의 제목을 만들어줌
- setMessage로 Dialog내부에 나타날 문구를 적어줌

### 4) Dialog 배부 버튼 만들기
```
final EditText et = new EditText(MainActivity.this);
ad.setView(et);
ad.setPositiveButton("확인", new DialogInterface.OnClickListener() {
        @Override
        public void onClick(DialogInterface dialog, int which) {
                String result = et.getText().toString();
                tv_result.setText(result);
                dialog.dismiss();
                }
        });

ad.setNegativeButton("취소", new DialogInterface.OnClickListener() {
        @Override
        public void onClick(DialogInterface dialog, int which) {
                dialog.dismiss();
                }
        });
        ad.show();
```
- setPositive를 이용하고 버튼 안에 확인이라는 내용을 넣어줌
- Dialog에 쓴 내용을 String으로 받아 tv_result에 setText로 넣어줌
- setNegativeButton도 동일함
- ad.show를 이용해 모든 것을 보여주도록 해줌
