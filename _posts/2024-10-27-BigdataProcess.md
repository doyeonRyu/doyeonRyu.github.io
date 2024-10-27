---
layout: single
title: "데이터 분석 프로세스"
categories: python
tag: [python, Bigdata]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

--- 
# 1. Objective Setting
---   

- 목표 정의 및 성공 기준 설정

# 2. Data Curation
---   
- 목적을 충족하는 데 필요한 데이터를 결정
- 데이터 수집
- 데이터 저장
- 품질과 양이 분석에 적합한지 확인

# 3. Exploratory Data Analysis (EDA)
---   
- 데이터 분포와 패턴 탐색
    - 중심 경향과 분산 파악
    - 평균, 중앙값, 범위, 분산, 표준 편차 등
- 이상치 및 결측치 파악
- 주요 변수 간 관계 시각화
- 통계적 기법, 데이터 시각화 도구 사용
    - Boxplot, histogram, scatterplot, ploty, seaborn, …
- 데이터가 프로젝트에 적절한지 적합성 확인

# 4. **Data Preprocessing**
---   
- 데이터 재구성
- dirty data 정제
    - 중앙값, 평균, 최빈값 등으로 변경하기 or drop하기 등 선택
    - 결측치(Nan)
    - 이상치(Outlier)
    - 필요없는, 사용할 수 없는 데이터
- 텍스트 데이터 전처리
- 데이터 스케일링(데이터 normalization, standardization)
    - Min-Max Scaling**:** 데이터 범위를 0과 1 사이로 변환하여 값들을 정규화
    - Standard Scaling**:** 데이터의 평균을 0, 표준편차를 1로 변환하여 정규 분포 형태로 만듦
    - Log Normalization: 값의 스케일 차이가 큰 경우 로그 변환을 통해 스케일을 줄임
- 범주형 변수 인코딩
    - label encoding: 범주형 변수를 순차적인 정수 값으로 변환(0, 1, 2, 3)
    - one-hot encoding: 범주형 변수를 이진 벡터로 변환하여 표현(0, 1)
- 피처 엔지니어링
    - 필요한 열 생성
    - 필요한 열만 추출
    - 열 병합, 축소
- 전처리 파이프라인 구축
- **모델링에 적합한 형태로 변환 완료**

# 5. Data Analysis
---   
- 모델 개발(머신러닝, 딥러닝)
    - train data를 통해 모델 학습
- 테스트
    - valid data로 모델 검증
    - Hold-out method, K-fold cross validation method
    - 과적합, 일반화 성능 점검
- 하이퍼 파라미터 최적화
    - Grid search
    - Randomized search
- 앙상블 러닝
    - Bagging method
        - Random forest: 다수의 decision tree 훈련
    - Boosting method
        - AdaBoost
        - Gradient Boosting
            - XGBoost
            - LightGB
- 패턴 발견 및 통찰 도출

# 6. Evaluation  
---   
- test data를 통해 결과 예측
- 모델 성능 평가
    - Regressor
        - MAE, MSE, MPE, MAPE, RMSE, SST
    - Classification
        - confusion matrix
            - Precision / Recall   
        | 실제값\예측값 | Yes | No  |   
        |--------------|-----|-----|   
        | Yes          | TP  | FN  |   
        | No           | FP  | TN  |   
        - ROC
    - Clustering
        - Elbow method
        - Silhouette index
- 모델 개선
- 성능 및 한계 검토

# 7. Deployment
---   
- 실제 환경에 모델 배포
- 지속적 모니터링
- 피드백 반영 및 유지보수