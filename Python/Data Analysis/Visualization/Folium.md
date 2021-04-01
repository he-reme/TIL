# Folium

> 지도 활용
>
> `exam7`

* 동적 지도 처리

#### 설치

```shell
conda install -c conda-forge folium
```

#### 임포트

```python
import folium
```



---



## 지도 만들기

* 맵 객체 생성

  ```
  test_map = folium.Map(location=[위도, 경도], zoom_start=12)
  ```
  * `location`
    * 중심 좌표
  * `tiles`
    * 지도에 필터 적용. 생략 시 보통 지도
    * `'Stamen Terrain'`
    * `'Stamen Toner'`

* 마커 추가

  ```python
  folium.Marker([lat, lng], popup='팝업메시지').add_to(test_map)
  ```

  * 원형 마커

    ```python
    folium.CircleMarker(
    	[lat, lng],
    	radius=10,         # 원의 반지름
        color='brown',         # 원의 둘레 색상
        fill=True,
        fill_color='coral',    # 원을 채우는 색
        fill_opacity=0.7, # 투명도    
        popup='팝업메시지'
    ).add_to(seoul_map)
    ```

  * 지도 위에 직접 찍고, 팝업도 추가하기

    ```python
    test_map.add_child(folium.ClickForMarker(popup='내가 찍음!!'))
    ```

    

---



## 지도 저장하기

* html 파일로 저장

  ```python
  test_map.save('output/test.html')
  ```

  

---



## 예제

* 마커 여러개 표시하기

  ```python
  import pandas as pd
  import folium
  
  # 대학교 리스트를 데이터프레임 변환
  df = pd.read_excel('./data/서울지역 대학교 위치.xlsx')
  
  # 서울 지도 만들기
  seoul_map = folium.Map(location=[37.55,126.98], tiles='Stamen Terrain', 
                          zoom_start=12)
  
  # 대학교 위치정보를 Marker로 표시
  for name, lat, lng in zip(df.index, df.위도, df.경도):
      folium.Marker([lat, lng], popup=name).add_to(seoul_map)
  display(seoul_map)
  
  # 지도를 HTML 파일로 저장하기
  seoul_map.save('output/seoul_colleges.html')
  ```

* 단계 구분도

  ```python
  import json
  geo_path = 'data/seoul_geo.json'
  geo_str = json.load(open(geo_path, encoding='utf-8'))
  pop = pd.read_csv("./data/cctv_seoul.csv")
  pop.head()
  ```

  ```python
  map = folium.Map(location=[37.5502, 126.982], zoom_start=11,
                   tiles='Stamen Toner',doubleClickZoom=False)
  fmap=folium.Choropleth(geo_data = geo_str,
                 data = pop,
                 columns = ['구별', '인구수'],
                 fill_color = 'YlGnBu',
                 key_on='feature.properties.name').add_to(map)
  fmap.geojson.add_child(
      folium.features.GeoJsonTooltip(['name'],labels=False)
  )
  display(map)
  ```

  * GeoJSON
    * 위치 정보를 갖는 점을 기반으로 체계적으로 지형을 표현하기 위해 설계된 개방형 공개 표준 형식
    * `[위도, 경도]` 묶음으로 작성되어있음

