# VideoRecord 만들기
### 1) VideoRecord 화면 구성하기
```
<Button
       android:id="@+id/btn_record"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="녹화시작"/>
<SurfaceView
        android:id="@+id/surfaceview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
```
- Button을 만들어 버튼을 누르면 녹화를 시작할 수 있도록 하는 버튼을 만듦
- SurfaceView는 동영상이나 애니메이션과 같이 연산처리가 많이 필요한 뷰를 위해서 사용함
- SurfaceView를 이용해 동영상을 찍을 때의 화면을 보여줄 수 있도록 함

### 2) build.gradle에 추가하기
```
implementation 'gun0912.ted:tedpermission:2.0.0'
```
- tedpermission을 이용해서 접근 권한을 일일이 설정하기 않아도 되도록 간단한 방법을 사용함

### 3) MainActivity 구성하기
```
public class MainActivity extends AppCompatActivity implements SurfaceHolder.Callback {

    private Button btn_record;
    private Camera camera;
    private MediaRecorder mediaRecorder;
    private SurfaceView surfaceView;
    private SurfaceHolder surfaceHolder;
    private boolean recording = false;
```
- SurfaceView를 사용하기 위해 MainActivity에 SurfaceHolder.Callback을 implements해줌
- xml에서 만든 Button을 선언해주고 Camera를 사용할 것이기 때문에 Camera도 선언해줌
- recording은 녹화하는 지를 확인하기 위해 처음 시작은 false로 지정함

### 4) onCreate 구성하기
```
TedPermission.with(this)
                .setPermissionListener(permission)
                .setRationaleMessage("녹화를 위하여 권한을 허용해주세요")
                .setDeniedMessage("권한이 거부되었습니다, 설정 >권한에서 허용해주세요")
                .setPermissions(Manifest.permission.CAMERA, Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.RECORD_AUDIO)
                .check();
```
- TedPermission을 이용해서 권한 허용창을 만들어줌
- Message는 허용창에 어떤 내용을 보여줄 것인지를 설정함

### 5) Button 클릭시 행동 구성하기
```
btn_record = (Button)findViewById(R.id.btn_record);
        btn_record.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (recording){
                    mediaRecorder.stop();
                    mediaRecorder.release();
                    camera.lock();
                    recording=false;
                }
                else{
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            Toast.makeText(MainActivity.this,"녹화가 시작되었습니다",Toast.LENGTH_SHORT).show();
                            try {
                                mediaRecorder = new MediaRecorder();
                                camera.unlock();
                                mediaRecorder.setCamera(camera);
                                mediaRecorder.setAudioSource(MediaRecorder.AudioSource.CAMCORDER);
                                mediaRecorder.setVideoSource(MediaRecorder.VideoSource.CAMERA);
                                mediaRecorder.setProfile(CamcorderProfile.get(CamcorderProfile.QUALITY_720P));
                                mediaRecorder.setOrientationHint(90);
                                mediaRecorder.setPreviewDisplay(surfaceHolder.getSurface());
                                mediaRecorder.prepare();
                                mediaRecorder.start();
                                recording=true;

                            }catch (Exception e){
                                e.printStackTrace();
                                mediaRecorder.release();
                            }
                        }
                    });
                }
            }
        });
```
- Button을 findViewById를 이용해서 위치를 찾아주고 onClick을 위한 메소드를 만들어줌
- 만약 recording==false라면 mediaRecorder를 멈추고 release를 함
- 만약 recording이 true라면 카메라를 실행시켜야 하기 때문에 이와 관련된 내용을 만들어줌
- Toast를 이용해서 녹화가 시작되었다는 메세지를 짧게 내보냄
- try-catch 예외 탐색기를 이용하고 이 내부에 mediaRecorder 객체를 이용해 다양한 메소드를 사용해줌
- 일단 camera를 사용하기 위해 unlock해줌

### 6) onPermissionListener 사용하기
```
PermissionListener permission = new PermissionListener() {
        @Override
        public void onPermissionGranted() {
            Toast.makeText(MainActivity.this,"권한 허가",Toast.LENGTH_SHORT).show();
            camera = Camera.open();
            camera.setDisplayOrientation(90);
            surfaceView = (SurfaceView)findViewById(R.id.surfaceview);
            surfaceHolder = surfaceView.getHolder();
            surfaceHolder.addCallback(MainActivity.this);
            surfaceHolder.setType(SurfaceHolder.SURFACE_TYPE_PUSH_BUFFERS);
        }

        @Override
        public void onPermissionDenied(ArrayList<String> deniedPermissions) {
            Toast.makeText(MainActivity.this,"권한 거부",Toast.LENGTH_SHORT).show();
        }
    };
```
- PermissionListener를 이용해서 접근 허용이나 거부 시에 실행할 코드를 작성할 수 있음
- PermissionGranted는 접근 서용시에 실행할 코드를 뜻함
- 접근을 허용할 시에 카메라를 open하고 setDisplayOrientation을 이용해 90도의 각도에서도 사용할 수 있도록 함
- PermissionDenied는 권한이 거부당했을 시에 실행하는 코드로 Toast를 이용해 권한이 거부당했음을 알림

### 7) SurfaceView의 구성
```
@Override
    public void surfaceCreated(@NonNull SurfaceHolder holder) {
    }
    private void refreshCamera(Camera camera) {
        if(surfaceHolder.getSurface() == null){
            return;
        }
        try {
            camera.stopPreview();
        }catch (Exception e){
            e.printStackTrace();
        }
        setCamera(camera);
    }
    private void setCamera(Camera cam) {
        camera = cam;
    }
    //서페이스뷰에서 변화가 일어났을때 호출 + 초기화
    @Override
    public void surfaceChanged(@NonNull SurfaceHolder holder, int format, int width, int height) {
        refreshCamera(camera);
    }
    @Override
    public void surfaceDestroyed(@NonNull SurfaceHolder holder) {
    }
```
- surfaceCreated는 서페이스 뷰가 처음으로 만들어졌을 때 실행하는 부분
- refreshCamera는 만약 서페이스뷰로 나타나는 이미지가 없을 경우에는 다시 시도하도록 하는 메소드
- try-catch를 이용해 예외상황을 나타낼 수 있도록 함
- surfaceChanged는 서페이스 뷰에서 변화가 일어났을 때 호출되며 초기화하는 부분
