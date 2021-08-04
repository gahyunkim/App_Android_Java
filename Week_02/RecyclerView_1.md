# RecyclerView 만들기_1

### 1) recyclerview 생성
```
<androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rv"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:scrollbarFadeDuration="0"
        android:scrollbarSize="5dp"
        android:scrollbarThumbVertical="@android:color/darker_gray"
        android:scrollbars="vertical">
</androidx.recyclerview.widget.RecyclerView>
```
- 안드로이드 리사이클러뷰는 기본적으로 스크롤 바가 달려있음. 
- 사용하지 않으면 자동으로 사라지는 스크롤 뷰를 계속 유지하기 위해서 android:scrollbarFadeDuration = "0"를 사용함
- scrollThumbVertical은 스크롤 바의 색상을 지정해준 것임
- android:scrollbars="vertical"로 스크롤바를 생성하여줌

### 2) 추가 버튼 생성하기
```
<Button
        android:id="@+id/btn_add"
        android:layout_weight="8"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="추가"/>
```
- layout_weight은 가로세로의 가로 세로의 길이를 무게 단위로 나타내어 배치하는 것. 비율을 맞추는 것이라고 생각함

### 3) item_list.xml 만들기
- 버튼을 누르면 추가될 리스트들을 보여주기 위한 새로운 xml을 생성함
- layout> new> Layout Resource File

### 4) item_list.xml 내부 위젯 구성하기
```
<ImageView
            android:layout_margin="5dp"
            android:id="@+id/iv_profile"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@mipmap/ic_launcher"/>
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            android:gravity="center_vertical">
            <TextView
                android:id="@+id/tv_name"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="android"/>
            <TextView
                android:id="@+id/tv_content"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="android_1"/>
</LinearLayout>
```
- center_vertical을 이용해 세로이면서 가운데로 정렬해줌
- ImageView를 이용해 왼쪽부분에 이미지를 넣어주고 TextView로 오른쪽 부분에 text를 써줌

### 5) java파일 생성하기
- item_list에 들어갈 변수들을 모두 선언하기 위한 MainData.java파일 생성
- item_list는 위에서 만든 ImageView, TextView2개를 포함한 것

### 6) MainData 파일 구성하기
```
private int iv_profile;
    private String tv_name;
    private String tv_content;

    public MainData(int iv_profile, String tv_name, String tv_content) {
        this.iv_profile = iv_profile;
        this.tv_name = tv_name;
        this.tv_content = tv_content;
    }
```
- item_list에 포함된 위젯들을 id를 이용해 private로 선언
- 각각의 멤버들을 이용해 생성자를 만들어줌  

```
 public int getIv_profile() {
        return iv_profile;
    }
    public void setIv_profile(int iv_profile) {
        this.iv_profile = iv_profile;
    }
    public String getTv_name() {
        return tv_name;
    }
    public void setTv_name(String tv_name) {
        this.tv_name = tv_name;
    }
    public String getTv_content() {
        return tv_content;
    }
    public void setTv_content(String tv_content) {
        this.tv_content = tv_content;
    }
```
- getter와 setter 생성하기를 통해 사용하게 될 멤버들의 getter와 setter들을 만들어 줌



