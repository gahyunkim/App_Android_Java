# musicplayer 만들기
### 1) 음악을 넣어줄 directory 만들기
- res> raw directory 생성하기
- 생성 후 Ctrl v를 이용해 raw파일에 틀고자 하는 음악을 넣어줌

### 2) 화면 구성하기
```
<Button
        android:layout_margin="4dp"
        android:id="@+id/btn_play"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="재생"/>

<Button
        android:layout_margin="4dp"
        android:id="@+id/btn_stop"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="정지"/>
```
- 음악을 켜고 끌 수 있는 버튼을 만들어줌
- weight를 1로 지정하여 두개의 버튼이 비율을 맞춰 화면상에 존재할 수 있도록 해줌
- margin을 주어 버튼들의 상하좌우의 거리를 만들어 줌

### 3) MainActivity에 Button 선언하기
```
private Button  btn_play;
private Button btn_stop;
MediaPlayer mediaPlayer;
...
btn_play=(Button)findViewById(R.id.btn_play);
btn_stop=(Button)findViewById(R.id.btn_stop);
```
- 화면에서 만들어준 Button들을 자바 파일 내부에 선언해줌
- 음악을 끄고 켜기 위해 MediaPlayer도 선언해줌

### 4) 버튼 클릭시에 나타날 행동 구현하기
```
btn_play.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //초기화 시키기
                mediaPlayer = MediaPlayer.create(MainActivity.this,R.raw.music1);
                mediaPlayer.start();
            }
        });

btn_stop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(mediaPlayer.isPlaying()){
                    mediaPlayer.stop();
                    mediaPlayer.reset();
                }
            }
        });
```
- btn_play 즉, 노래를 시작하기 위해 이 버튼을 누를 경우 MediaPlayer를 일단 초기화시키고 start() 메소드를 이용해 노래가 시작될 수 있도록 함
- MediaPlayer.create(MainActivity.this,R.raw.music1)에서 create 내부에 R.raw.music1을 하여 music1이라는 노래를 사용할 수 있도록 지정함
- btn_stop을 누를 경우 if 조건문을 사용함
- 만약 노래가 진행되고 있다면 이 노래를 멈추기 위해 stop()과 reset() 메소드를 사용함

### 5) 액티비티 종료시 구현
```
@Override
    protected void onDestroy() {
        super.onDestroy();
        if(mediaPlayer != null){
            mediaPlayer.release();
            mediaPlayer= null;
        }
    }
```
- 액티비티가 종료 될 때 이곳을 실행시키는 메소드를 사용함
- 만약 mediaPlayer가 null이 아니라면 release()메소드를 실행함
- 그리고 mediaPlayer를 null로 만들어 종료 시킬 수 있도록 
