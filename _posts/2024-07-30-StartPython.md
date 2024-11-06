---
layout: single
title: "Window에서 Python 시작하기"
categories: python
tag: [python]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

## Anaconda 설치
> Window 기반에서 python을 작동하기 위해서 아나콘다가 필요하다.   
> **아나콘다란?**   
> 파이썬에서 필요한 라이브러리 설치, 버전 관리 등의 작업을 가능하게 한다.   
> 아래 링크에 들어가 window 버전 설치하기   
> [Anaconda Download](https://docs.anaconda.com/miniconda/)   

## Anaconda Prompt (miniconda3)
설치가 끝나면 Anaconda Prompt (miniconda3) 앱을 실행한다.
실행 후 프롬포트에 아래와 같이 명령어를 입력한다.   

버전이 출력되면 설치 완료   
![image](https://github.com/user-attachments/assets/aeeafabf-9bb8-4c7c-8761-285b2920d085)

```
# 버전 출력하기
conda --veriosn
python --version
```

## 가상환경 만들기
파이썬 실행 시에는 가사환경에서 하는 것이 라이브러리의 버전 충돌 문제 등을 해결하기 좋다.   

### 존재하는 가상환경 출력하기
```
conda env list
```
아래의 결과처럼 현재 사용 중인 가상환경이 출력된다.   
![image](https://github.com/user-attachments/assets/7de89d2d-bc93-4895-aa64-8b54b19510d9)

### 새 가상환경 생성하기
```
conda create -n test
# test: 새 가상환경 이름(원하는 이름으로 변경)
```

이 때, **Proceed ([y]/n)?** 이 뜨면 y를 입력한다.   

![image](https://github.com/user-attachments/assets/37e320dc-fb2e-4b90-a628-69925fa7d009)

이 후, 다시 한 번 가상환경 리스트를 출력하면 새로 추가된 것을 확인할 수 있다.   
```
conda env list
```
![image](https://github.com/user-attachments/assets/fc0f6053-e230-4da7-8d03-1ea87d8565f5)

### 새 가상환경으로 이동하기 
```
conda activate test
```
![image](https://github.com/user-attachments/assets/844a4e40-3f96-40e4-ba1c-164669000474)   

base에서 test로 변경된 것 확인하기   

## 가상환경에서 python 실행하기
### 파이썬 설치하기
```
python --version
```
파이썬 버전 확인 시 파이썬이 존재하지 않으면 아래의 명령문을 통해 깔아준다.   

```
conda install python=3.12
```
![image](https://github.com/user-attachments/assets/e64988e1-cba3-40a1-869c-4be94caa8aa1)   

이미 파이썬이 존재해서 그 과정은 패스하였다.   

### 파이썬 라이브러리 설치하기
numpy를 예시로 들었다.   
```
pip install numpy
```
![image](https://github.com/user-attachments/assets/9b8d85b2-3a0a-4634-89c6-59ae6e3a8c0b)

설치된 라이브러리 확인하기
```
conda list
```

### 파이썬 실행하기

python 명령문을 치면 python 실행 화면으로 넘어간다.   
\>\>\> 부분이 파이썬 코드 부분이다.   
```
python
```
파이썬 코드 작성 이후 exit()를 작성하면 python 실행 화면에서 나오게 된다.   
```
exit()
```

![image](https://github.com/user-attachments/assets/78fb40e0-f9e8-44cc-8a9e-88c95b4dab24)

## 가상환경 비활성화
해당 가상환경에서 나와 다시 base로 이동하려면 아래의 명령문을 입력한다.   
```
conda deactivate
```
![image](https://github.com/user-attachments/assets/4a3fddc2-5801-4197-8a9a-8ff8824555a8)


## 가상환경 삭제하기
```
conda remove -n test --all
```

![image](https://github.com/user-attachments/assets/f606d300-39a9-438b-8482-f7f63bb5bda0)

### 삭제 확인하기   
다시 한 번 가상 환경 리스트를 출력해 삭제됐는지 확인한다.   
```
conda env list
```
![image](https://github.com/user-attachments/assets/a8aa9854-8460-47e0-888e-c5016297b174)