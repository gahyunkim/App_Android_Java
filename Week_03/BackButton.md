# BackButton 두번 눌러서 뒤로기기 구성
### 1) MainActivity 구성하기
```
private long backBtnTime =0;
```
- 버튼을 누른 시간을 backBtnTime = 0으로 하려 시간을 알기 쉽도록 함

### 2) onBackPressed 구성하기
```
@Override
    public void onBackPressed() {
        long curTime = System.currentTimeMillis();
        long gapTime = curTime -backBtnTime;
        //2초안에 한번 더 누르게되면 뒤로가기가 되는
        if(0<=gapTime&& 2000>=gapTime){
            super.onBackPressed();//back 버튼을 눌렀을 떄 뒤로가기 기능이 활성화 됨
        }
        else {
            backBtnTime = curTime;
            Toast.makeText(this,"한번더 누르면 종료",Toast.LENGTH_SHORT).show();
        }

    }
```
- onBackPressed는 뒤로가기 버튼을 눌렀을 때 일어나는 현상을 담은 메소드
- curTime은 시스템 내에서 현재의 시간을 담는 변수
- gapTime은 현재 시간에서 backButton을 누른 시간을 담은 변수
- 만약 gapTime이 0보다 크거나 같다면 뒤로가기가 가능하도록 함
- 또한 gapTime이 2000 즉, 2초 내에 다시 한번 뒤로가기 버튼을 누르면 뒤로가기가 활성화 되도록 함
- 그렇지 않고 backBtnTime 버튼을 누른 시간과 현재 시간이 같다면, 혹은 위의 조건을 충족하지 않는다면 Toast 메세지를 이용해 다시 한번 더 누르라고 메세지를 보내줌
