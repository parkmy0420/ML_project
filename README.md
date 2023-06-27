<img width="1000" alt="스크린샷 2023-06-27 오후 9 43 03" src="https://github.com/parkmy0420/ML_project/assets/63055186/cbc99132-b511-4bc5-a2da-2d4b1f502810">

# 내 옷 좀 추천해 조!
> 의류 실측 데이터 기반 프리사이즈 분석 및 개인화 의류 추천 시스템

## 목차
[Introduction](#-introduction)
1. [Project Introduction](#1-Project-Introduction)
2. [Result Video](#2-Result-Video)
3. [Project Background](#3-project-background)

[Development Process](#%EF%B8%8F-development-process)
1. [Data Description](#1-Data-Description)
2. [EDA](#2-EDA)
3. [Preprocessing](#3-Preprocessing)
4. [Model](#4-Model)
5. [Limitations and Improvements](#5-Limitations-and-Improvements)

-------------
## 💡 Introduction

### 1. Project Introduction
#### “ 의류 실측 데이터 기반 프리사이즈 분석 및 개인화 의류 추천 시스템 ”
무신사에서 상의 데이터를 크롤링하여 획일화 된 사이즈 표기방식으로 변환하고, 사용자의 신체 정보에 따라 맞춤형 의류 추천 시스템을 구현  
<img width="600" alt="Untitled" src="https://github.com/parkmy0420/ML_project/assets/87077176/62abb6fb-7d58-4b74-b2da-d8d1e728e9e2">

### 2. Result Video
https://github.com/parkmy0420/ML_project/assets/87077176/5712b07e-9d10-4715-bde4-4e2fbd1790f2
 [Untitled.mp4](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ddb3edd5-2cc6-4dfd-b587-0a3c36ed3e89/Untitled.mp4)
    
### 3. Project Background
 - **"2017~2019년 사이 온라인 쇼핑몰 거래액  120% 증가"**  
  통계청 온라인쇼핑동향조사에 따르면 2017년 이후부터 지속적으로 온라인 쇼핑 거래액이 증가하고 있다.
 - **"프리사이즈 기준의 모호함"**  
  하지만, one 사이즈인 ‘프리사이즈’와 각 브랜드 별로 다른 사이즈 기준으로 인해 소비자들은 본인 체형에 맞는 사이즈 선택의 어려움을 겪고있다.  
  (출처 : [온라인 의류사업 지속적인 성장](http://dew.dothome.co.kr/2020/12/26/도대체-프리사이즈의-기준이-뭔가요-규제-없는-의/) / [프리사이즈 실태](http://www.storyofseoul.com/news/articleView.html?idxno=3710))
 
▷ 따라서, 프리사이즈 및 브랜드 별로 다른 사이즈 기준을 일관된 사이즈로 정립하고, 사용자의 특성(키, 몸무게, 성별), 태그를 입력 받아 고객의 특성에 맞는 제품 추천 시스템을 개발하고자 하였다.

----------

## ⚙️ Development Process
### 1. Data Description
<img width="600" alt="Untitled" src="https://github.com/parkmy0420/ML_project/assets/87077176/87f73b83-8947-4263-b68e-801fd0880ad5">

### 2. EDA
 - 제품 성별 비율 및 제품 내 프리사이즈 비율 확인  
<img width="600" alt="ratio graph" src="https://github.com/parkmy0420/ML_project/assets/87077176/0339237a-d69a-4a3e-8f76-fa0f9f415d63">

 - 사이즈 별 실측 데이터 확인(boxplot graph)  
<img width="600" alt="ratio graph" src="https://github.com/parkmy0420/ML_project/assets/87077176/b1619ebb-e91a-4144-8490-6a57892c2020">

### 3. Preprocessing
- 소매길이 컬럼 제거
  - 반팔, 긴팔, 민소매의 구분이 되어있지 않아 사이즈별 소매길이가 상관관계가 없음
- Null 값 및 중복 사이즈 데이터 삭제
- 성별 컬럼의 ‘라이프’ 삭제
  - 19개의 행이있으며, 객관적인 성별의 구분이 어려움
- 특정 브랜드(GLIMMER) 내 성인 사이즈가 아닌 행 제거
- 이상치 제거 - IQR * 3  
  <img width="600" alt="ratio graph" src="https://github.com/parkmy0420/ML_project/assets/87077176/6ad4d13d-73c1-4630-93f4-5c28a1cd15c6">  
  <img width="600" alt="ratio graph" src="https://github.com/parkmy0420/ML_project/assets/87077176/5cc8f96e-0391-484c-9af8-d7c21a6d11a7">

- 리뷰 데이터 키, 몸무게의 이상치 제거
  - 키 : 150cm 미만 / 200cm 이상
  - 몸무게 : 40kg 미만 / 120kg 초과 데이터 제거  
  <img width="600" alt="ratio graph" src="https://github.com/parkmy0420/ML_project/assets/87077176/6598c22b-9315-45a4-922a-0f2ce43d182b">



### 4. Model
#### 4.1 Classification Model
  <img width="600" alt="classificationModel" src="https://github.com/parkmy0420/ML_project/assets/87077176/6ee2628b-a029-48f4-967f-eb3d5e12b488">
  
- Description
  - Random Forest Model (랜덤 포레스트 모델)  
  → MUSINSA STANDARD의 실측 데이터(총장, 가슴단면, 어깨너비)로 사이즈 분류 시행
  
- Model Selection Process  
  <img width="600" alt="Untitled (2)" src="https://github.com/parkmy0420/ML_project/assets/87077176/99485371-01cc-4a18-8f28-52fb89d2e439">
        
- Hyper Parameter Selection Process         
  <img width="600" alt="Untitled (3)" src="https://github.com/parkmy0420/ML_project/assets/87077176/c6fe100e-95cf-4422-96fd-5a2033c59d63">
        
- Classification Model Evaluation  
  <img width="600" alt="Untitled (4)" src="https://github.com/parkmy0420/ML_project/assets/87077176/528907c1-bc1d-4eb1-a8ea-109460593b3b">
  <img width="600" alt="Untitled (5)" src="https://github.com/parkmy0420/ML_project/assets/87077176/c1d0641f-1734-4807-9edd-71d1e6d8c785">

- Results of the Classification Model (final data set)  
  <img width="600" alt="Untitled (6)" src="https://github.com/parkmy0420/ML_project/assets/87077176/540d75bd-12ca-4ee1-b747-8b84c0737544">
            
#### 4.2 Recommendation Model
  <img width="600" alt="Untitled (7)" src="https://github.com/parkmy0420/ML_project/assets/87077176/cc0513ab-7097-490d-a4ac-07b777c7c2e7">

- Description
  - Cosine Similarity (코사인 유사도)
  →  사용자의 특성(키, 몸무게, 성별)을 통하여 가장 유사한 상위 20개 제품 추천
  →  TF-IDF로 얻어진 태그 벡터의 유사도를 이용해 최종 제품 추천
  - TF-IDF (단어 빈도-역 문서 빈도)
  →  한국어 형태로 된 태그를 벡터 형태로 표현하기 위해 사용

- Result of the Recommendation Model  
  <img width="600" alt="Untitled (8)" src="https://github.com/parkmy0420/ML_project/assets/87077176/4e0ebae5-a535-4ada-a4ae-d63c2ecf09b1">

#### 4.3 Summary (results of the model)
- Classification Model
  - **MUSINSA STANDARD**의 실측 데이터를 기준으로 사이즈 분류 모델은 **RandomForest**로 선정하여 진행함
  - 남성, 여성을 나누어 분류 모델을 진행하였고, **Grid Search**를 통하여 최적의 하이퍼 파라미터를 도출함
  - **남성**은 F1스코어 기준 **3XL, S, 2XL** 순으로 모델 성능이 좋았음
  - **여성**은 모델 성능평가 결과 **XS, S, L** 순 나타났음
- Recommendation Model
  - 제품 정보(키, 몸무게, 성별, 태그 등)를 벡터화시켜 **코사인 유사도**를 이용하여 추천시스템을 진행함 (콘텐츠 기반)
  - 키, 몸무게, 성별, 선호 사이즈를 입력하면 유사도가 가장 높은 제품 N개 추천해주는 시스템을 제작함
  - 남성, 여성 모두 사이즈를 기반한 카테고리 별 제품을 잘 보여주는 것으로 확인됨

### 5. Limitations and Improvements
#### 5.1 Limitations
- 모델 비교 선택 시 모델 간 평가지표의 차이가 없어 과적합이 의심됨으로 객관적 판단이 어려움
- 데이터 개수의 부족으로 인해 극단 값들의 추천 결과가 아쉬움
- 고객 별로 추구하는 스타일이 달라서 사이즈 기반으로만 추천하기에는 정확도가 떨어져 보였음
- 추천 시스템을 객관적으로 평가하기 어려움
    
#### 5.2 Improvements
- 더 많은 리뷰 데이터를 수집하면 더 정확하고 다양한 제품 추천이 가능할 것으로 보임
- 규제 기법(Ridge, Lasso) 등을 활용하여 과적합을 줄이는 시도가 필요

--------------

## ⭐️ Team member Information

|Member|Infomation Link|
|------|----------|
|김보석|<a href="https://github.com/Jaredsasset"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white"/> <a href="https://velog.io/@fnrfn2"><img src="https://img.shields.io/badge/Velog-20C997?style=flat-square&logo=Velog&logoColor=white"/> <a href="mailto:fnffn2354@gmail.com"><img src="https://img.shields.io/badge/Mail-EA4335?style=flat-square&logo=Gmail&logoColor=white"/></a>|
|박미영|<a href="https://github.com/parkmy0420"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white"/> <a href="https://velog.io/@zer0"><img src="https://img.shields.io/badge/Velog-20C997?style=flat-square&logo=Velog&logoColor=white"/> <a href="mailto:parkmy0420@gmail.com"><img src="https://img.shields.io/badge/Mail-EA4335?style=flat-square&logo=Gmail&logoColor=white"/></a>|
|박성호|<a href="https://github.com/Pakkoc"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white"/> <a href="https://velog.io/@pa__kko"><img src="https://img.shields.io/badge/Velog-20C997?style=flat-square&logo=Velog&logoColor=white"/> <a href="mailto:qkrtjdgh751014@gmail.com"><img src="https://img.shields.io/badge/Mail-EA4335?style=flat-square&logo=Gmail&logoColor=white"/></a>|
|이성희|<a href="https://github.com/zoe-0314"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white"/> <a href="https://velog.io/@tjdgml1735"><img src="https://img.shields.io/badge/Velog-20C997?style=flat-square&logo=Velog&logoColor=white"/> <a href="mailto:tjdgml1735@naver.com"><img src="https://img.shields.io/badge/Mail-EA4335?style=flat-square&logo=Gmail&logoColor=white"/></a>|
|정설령|<a href="https://github.com/SeolRyung"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white"/> <a href="https://velog.io/@seolryung"><img src="https://img.shields.io/badge/Velog-20C997?style=flat-square&logo=Velog&logoColor=white"/> <a href="mailto:tjffud97@gmail.com"><img src="https://img.shields.io/badge/Mail-EA4335?style=flat-square&logo=Gmail&logoColor=white"/></a>|
|최은욱|<a href="https://github.com/Anti-KAOS"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white"/></a>|

