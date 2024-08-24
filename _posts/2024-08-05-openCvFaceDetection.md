---
layout: single
title: "python과 openv를 활용해 얼굴 인식하기"
categories: python
tag: [python, openCv]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

## 개요   
>> 1. opencv를 통해 노트북의 카메라를 열어 사람을 인식   
>> 2. 사람 수를 인식해 화면에 사람 수 출력   
>> 3. 웹캠 화면을 비디오로 저장   
>> 4. ['Frame', 'Timestamp', 'face_count']의 형태의 데이터로 csv 파일로 저장   
>> \* 사람 얼굴을 인식하기 위해 Haar Cascade Classifier를 사용함!   
>> https://github.com/opencv/opencv/tree/master/data/haarcascades   

---   

## 결과   
### 웹캠 사진   
\!\[image1](이미지주소)   
사람 수에 따라 숫자가 바뀌는 것을 확인할 수 있다.   
이 웹캠은 따로 비디오로 저장함.   

### csv 파일   
\!\[image2](이미지주소)   
결과를 csv파일로 프레임 당 저장함으로써 건물 유입 인구 수, 혼잡 정도를 파악할 수 있을 것으로 기대된다.   
또한, 온도, 습도등의 기능을 추가하여 건물 내 쾌적성 향상에 도움을 줄 수 있을 것으로 예상된다.   

## python code    
아래의 깃허브 참고!   
\[github](링크)  
