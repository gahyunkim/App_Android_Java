# GoogleMap 연동하기 & 화면으로 보여주기
### 1) 화면 구성하기
```
<fragment
        android:id="@+id/googleMap"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        class="com.google.android.gms.maps.MapFragment"/>
```
- 구글맵이 전체 화면에 나타날 수 있게 fragment를 match_parent로 지정해줌

### 2) GoogleMap 연동
- googleMap을 연동하기 위해 검색창에 구글맵콘솔을 입력
- 프로젝트 만들기를 한 후 api키를 찾아 복사함
- Manifest 내부에 meta-data 를 추가함
```
<meta-data
            android:name="com.google.android.geo.API_KEY"
            android:value="API키 내용 입력"/>
```
- 생성한 API키를 value에 입력하여 googleMap을 사용할 수 있도록 함
- buildgradle 내부에는 implementation을 통해 google.android로 맵을 사용할 수 있도록 만들어줌

### 3) MainActivity 구성하기
```
private FragmentManager fragmentManager;
private MapFragment mapFragment;
...
fragmentManager = getFragmentManager();
mapFragment = (MapFragment)fragmentManager.findFragmentById(R.id.googleMap);

mapFragment.getMapAsync(this);
```
- private로 사용할 FragmentManager와 MapFragment를 선언함
- fragmentManager를사용하기 위해 getFragmentManager()를 해줌
- mapFramgment도 findFragmentById를 이용해 위치를 찾아줌

### 4) onMapReady 메소드 구성하기
```
@Override
    public void onMapReady(GoogleMap googleMap) {
        LatLng location = new LatLng(37.485249, 126.901594);
        MarkerOptions markerOptions = new MarkerOptions();
        markerOptions.title("구로디지털단지역");
        markerOptions.snippet("전철역");
        markerOptions.position(location);
        googleMap.addMarker(markerOptions);

        googleMap.moveCamera(CameraUpdateFactory.newLatLngZoom(location,16));
    }
```
- 이 메소드는 구글맵이 준비되면 이쪽으로 호출되도록 하는 역할
- LatLng는 위도와 경도의 위치를 지정할 수 있도록 함
- markOptions를 새롭게 선언해주고 title을 만들어줌
- snippet는 세부적인 내용을 적을 수 있는 공간
- moveCamera는 카메라를 움직이고 줌을 얼마나 할 것인지를 결정할 수 있음

