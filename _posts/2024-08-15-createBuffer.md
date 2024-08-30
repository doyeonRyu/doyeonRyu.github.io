---
layout: single
title: "서울 지하철 역 지도에 표시하고, 버퍼 생성하기"
categories: gis
tag: [python]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

# python과 folium을 통해 서울 지하철 역을 지도에 표시하고 버퍼 생성하기     
> 데이터 출처: [서울 열린데이터 광장 | 서울시 역사마스터 정보](https://data.seoul.go.kr/dataList/OA-21232/S/1/datasetView.do)   
> 서울의 지하철역이 너무 많아 2호선을 예로 진행했다.   
> 모든 코드가 궁금하다면 [https://github.com/doyeonRyu]https://github.com/doyeonRyu 를 참고  
> 지도 출력을 위해 주피터 노트북을 사용했다.    

## 파이썬 코드

### 사용할 라이브러리 불러오기   
```python
import folium
from folium.plugins import FloatImage
import pandas as pd
from folium import Marker
```

### 지하철 역 정보 csv 파일 불러오기   
```python
# 서울 지하철역 데이터 불러오기
station = pd.read_csv("서울시 역사마스터 정보.csv", encoding='cp949')
station.head()
```

### 서울을 표시하는 지도 생성하기   
```python
# 서울 지도 만들기     
seoul_map = folium.Map(location=[37.55,126.98],zoom_start=12)
seoul_map
```

### 2호선의 모든 역을 표시하고 반경 1km를 원으로 표시하기   
```python
# 반경 1km를 미터로 변환
buffer_size_km = 1
buffer_size_m = buffer_size_km * 1000

# 2호선 역 표시하고 반경 1km 원 표시
for i in range(len(station)):
    if station['호선'][i] == "2호선":
        color = 'green'

        Marker([station['위도'][i],station['경도'][i]],
               popup=station['역사명'][i], 
               icon=folium.Icon(color = color, icon='bookmark')
               ).add_to(station_map)
        
        folium.Circle(
            location=[station['위도'][i], station['경도'][i]],
            radius=buffer_size_m,  # radius in meters
            color='red',
            fill=True,
            fill_opacity=0.2
        ).add_to(station_map)

# 2호선 레전드 추가
legend_html = '''
     <div style="
     position: fixed; 
     top: 50px; right: 50px; width: 150px; height: 90px; 
     border:2px solid grey; z-index:9999; font-size:14px;
     background-color:white; opacity: 0.8;
     ">
     <p style="margin:10px;"><b>Legend</b></p>
     <p style="margin:10px;"><i style="color:red; font-size:18px;" class="fa fa-circle"></i> 2호선 반경 1km</p>
     </div>
     '''

# 지도에 레전드 추가
station_map.get_root().html.add_child(folium.Element(legend_html))

# 지도에 나침반 추가
compass_rose = folium.FeatureGroup('compass rose')
FloatImage('https://upload.wikimedia.org/wikipedia/commons/9/99/Compass_rose_simple.svg', bottom =80, left = 7).add_to(compass_rose)
compass_rose.add_to(station_map)

# 지도 출력
station_map
```

### html 파일로 저장하기
```python
# HTML 파일로 저장
station_map.save('2호선_역정보.html')
```  


# 결과 - 2호선_역정보.html   

![image](https://github.com/user-attachments/assets/3ea83f36-d288-46e8-b020-b08e21eeef1d)

# 고찰   

사람이 걸어갈 수 있는 거리를 반지름 1km로 가정해서 반지름이 1km인 버퍼를 생성하였다.   
모든 지하철역을 기존 지도에 나와있는 색으로 변경하여 생성하면 구분이 쉬울 것으로 예상되어 우선적으로 2호선의 초록색을 표시하여 나타내었다.   
역들을 지도에 표시하고 반경을 버퍼로 표현함으로써 지하철역과 주변 상권, 주거지를 분석하고 대중교통이 불리한 지역들을 선별하여 접근성을 강화시킬 수 있을 것으로 예상된다.   
또한 유동 인구를 분석해 지하철 노선을 최적화하거나 개선에 도움을 줄 수 있다.   
