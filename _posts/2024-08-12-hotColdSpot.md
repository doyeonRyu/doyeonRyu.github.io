---
layout: single
title: "Hot spot & Cold spot: 대한민국 시군구별 인구 시각화"
categories: python
tag: [python, gis]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

## 시군구 인구 데이터와 최신 행정구역 데이터를 통해 대한민국 인구 hotspot & coldspot 시각화하기   

> 데이터 출처
> 행정안전부_지역별(법정동) 성별 연령별 주민등록 인구수: [https://www.data.go.kr/data/15099158/fileData.do](https://www.data.go.kr/data/15099158/fileData.do)   
> \* 지역별 인구를 통해 시군구 인구 데이터로 병합함   
> 대한민국 최신 행정구역 데이터: [http://www.gisdeveloper.co.kr/?p=2332](http://www.gisdeveloper.co.kr/?p=2332)      



## 파이썬 코드   

### 라이브러리, 데이터 불러오기   
```python
# 라이브러리 불러오기
import pandas as pd
import geopandas as gpd
import numpy as np
import matplotlib.pyplot as plt

# 데이터 불러오기
sig = gpd.read_file('gis/sig/sig.shp', encoding="cp949")
population = pd.read_csv('gis/행정안전부_지역별(법정동) 성별 연령별 주민등록 인구수_20240731.csv', encoding='cp949')
```

### 데이터 전처리 과정   
```python
# 데이터 전처리   

# 필요한 열만 남기고 나머지 drop
population = population[['법정동코드', '시군구명', '읍면동명', '리명', '계']]

# '시군구명'을 기준으로 데이터를 그룹화하고, '계' 값을 합산
population = population.groupby('시군구명')['계'].sum().reset_index()

# sig와 population을 시군구명 기준으로 병합
sig = sig.merge(population, how='left', left_on='SIG_KOR_NM', right_on='시군구명')

# 시군구명 열 중복이므로 삭제
sig = sig.drop(columns=['시군구명'])

# 결과 확인
# print(sig)
```

### hotspot 시각화하기
```python
# 데이터를 통해 시군구의 인구를 hotspot과 coldspot으로 시각화 하기
sig.plot(column='SIG_CD', cmap='coolwarm')
plt.title("시군구 Hotspot & Coldspot")
plt.show()
```

## 결과 확인   
![시군구인구hotspot](https://github.com/user-attachments/assets/f165f18e-8460-4371-9274-f7bd9dad5230)

## 마무리   
시각화 과정에서 폰트 문제로 한글이 깨지는 문제가 발생했다.    
이는 다음에 다루어 보도록 하겠다.   

인구 데이터를 새로 받아와서 시각화를 진행했지만 그냥 행정구역 데이터에서 column을 시군구 코드를 기준으로 시각화해도 결과가 같게 나온다.    