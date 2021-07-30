# Drawer Navigation 만들기
### 1) activity_main에 drawerLayout 만들기
```
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
...
</androidx.drawerlayout.widget.DrawerLayout>
```
-androidx.drawerlayout을 이용해서 drawerLayout을 만들어 줌

### 2) LinearLayout에 Button 만들기
```
<LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <Button
            android:id="@+id/btn_open"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="열려라 참깨"/>
    </LinearLayout>
```
- drawerlayout안에 LinearLayout을 만들어주고 Button을 생성함

### 3) activity_drawer.xml 새로 생성하기
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="240dp"
    android:layout_height="match_parent"
    android:layout_gravity="start"
    android:background="#9DCFEA"
    android:orientation="vertical"
    android:id="@+id/drawer">
```
- gravity를 이용해 start부분에 위치하도록 함
- 왼쪽에서 나타나는 메뉴판이기 때문에 width를 240dp로 지정해줌

### 4) 메뉴 속에 내용 추가
```
<Button
        android:id="@+id/btn_close"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="메뉴 닫기"
        android:layout_margin="10dp"/>

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="설정으로 이동"
        android:gravity="center"/>

    <LinearLayout
        android:layout_margin="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="테스트 메뉴"
            android:gravity="center"/>

    </LinearLayout>
```
- Button, TextView 모두 id를 생성하여 java파일에서 사용할 수 있도록 함
- 각각 margin을 이용해서 상하좌우의 거리를 조정해줌

### 5) MainActivity.java에 drawerLayout, drawerView 선언하기
```
private DrawerLayout drawerLayout;
private View drawerView;
```
- 선언을 통해서 java에서 사용할 수 있도록 만들어 줌

### 6) onCreate 내부에 내용 추가
```
drawerLayout = (DrawerLayout)findViewById(R.id.drawer_layout);
        drawerView = (View)findViewById(R.id.drawer);
        Button btn_open = (Button)findViewById(R.id.btn_open);
        btn_open.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                drawerLayout.openDrawer(drawerView);
            }
        });
```
- findViewById를 이용해서 drawerLayout, drawerView 의 위치를 찾음
- xml 파일에서 만든 Button도 동일하게 생성해줌
- btn_open의 경우는 클릭시에 drawerView를 보일 수 있도록 만들기 위해서 setOnClickListener를 사용
- openDrawer를 통해 drawerView를 open할 수 있도록 함

```
Button btn_close = (Button)findViewById(R.id.btn_close);
        btn_close.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                drawerLayout.closeDrawers();
            }
        });
```
- Button btn_close를 생성해줌
- btn_close를 누르면 drawerView가 닫힐 수 있어야하므로 setOnClickListener를 사용함
- closeDrawers를 통해서 drawerView가 닫히도록 설정함

```
drawerLayout.setDrawerListener(listener);
        drawerView.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View view, MotionEvent motionEvent) {
                return true;
            }
        });
```
- listener는 DrawerLayout에서 특정 이벤트가 발생했을 때 처리하는 역할을 함
_listener에 대한 자세한 이야기는 밑에서.._
- onTouchListener는 터치 이벤트를 감지하는 역할을 함

### 7) listener 세부 정리
```
DrawerLayout.DrawerListener listener = new DrawerLayout.DrawerListener() {
        @Override
        public void onDrawerSlide(@NonNull @org.jetbrains.annotations.NotNull View drawerView, float slideOffset) {
        }
        @Override
        public void onDrawerOpened(@NonNull @org.jetbrains.annotations.NotNull View drawerView) {
        }
        @Override
        public void onDrawerClosed(@NonNull @org.jetbrains.annotations.NotNull View drawerView) {
        }
        @Override
        public void onDrawerStateChanged(int newState) {
        }
    };
```
- onDraweSlide는 말그대로 drawer를 슬라이드로 여는 부분
- onDrawerOpened는 drawer가 오픈되었을 때
- onDrawerClosed는 drawer가 닫혔을 때
- onDrawerStateChanged는 drawer의 상태가 변화하였을 때를 담당

### 8) activity_main에 activity_drawer 포함하기
```
<include layout="@layout/activity_drawer"/>
```
- include를 통해서 main에 drawer를 포함할 수 










