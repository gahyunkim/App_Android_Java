# SNS 하단 네비게이션 바 만들기
### 1) buttom_menu.xml만들기
- res > new > menu > buttom_menu.xml 생성하기
- item 위젯을 이용해 만들고자 하는 메뉴의 개수를 맞춰 생성해줌
- 각각의 item에 들어갈 이미지는 drawable에서 기본적으로 제공하는 아이콘을 사용함

### 2) activity_main.xml구성하기
- 하단 메뉴바를 만들기 위해 palette에서 bottomNavigationView를 화면으로 끌어와 하단에 위치시킴
- 기본적인 내용이 들어갈 Frame도 만들기 위해 FrameLayout도 동일하게 화면으로 끌어와 위치시킴
```
<FrameLayout
        android:id="@+id/main_frame"
        android:layout_width="409dp"
        android:layout_height="544dp"
        app:layout_constraintBottom_toTopOf="@+id/bottomNavi"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent">

    </FrameLayout>

    <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottomNavi"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:itemIconTint="#000000"
        app:itemTextColor="#000000"
        app:layout_constraintBottom_toBottomOf="parent"
        app:menu="@menu/bottom_menu"
        tools:layout_editor_absoluteX="1dp" />
```
- 각각의 id를 부여하고 width와 height를 원하는 크기로 조절함
- 이렇게 구성하면 하단의 메뉴바에는 아까 설정한 아이콘이 메뉴바에 나타나게 됨

### 3) 각각의 아이콘 내용 구현하기(1)
- 하단바 메뉴에 있는 아이콘들을 클릭하면 그에 맞는 화면으로 이동하기 위해 각각의 화면을 만들어 줌
- res > layout에서 fra1,frag2..로 원하는 이름으로 각각의 화면을 구성함
```
<TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="1번 화면"
        android:textSize="40sp"/>
```
- 아이콘이 선택되었을 때 화면의 이동을 보여주기 위해 각각의 화면에는 서로 다른 text를 넣어줌
- TextView 위젯을 이용해 text가 보여질 수 있도록 하고 frag1, frag2모두 텍스트를 다르게 해줌

### 4) 각각의 아이콘 내용 구현하기(2)
```
public class Frag1 extends Fragment {
    private View view;

    @Nullable
    @org.jetbrains.annotations.Nullable
    @Override
    public View onCreateView(@NonNull @org.jetbrains.annotations.NotNull LayoutInflater inflater, @Nullable @org.jetbrains.annotations.Nullable ViewGroup container, @Nullable @org.jetbrains.annotations.Nullable Bundle savedInstanceState) {
        view = inflater.inflate(R.layout.frag1, container, false);

        return view;
    }
}
```
- extends Fragment를 해주어서 fragment의 성질을 이용할 수 있도록 상속해줌
- onCreateView 메소드를 선언해주고 내부에 frag1화면으로 이동할 수 있도록 하는 메소드 내용을 구현함
- Frag1.java, Frag2.java... 등 모두 동일한 방식으로 만들어 줌

### 5) MainActivity 구성하기
```
private BottomNavigationView bottomNavigationView;
    private FragmentManager fm;
    private FragmentTransaction ft;
    private Frag1 frag1;
    private Frag2 frag2;
    private Frag3 frag3;
    private Frag4 frag4;
    private Frag5 frag5;
```
- 우선 사용하고자 하는 Frag1 frag1과 FragmentManager등을 선언함
```
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        bottomNavigationView =findViewById(R.id.bottomNavi);
        bottomNavigationView.setOnNavigationItemSelectedListener(new BottomNavigationView.OnNavigationItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected(@NonNull @NotNull MenuItem item) {
                switch (item.getItemId()){
                    case R.id.action_airplane:
                        setFrag(0);
                        break;
                    case R.id.action_cloud:
                        setFrag(1);
                        break;
                    case R.id.action_subway:
                        setFrag(2);
                        break;
                    case R.id.action_mic:
                        setFrag(3);
                        break;
                    case R.id.action_phone:
                        setFrag(4);
                        break;
                }
                return false;
            }
        });
        frag1 = new Frag1();
        frag2 = new Frag2();
        frag3 = new Frag3();
        frag4 = new Frag4();
        frag5 = new Frag5();
        setFrag(0); 
    }
```
- onCreate 메소드 내부에는 사용하고자 하는 bottomNavigationView를 선언하고 찾아줌
- onNavigationItemSelected 메소드를 이용해 아이콘이 선택되었을 때를 확인할 수 있는 내용을 구현함
- switch- case문을 사용하고 item.getItemId가 case에서 원하는 id가 맞을 경우 setFrag(0)으로 이동할 수 있도록 함
```
frag1 = new Frag1();
        frag2 = new Frag2();
        frag3 = new Frag3();
        frag4 = new Frag4();
        frag5 = new Frag5();
        setFrag(0);  //첫 프래그먼트 화면을 무엇으로 지정해줄지 선택
```
- 이 부분은 frag1,frag2등을 사용하기 위해 new로 생성해준 것

```
    private void setFrag(int n){
        fm = getSupportFragmentManager();
        ft = fm.beginTransaction();
        switch (n){
            case 0:
                ft.replace(R.id.main_frame,frag1);
                ft.commit();
                break;
            case 1:
                ft.replace(R.id.main_frame,frag2);
                ft.commit();
                break;
            case 2:
                ft.replace(R.id.main_frame,frag3);
                ft.commit();
                break;
            case 3:
                ft.replace(R.id.main_frame,frag4);
                ft.commit();
                break;
            case 4:
                ft.replace(R.id.main_frame,frag5);
                ft.commit();
                break;
        }
```
- 위에서 아이콘이 클릭되면 setFrag(0)으로 이동하도록 되어있음
- setFrag(int n), 즉 setFrag 메소드에서 0을 받았으므로 switch-case문에서 맞는 조건문을 찾아서 그 화면으로 이동할 수있도록 함
- 프래그먼트의 교체가 이루어질 수 있도록 하기 위한 메소드임
- setFrag(0), 위에서의 이 코드는 첫번째로 보여지는 화면을 setFrag(0)으로 지정하겠다는 의미임
