<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
    <title>간단한 지도 표시하기</title>
    <script type="text/javascript" src="https://openapi.map.naver.com/openapi/v3/maps.js?clientId=8Qu0MocZu3O0FV2iEegs&callback=CALLBACK_FUNCTION&submodules=geocoder"></script>


</head>
<body>
<div id="map" style="width:400px;height:400px;"></div>


<script>
var lat, lng;
function getLocation() {
  if (navigator.geolocation) { // GPS를 지원하면
    navigator.geolocation.getCurrentPosition(function(position) {
      lat=position.coords.latitude;
	  lng=position.coords.longitude;
    }, function(error) {
      console.error(error);
    }, {
      enableHighAccuracy: false,
      maximumAge: 0,
      timeout: Infinity
    });
  } else {
    alert('GPS를 지원하지 않습니다');
  }
}
getLocation();


url_0='http://map.naver.com/index.nhn?slat=';
url_1=lat;
url_7='&slng=';
url_3=lng;
url_8='&stext=';
url_5='한라';
url_9='&elat=';
url_2='&elng=';
url_4='&etext=';
url_6='&menu=route&pathType=3';

setTimeout("t2()",4000);

function t2(){
naver.maps.Service.reverseGeocode({
        location: new naver.maps.LatLng(lat, lng),
    }, function(status, response) {
        if (status !== naver.maps.Service.Status.OK) {
            return alert('Something wrong!');
        }

        var result = response.result, // 검색 결과의 컨테이너
            items = result.items; // 검색 결과의 배열
			items[0].point.x=lng;
			items[0].point.y=lat;
			f1.lb1.value=items[0].point.x;
			f1.lb2.value=items[0].point.y;
			url_1=lat;
			url_3=lng;
			console.log();
			ad=items[0].address;
			url_5=ad;
			f1.lb0.value=ad;
			
		var map = new naver.maps.Map("map", {
    center: new naver.maps.LatLng(items[0].point.y, items[0].point.x),
    zoom: 10,
    mapTypeControl: true
});

var marker = new naver.maps.Marker({
    position: new naver.maps.LatLng(items[0].point.y, items[0].point.x),
    map: map
});
        // do Something
    });
}



function t1(){


ad = f1.lb3.value;

naver.maps.Service.geocode({
        address: ad
    }, function(status, response) {
        if (status === naver.maps.Service.Status.ERROR) {
            return alert('Something wrong!');
        }

        var result = response.result, // 검색 결과의 컨테이너
            items = result.items;// 검색 결과의 배열
			console.log(result);
			f1.lb1.value=items[0].point.x;
			f1.lb2.value=items[0].point.y;
url_main=url_0+url_1+url_7+url_3+url_8+url_5+url_9+items[0].point.y+url_2+items[0].point.x+url_4+ad+url_6;
			f1.lb4.value=url_main;
        // do Something
		
	var map = new naver.maps.Map("map", {
    center: new naver.maps.LatLng(items[0].point.y, items[0].point.x),
    zoom: 10,
    mapTypeControl: true
});//지도재지정

var marker = new naver.maps.Marker({
    position: new naver.maps.LatLng(items[0].point.y, items[0].point.x),
    map: map
});//마커재지정
	
    });
}	
</script>
<form name="f1">
<input type = "label" value="1" name ="lb0" size="35px">
<input type = "label" value="1" name ="lb1">
<input type = "label" value="1" name ="lb2"> <br>
<input type = "text" value="" name="lb3" size="35px">
<input type = "button" value="누르세요" name="btn0" onclick="t1()">
<input type = "label" value="1" name ="lb4">
<button type = "button" name="btn1" onclick="location.href=f1.lb4.value">길찾기</button>
</form>
</body>
</html>
