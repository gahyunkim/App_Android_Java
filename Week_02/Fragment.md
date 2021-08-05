# Fragment(메뉴 하단바)만들기
### 1) RelativeLayout 사용하기
```
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
...
</RelativeLayout>
```
- RelativeLayout은 자식뷰 위젯들이 상대적인 위치 관계에 따라서 영역을 결정하는 레이아웃

### 2) FrameLayout 구성하기
```
<FrameLayout
        android:id="@+id/frame"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

</FrameLayout>
```
- FrameLayout은 여러개의 뷰를 중첩으로 배치한 후 그중 한를 레이아웃의 가장 위에 표시하는 레이아웃

### 3) LinerLayout 구성하기
```
<LinearLayout
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:layout_alignParentBottom="true">

        <Button
            android:id="@+id/btn1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="메뉴1"/>
        <Button
            android:id="@+id/btn2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="메뉴2"/>
        <Button
            android:id="@+id/btn3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="메뉴3"/>
        <Button
            android:id="@+id/btn4"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="메뉴4"/>
</LinearLayout>
```
- layout_alignParentBottom은 부모 컨테이너의 아래 쪽과 뷰의 아래부분을 맞춰주는 방법
- Button4개를 만들어주고 각각의 weight즉, 비율을 1씩 지정해 줌

### 4) 버튼을 누르면 이동할 화면 4개 만들기
```
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="30sp"
        android:text="안드로이드1">
    </TextView>

</FrameLayout>
```
- fragment1.xml로 화면을 만들어주고 내부를 구성함
- 버튼을 누르면 이동할 화면에 TextView를 만들어 어떤 화면으로 이동했는지 알 수 있도록 함
- 동일한 xml을 text만 달리하여 4개 만들어줌

### 5) MainActivity 구성하기
```
Button btn1,btn2,btn3,btn4;
...
btn1 = (Button)findViewById(R.id.btn1);
btn2 = (Button)findViewById(R.id.btn2);
btn3 = (Button)findViewById(R.id.btn3);
btn4 = (Button)findViewById(R.id.btn4);
```
- 화면에서 만든 버튼들을 선언해줌
- 각각의 버튼들을 findViewById를 이용해서 

### 6) onClick 설정하기
```
btn1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                FragmentTransaction transaction = getSupportFragmentManager().beginTransaction();
                Fragment1 fragment1 = new Fragment1();
                transaction.replace(R.id.frame,fragment1);
                transaction.addToBackStack(null);
                transaction.commit();
            }
        });
```
- fragment는 액티비티가 여러개의 화면을 가질 수 있도록 만들어짐
- FragmentManager를 통해서 FragmentTransaction 의 인스턴스를 가져옴
- beginTransaction()으로 프래그먼트 트랜색션을 시작하도록 함
- commit을 통해 트랜색션을 마무리함

### 7) 연결할 Fragment파일 만들기
```
public class Fragment1 extends Fragment {

    public Fragment1(){
    }

    @Override
    public View onCreateView(@NonNull @org.jetbrains.annotations.NotNull LayoutInflater inflater, 
    @Nullable @org.jetbrains.annotations.Nullable ViewGroup container,
    @Nullable @org.jetbrains.annotations.Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment1,container,false);
    }
}
```
- Fragment에는 onCreate가 아닌 onCreateView가 존재함
- onCreateView는 onCreate를 호출한 후에 화면 구성시에 호출됨
- inflater를 이용해서 layout인 fragment를 불러올 수 있음

