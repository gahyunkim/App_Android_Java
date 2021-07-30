# ListView와 Adapter를 이용한 List 만들기
### 1) ListView 생성하기
```
<ListView
        android:id="@+id/list"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
</ListView>
```
- id는 list로 만들어주고 ListView 위젯을 이용해서 List를 만들어 줌

### 2) java파일에서 list 생성 + find
```
private ListView list;
...
list=(ListView)findViewById(R.id.list);
```
- ListView로 list를 선언해줌
- findViewById로 list가 어느 위치에 있는지 알려줌

### 3) 데이터 저장을 위한 배열 리스트 만들기
```
List<String> data = new ArrayList<>();
ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1,data);
list.setAdapter(adapter);  //어댑터로 선언한 리스트를 다시 리스트에 선언해줌
```
- ArrayList<>()는 배열의 크기가 정해져 있지 않을 때 사용하는 배열
- 배열 안에 들어갈 자료형이 String이기 때문에 <String>으로 만들어줌
- ArrayAdapter는 만들어진 List배열과 Adapter 뷰를 연결하는 클래스 (List와 ListView를 연결해주는 역할을 하는 것이 Adapter)
- setAdapter를 이용해 ArrayAdapter로 선언한 리스트를 다시 List에 선언해줌
   
### 4) 리스트에 데이터 추가하기
```
data.add("안드로이드");
data.add("안녕하세요");
data.add("버즈");
adapter.notifyDataSetChanged();
```
- date.add로 리스트에 들어갈 내용을 추가해줌
- notifyDataSetChanged()으로 이 상황을 최종적으로 저장해줌


