# leaflet

#### 패키지

```R
install.packages("leaflet")
library(leaflet)
```

#### 기본

```R
# 지도 배경 그리기
leaflet()

# 지도 배경에 타일깔기 (빈 세계지도)
leaflet() %>% addTiles() 

# 지도 배경에 센터 설정하기. setView만 하면 값만 반영됨. 맵 안보임.
map0 <- leaflet() %>% setView(lng = lng값, lat = lat값, zoom = 16)  
map0

# 지도 배경에 센터 설정하고 타일깔기. addTiles해줘야 맵 보임
map1 <- map0 %>% addTiles() 
map1
```

#### 저장

```R
install.packages("htmlwidgets")
library(htmlwidgets)
saveWidget(map, file="output/mymap.html")
```



---



## 예제

#### 원하는 위치에 있는 원을 누르면 팝업창 띄우기

* `dplyr` 사용
* `popup`

```R
mk <- multi_lonlat
lon <- mk$lon
lat <- mk$lat

# 팝업 메시지
msg <- '<strong><a href="http://www.multicampus.co.kr" style="text-decoration:none" >멀티캠퍼스</a></strong><hr>우리가 공부하는 곳 ㅎㅎ'

map <- leaflet() %>% 
	setView(lng = mk$lon, lat = mk$lat, zoom = 16) %>% addTiles() %>%
	addCircles(lng = lon, lat = lat, color='green', popup = msg )
map
```

#### 맵 로드 하자마자 해당 위치에 팝업창 먼저 보여주기

* `addPopups()`

```R
content <- paste(sep = '<br/>',"<b><a href='https://www.seoul.go.kr/main/index.jsp'>서울시청</a></b>",'아름다운 서울','코로나 이겨냅시다!!')
map<-leaflet() %>% addTiles() %>%  addPopups(126.97797, 37.56654, content1)
map
```

