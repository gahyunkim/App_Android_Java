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
- ArrayList<MainData> arrayList에서는 MainData클래스에서의 list를 선언해줌
