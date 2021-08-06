# Music을 틀고 끄는 Service 만들기
### 1) 화면 구성하기
```
<Button
        android:id="@+id/btn_start"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="서비스 시작"/>

<Button
        android:id="@+id/btn_stop"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="서비스 종료"/>
```
- 서비스를 시작하고 종료할 수 있는 버튼 위젯 두개를 생성함

### 2) MainActivity 구성하기
```
Button btn_start;
Button btn_stop;
...
btn_start = (Button)findViewById(R.id.btn_start);
btn_stop = (Button)findViewById(R.id.btn_stop);
```
- 생성한 Button을 선언하고 onCreate메소드 내부에 findViewById를 이용해 버튼을 찾음

### 3) onCkickListener 구성하기
```
btn_start.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            startService(new Intent(getApplicationContext(),MusicService.class));
        }
});

btn_stop.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            stopService(new Intent(getApplicationContext(),MusicService.class));
        }
});
```
- btn_start는 startService를 이용해서 MusicService를 사용함
- btn_stop은 stopService를 이용함

### 4) MusicService.java파일 구성하기
```
MediaPlayer mediaPlayer;
...
@Override
    public void onCreate() {
        super.onCreate();

        mediaPlayer = MediaPlayer.create(this,R.raw.music);
        mediaPlayer.setLooping(false);
    }
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        mediaPlayer.start();
        return super.onStartCommand(intent, flags, startId);
    }
    @Override
    public void onDestroy() {
        mediaPlayer.stop();
        super.onDestroy();
    }
```
- 음악을 실행하기 위해 MediaPlayer를 사용함
- onCreate는 시작할때 초기화를 해주는 부분
- layout에서 raw파일을 만들고 그 안에 다운받은 music파일을 넣음
- 이 파일을 사용하기 위해 mediaPlayer = MediaPlayer.create(this,R.raw.music); 이렇게 해줌
- 반복재생을 안하면 false로 하고 반복재생을 하면 true로 설정함
- onStart는 시작을 위한 부분, 음악이 시작하는 부분을 뜻함
- mediaPlayer.start()를 통해 미디어를 시작할 수 있도로 함
- Destroy는 종료하는 부분

### 5) AndroidManifest부분 추가하기
```
<service android:name=".MusicService"/>
```
- application 내부에 service를 사용하기 위해 service를 추가해줌
