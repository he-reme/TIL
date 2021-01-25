# Map

> 구글맵으로 학습함

## window.navigator.geolocation 객체

> 위치 요청에 대해 사용자가 동의하면
>
> 브라우저의 위치 정보가 반환됨



---



## 위치 정보 권한 설정

> \+ 위치 정보 반환하기

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8'>
</head>
<body>
	<p id="demo">위치정보를 추출하려면 실행 버튼을 클릭하세요:</p>
	<button onclick="getLocation()">실행</button>
	
	<script>
    	var x=document.getElementById("demo");
		function getLocation() {
        	if (navigator.geolocation) { 
        		navigator.geolocation.getCurrentPosition(showPosition,showError);
        	}
        	else {
        		x.innerHTML=" 이 브라우저는 geolocation을 지원하지 않습니다.";
        	}
      	}
      	function showPosition(position) {
         	x.innerHTML="위도: " + position.coords.latitude + "<br />경도: " + position.coords.longitude;       
      	}
      	function showError(error) {
        	switch(error.code) {
            	case error.PERMISSION_DENIED:
                	x.innerHTML="사용자가 위치 기능 사용을 거부했습니다."
                	break;
            	case error.POSITION_UNAVAILABLE:
                	x.innerHTML="위치를 구할 수 없습니다.";
                	break;
            	case error.TIMEOUT:
                	x.innerHTML="사용자가 위치 기능 사용을 거부했습니다.";
                	break;
            	case error.UNKNOWN_ERROR:
                	x.innerHTML="기타 에러";
         	}
      	}
	</script>
</body>
</html>
```



---



## 주소와 좌표(위도, 경도)  변환 프로그램

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
</head>
<body>
	<h1>주소와 좌표 변환 프로그램</h1>
	<button onclick="addToCoord();">주소를 좌표로</button>
	<button onclick="coordToAddr();">다시 주소로</button>
	<script>
	var latlng;
		function addToCoord() {
			var address = prompt("주소를입력하세요");
			var lat;
			var lng;
			if (address) {
				$.getJSON("https://maps.googleapis.com/maps/api/geocode/json?key=[google key]&address="+encodeURIComponent(address), function(data) {
					lat = data.results[0].geometry.location.lat;
					lng = data.results[0].geometry.location.lng;
					alert("좌표로 : " + lat + ":" + lng);		
					latlng = encodeURIComponent(lat+","+lng);											
				});		
				
			}
		}
	    function coordToAddr() {
	    	$.getJSON("https://maps.googleapis.com/maps/api/geocode/json?key=[google key]&latlng="+latlng, function(data) {
				alert("다시 주소로 : " + data.results[0].formatted_address);
			});
	    }
	</script>
</body>
</html>
```



---



## 구글 맵 그리기

```html
<!DOCTYPE html>
<html>
  <head>
  	<meta charset='utf-8'>
    <title>Simple Map</title>
     <script src="https://maps.googleapis.com/maps/api/js?key=[google key]" ></script>
    <style type="text/css">
       #map {
        height: 600px;
        width: 100%; 
      }
    </style>   
  </head>
  <body>
    <h1>구글 지도 출력</h1>
    <hr>
    <div id="map"></div>
     <script>
		var dom = document.getElementById("map");
		if(dom) {
			var latlng = { lat: [위도], lng: [경도]};
            // 맵 그리기
			var map = new google.maps.Map(dom, {
            	center: latlng,
            	zoom: 16
          	});
            // 현재 위치 마커 찍기
			new google.maps.Marker({position: latlng, map: map});
        }      
    </script>
  </body>
</html>
```



---



## 마커 클릭 시 정보 출력하기

```html
<!DOCTYPE html>
<html>
  <head>
  	<meta charset='utf-8'>
    <title>Simple Map</title>
     <script src="https://maps.googleapis.com/maps/api/js?key=[google key]" ></script>
    <style type="text/css">
       #map {
        height: 600px;
        width: 100%; 
      }
    </style>   
  </head>
  <body>
    <h1>구글 지도 출력</h1>
    <hr>
    <div id="map"></div>
     <script>
		var dom = document.getElementById("map");
		if(dom) {
			var latlng = { lat: [위도], lng: [경도]}
			var map = new google.maps.Map(dom, {
            	center: latlng,
            	zoom: 16
          	});
			var marker = new google.maps.Marker({position: latlng, map: map});
			
			var contentString = "<h3>현재 위치입니당!<img src='../images/clover.png' width='20'></h3>";
			
			var infowindow = new google.maps.InfoWindow({
			    content: contentString
			});
			
			marker.addListener('click', function() {
			    infowindow.open(map, marker);
			});
        }     
    </script>
  </body>
</html>
```

