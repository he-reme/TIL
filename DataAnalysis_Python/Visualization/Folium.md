# Folium

> 지도 활용
>
> `exam7`

* 동적 지도 처리
* Python에서 사용 가능한 라이브러리로서 지도를 다루는 대표적인 라이브러리
* leaflet.js 기반으로 지도를 그려주고, 모바일에서도 쓸 수 있을 만큼 가벼움

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

  * 마커 아이콘 바꾸기
  
    `https://mkjjo.github.io/python/2019/08/11/folium.html` 참고..
  
    * 예제
  
      ```python
      import folium
      
      # 서울 지도 만들기
      hoho = [37.5729812, 126.990504 ]
      hoho_map = folium.Map(location=hoho, zoom_start=16)
      
      icon = folium.Icon(icon='star', color='purple') # 아이콘 설정
      
      folium.Marker(hoho, tooltip='호호식당', icon = icon).add_to(hoho_map)
      display(hoho_map)
      
      hoho_map.save('hw5.html')
      ```
  
      

---



## 지도 저장하기

* html 파일로 저장

  ```python
  test_map.save('output/test.html')
  ```

  

---



## 단계 구분도

> Choropleth map

* 각기 다른 음영이나 색상 또는 값으로 각 지역과 관련된 데이터를 표현한 지도
* 두 데이터를 파라미터로 넘겨줘야 하는데 데이터는 각자 다른 파일에 있으므로, **시각화할 데이터를 지도에 얹으려면 두 데이터를 매핑해야 함**
  * **지도 데이터 파일** (.geojson 혹은 .json)
    * 지역에 대한 경계 정보를 제공
  * **시각화하고자 하는 데이터 파일** (.csv 등)
    * 지역별로 표현하고자 하는 데이터를 제공
* GeoJSON
  * 위치 정보를 갖는 점을 기반으로 체계적으로 지형을 표현하기 위해 설계된 개방형 공개 표준 형식
  * `[위도, 경도]` 묶음으로 작성되어있음

```python
folium.Choropleth(
	geo_data = "지도 데이터 파일 경로 (.geojson, geopandas.DataFrame)"
	data = "시각화 하고자 하는 데이터파일. (pandas.DataFrame)"
	columns = (지도 데이터와 매핑할 데이터, 시각화 하고려는 데이터),
	key_on = "지도 데이터 파일에서 데이터 파일과 매핑할 값 feature.properties.xxx",
	fill_color = "시각화에 쓰일 색상",
	[fill_opacity=, line_opacity= ,]
	legend_name = "칼라 범주 이름",
).add_to(m)
```

```python
m.save('output/map.html') # 저장
```



* 예시1

  ```python
  # 팝업처리 추가
  import pandas as pd
  import folium
  import json
  
  # 경기도 인구변화 데이터를 불러와서 데이터프레임으로 변환
  file_path = 'data/경기도인구데이터.xlsx'
  df = pd.read_excel(file_path, index_col='구분')  
  df.columns = df.columns.map(str)
  
  # 경기도 시군구 경계 정보를 가진 geo-json 파일 불러오기
  geo_path = 'data/경기도행정구역경계.json'
  try:
      geo_data = json.load(open(geo_path, encoding='utf-8'))
  except:
      geo_data = json.load(open(geo_path, encoding='utf-8-sig'))
  
  #print(geo_data)
  
  # 경기도 지도 만들기
  g_map = folium.Map(location=[37.5502,126.982], 
                     tiles='Stamen Terrain', zoom_start=9)
  
  test = folium.Html('<b>Hello world</b>', script=True)
  
  popup = folium.Popup(test, max_width=2650)
  
  # 출력할 연도 선택 (2007 ~ 2017년 중에서 선택)
  year = '2017'  
  
  # Choropleth 클래스로 단계구분도 표시하기
  fmap=folium.Choropleth(geo_data=geo_data,    # 지도 경계
                   data = df[year],      # 표시하려는 데이터
                   columns = [df.index, df[year]],  # 열 지정
                   fill_color='YlOrRd', fill_opacity=0.7, line_opacity=0.3,
                   threshold_scale=[10000, 100000, 300000, 500000, 700000],               
                   key_on='feature.properties.name',
                   highlight=True
                   
                   ).add_to(g_map)
  fmap.geojson.zoom_on_click = False
  fmap.geojson.add_child(
      folium.features.GeoJsonPopup(['name'],labels=False)
  )
  
  display(g_map)
  # 지도를 HTML 파일로 저장하기
  g_map.save('output/gyonggi_population_' + year + '_3.html')
  
  ```

* 예시2 (인구수에 따라 지도로 나타내기)

  ```python
  import json
  #geo_path = 'data/hankuk1_geo.json' # 서울시 동 별 지도
  geo_path = 'data/seoul.geojson' # 서울시 지도
  geo_str = json.load(open(geo_path, encoding='utf-8'))
  
  pop = pd.read_csv("./data/cctv_seoul.csv")
  pop.head()
  ```

  ```python
  map = folium.Map(location=[37.5502, 126.982], zoom_start=11)
  fmap=folium.Choropleth(geo_data = geo_str,
                 data = pop,
                 columns = ['구별', '인구수'],
                 fill_color = 'YlGnBu',
                 key_on='feature.properties.name').add_to(map)
  fmap.geojson.zoom_on_click = False
  fmap.geojson.add_child(
      folium.features.GeoJsonTooltip(['name'],labels=False)
  )
  display(map)
  ```





---



## 예제

* 마커 여러개 표시하기

  ```python
  import pandas as pd
  import folium
  
  # 대학교 리스트를 데이터프레임 변환
  df = pd.read_excel('./data/서울지역 대학교 위치.xlsx')
  df.columns = ['학교명', '위도', '경도']
  print(df.head())
  seoul_map = folium.Map(location=[37.55,126.98], tiles='Stamen Terrain', 
                          zoom_start=12)
  
  # 대학교 위치정보를 Marker로 표시
  for name, lat, lng in zip(df.학교명, df.위도, df.경도):
      folium.Marker([lat, lng], popup=name).add_to(seoul_map)
  display(seoul_map)
  # 지도를 HTML 파일로 저장하기
  
  seoul_map.save('output/seoul_colleges.html')
  ```

