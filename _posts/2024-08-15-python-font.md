---
layout: single
title: "python matplotlib 사용할 때 한글 폰트 깨짐 해결하기"
categories: python
tag: [python, matplotlib]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

> python에서 matplotlib을 사용해 그래프를 그리는 과정에서 한글로 작성한 부분이 네모 박스로 나타나는 것을 해결하고자 하였다.   

## 1. 기존 컴퓨터에 깔려 있는 폰트 활용하기   

### 라이브러리 설치하기
```bash
pip install matplotlib 
```

### 가지고 있는 폰트 확인하기
```python
from matplotlib import font_manager
font_manager.findSystemFonts()
```

위의 코드를 실행하면 다음과 같이 **C:\\Windows\\Fonts**에 들어있는 모든 폰트를 보여준다.   
여기서 원하는 것을 골라서 사용하면 된다.   
![image](https://github.com/user-attachments/assets/e2d24a7e-cd90-4be7-a3f9-2f8de57b5d34)

### 폰트 적용하기   
```python
import matplotlib.pyplot as plt

plt.rcParams['font.family'] ='malgun.ttf'
```

두 번째 코드는 마이너스 부호에서 오류가 나는 경우이다.   
다음의 코드에서 False로 해주면 된다. 
```python
import matplotlib.pyplot as plt

plt.rcParams['axes.unicode_minus'] = False # 음수가 오류나는 경우  
```

### 결과 확인

- 이전 결과   
![시군구인구hotspot](https://github.com/user-attachments/assets/55867acd-2663-449c-af8f-32e177cf3a6e)   

- 한글 폰트 적용 후   
![시군구인구hotspot맑은고딕](https://github.com/user-attachments/assets/705c29ca-b9b8-4c72-8c04-354a4d2f343d)   


## 2. 원하는 폰트 다운로드해 활용하기   
### 원하는 폰트 고르고 다운로드하기    
여러 블로그를 찾아보다가 나눔고딕 D2coding 폰트가 python에 적합한 글꼴이라는 말이 많아 깔아볼 겸 적용해 보기로 하였다.   

네이버 폰트 다운로드 사이트에서 나눔고딕 D2coding 글꼴을 다운해 주면 된다.   
[네이버 폰트 다운로드 사이트](https://hangeul.naver.com/fonts/search?f=nanum)   

다운 후 압출을 풀러 폴더 안의 폰트 파일을 더블 클릭 후 설치해 주면 된다.   

### 다운로드한 폰트 경로 찾기   
설치를 하고 나면 경로를 모르는 경우가 많은데 이럴 경우 검색에서 글꼴 설정을 치고 들어가서 

![image](https://github.com/user-attachments/assets/609859ee-0837-42cb-9466-30ea8caa762e)

아래 사진의 글꼴 파일에서 경로를 찾을 수 있다.   

![image](https://github.com/user-attachments/assets/3d70b35a-6433-4f30-a209-30af359a5ca4)

---   

또 다른 방법은   
다시 **C:\\Windows\\Fonts** 여기서 d2coding을 찾으니 저장이 잘 되어 있길래 우클릭해 속성에 들어가서 찾을 수 있었다.    

### 폰트 잘 다운로드 됐는지 확인하기 

```python
import os

font_path = 'C://Users//USER//AppData//Local//Microsoft//Windows//Fonts//D2Coding-Ver1.3.2-20180524-all.ttc'  # 경로를 시스템에 맞게 조정하기
if not os.path.exists(font_path):
    print("폰트 파일이 존재하지 않습니다.")
else: 
    print("폰트 파일이 존재합니다.")
```

### 폰트 적용하기 
폰트 적용은 위와 동일한 방법으로 하면 된다.   
```python
import matplotlib.pyplot as plt

plt.rcParams['font.family'] ='D2Coding-Ver1.3.2-20180524-all.ttc'
```

### 출처   
다음의 글을 읽고 참고하여 d2coding 폰트를 저장함    
[https://blog.naver.com/jazzlubu/222851163855](https://blog.naver.com/jazzlubu/222851163855)

## 고찰   
잘 되다가도 왜 같은 코드를 여러 번 반복해서 실행하면 폰트가 없다고 뜰까...   