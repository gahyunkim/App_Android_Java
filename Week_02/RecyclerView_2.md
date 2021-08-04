# RecyclerView 만들기_2

### 1) MainAdapter.java 파일 내용 구성하기
```
public class MainAdapter extends RecyclerView.Adapter<MainAdapter.CustomViewHolder> {

    private ArrayList<MainData> arrayList;
    public MainAdapter(ArrayList<MainData> arrayList) {
        this.arrayList = arrayList;
    }
```
- MainData 클래스 안에 있는 데이터들을 RecyclerView에 보여주기 위한 파일
- ViewHolder는 View를 보관하는 객체로 Item들을 바로 접근할 수 있도록 저장하고 사용하기 위한 객체
- Adapter<MainAdapter.CustomViewHolder>를 extends하여 사용할 수 있도록 함
- ArrayList<MainData> arrayList를 이용해 아이템들을 담을 ArrayList를 MainAdapter 안에 구현함
   
### 2) CustomViewHolder 내용 구성하기
```
public class CustomViewHolder extends RecyclerView.ViewHolder {

        protected ImageView iv_profile;
        protected TextView tv_name;
        protected TextView tv_content;

        public CustomViewHolder(@NonNull @org.jetbrains.annotations.NotNull View itemView) {
            super(itemView);
            this.iv_profile = (ImageView) itemView.findViewById(R.id.iv_profile);
            this.tv_name = (TextView) itemView.findViewById(R.id.tv_name);
            this.tv_content = (TextView) itemView.findViewById(R.id.tv_content);
        }
    }  
```
- protected를 이용해 item들을 선언해줌
- findViewById를 이용해서 세개의 item들의 위치를 알 수 있도록 선언함

### 3)  onBindViewHolder 구성하기(1)
```
public void onBindViewHolder(@NonNull @org.jetbrains.annotations.NotNull MainAdapter.CustomViewHolder holder, int position) {  
    holder.iv_profile.setImageResource(arrayList.get(position).getIv_profile());  
  holder.tv_name.setText(arrayList.get(position).getTv_name());  
  holder.tv_content.setText(arrayList.get(position).getTv_content());  
}
```
- onBindViewHolder는 뷰 홀더에 들어갈 데이터를 연결해주는 작업을 함
- setImageResource은 xml 에는 imageView 만 추가하고 Activity에서 보여주는 방법
- get(position)은 arrayList에서 저장된 데이터의 위치를 받는 의미

### 4) onBindViewHolder 구성하기(2)
```
holder.itemView.setTag(position);  
holder.itemView.setOnClickListener(new View.OnClickListener() {  
    @Override  
  public void onClick(View v) {  
        String curName = holder.tv_name.getText().toString();  
  Toast.makeText(v.getContext(),curName,Toast.LENGTH_SHORT).show(); 
  }  
});  
  
holder.itemView.setOnLongClickListener(new View.OnLongClickListener() {  
    @Override  
  public boolean onLongClick(View v) {  
        remove(holder.getAdapterPosition());  
 return true;  }  
});
```
- setTag(position)을 통해서 Arraylist에서 받아온 position의 tag를 만들어 줌
- setOnClickListener를 이용해서 클릭을 했을 때의 행동을 만들어 줌
- tv_name의 현재 text를 문자열로 받아오고 클릭시에 짧은 시간동안 Toast 메시지를 보여주도록 함
- setOnLongClickListener는 itemView를 오랜 시간 누를 경우에 해당하는 메소드
- 오래 누르게 되면 remove 메소드를 호출하고 getAdapterPosition을 통해 그 위치의 itemview를 없앨 수 있도록 함

### 5) remove 메소드 구성
```
public void remove(int position){  
    try{  
        arrayList.remove(position);  
  notifyItemRemoved(position);  
  } catch (IndexOutOfBoundsException ex){  
        ex.printStackTrace();  
  }  
}
```
- 선택한 위치에 있는 itemView를 삭제하기 위해 position을 사용함
- try-catch를 사용해서 예외 상황이 일어났을 떄 강제 실행을 하도록 함
- notify는 새로고침이라는 뜻으로 리스트 뷰를 지운 다음에 새로고침을 해준다는 의미

### 6)   itemView 카운트 메소드 만들기
```
public int getItemCount() {  
    return (null != arrayList ? arrayList.size() : 0);  
}
```
- 만약 arrayList가 0이 아니면  arryList.size()이고 arrayList가 null이면 0이라는 뜻
### 7) MainActivity에 선언하기
```
private ArrayList<MainData> arrayList;  
private MainAdapter mainAdapter;  
private RecyclerView recyclerView;  
private LinearLayoutManager linearLayoutManager;
```
-화면에서 사용하기 위한 arrayList, mainAdapter 등을 선언함

### 8) onCreate 구성하기
```
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
  setContentView(R.layout.activity_main);  
  
  recyclerView = (RecyclerView)findViewById(R.id.rv);  
  linearLayoutManager = new LinearLayoutManager(this);  
  recyclerView.setLayoutManager(linearLayoutManager);  
    
  arrayList = new ArrayList<>();  
  mainAdapter = new MainAdapter(arrayList);  
  recyclerView.setAdapter(mainAdapter);  
  
  Button btn_add = (Button)findViewById(R.id.btn_add);  
  btn_add.setOnClickListener(new View.OnClickListener() {  
        @Override  
  public void onClick(View v) {  
            MainData mainData = new MainData(R.mipmap.ic_launcher,"android","android_1");  
  arrayList.add(mainData);  
  mainAdapter.notifyDataSetChanged();  
  }  
    });  
}
```
- findViewById를 이용해 위에서 선언한 객체들을 찾도록 함
- Button의 경우는  onClickListener를 이용해 버튼을 누르면 item들이 추가될 수 있도록 함

