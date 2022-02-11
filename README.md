# Hoseo_AI_Competition
A.I. Classification Competition of HoseoUniv in 2021


Team  ACC 100

## Contents
   
[1. Team Introduce](#Team-Introduce)   
   
[2. Strategy](#Strategy)   
   
[3. Result](#Result)   


## Team Introduce
송민석 __컴퓨터공학부 학부생__

임재성 __컴퓨터공학부 학부생__

김희중 __컴퓨터공학부 학부생__

## Strategy

+ Data Preprocessing
  * 처음 대회 측에서 Data set을 받았을 때는 feature들의 의미를 알 수 없었습니다.
  * 그래서 Data set 정형화를 시도했습니다.
  
  **before**   
  ![그림1](https://user-images.githubusercontent.com/59774709/153637887-9af649f1-7dc8-4193-bdcd-b3e18e0a4302.jpg)
  
  **after**   
  ![그림2](https://user-images.githubusercontent.com/59774709/153637894-b07460e8-9ef1-4477-be36-b23b121fccc3.png)   
  
  엑셀 확장자였던 Data set을 **json**으로 바꾼 다음에,   
  먼저 Feature_Group_C의 **key**, **value** 값으로 feature를 각각 나눠주고,    
  나머지 A, B는 의미를 알 수 없어 전부 독립적인 feature로 나눠주었습니다.
  
  **Exel**   
  ![그림3](https://user-images.githubusercontent.com/59774709/153638340-927077a6-6977-40a8-883a-e218045e4f9d.png)
  
  
  
  + Visualizing   
  **Feature 시각화 - CNN**   
  <img width="403" alt="그림4" src="https://user-images.githubusercontent.com/59774709/153639781-b98a4f8f-692a-40ad-ae44-ea54a20346fb.png">   
  
  먼저 CNN을 사용해 각 행을 2차원 이미지 배열로 만들어주고,   
  모든 feature를 min-max 정형화로 신경망 연산을 돌려봤지만   
  낮은 accuracy가 나와서 다른 방법을 시도했습니다.   
  
  + Scaling   
  ![그림5](https://user-images.githubusercontent.com/59774709/153641075-9353318e-093f-42e5-b154-5bd79fe38f47.png)   
  다른 방법으로 Standard Scaling을 통해 Data Scaling 진행해봤고   
  
  + Remove Outliers   
  ![그림6](https://user-images.githubusercontent.com/59774709/153641273-023ecc9b-071c-4a90-9530-8e9e84ed3db7.png)   
  IQR을 이용한  이상치 제거를 통해 모델의 학습능력 향상시켰습니다.   
  
  + PCA(Principal Comonent Analysis)   
  ![그림7](https://user-images.githubusercontent.com/59774709/153641887-34a39a99-21c5-44a4-a0a8-b952f83e7f0a.png)   
  이외에 accuracy를 더 끌어올리기 위해 PCA 차원 축소 알고리즘을 통해 모델 복잡도를 줄여보았습니다.   
  
+ Ensemble learning
  + **Ensemble Learning 사용**   
  시도한 방법들이 결과가 좋지 않아, kaggle 대회에 주로 사용되는 Ensemble Learning을 도입해 봤습니다.   
     
     
     
  + Boosting      
  ![그림8](https://user-images.githubusercontent.com/59774709/153642725-2dc7b6dd-bb0a-4943-9cc8-573c2a84b7c2.png)   
    + Boosting이란 가중치를 활용하여 분류기를 만드는 방법을 말하는데,   
    
    + 여러 개의 독립적인 모델들이 각각 값을 예측 후 그 결과를 통해 최종 예측값 설정하고,   
    
    + 잘못 분류된 데이터에 집중하여 새로운 분류 규칙을 만드는 과정을 반복합니다.   
     
  + Voting   
  ![그림9](https://user-images.githubusercontent.com/59774709/153643144-8b233771-84db-4e47-83a2-212ab7072eb4.png)   
    + 각 Class별 모델들이 예측한 확률의 평균값을 계산하여 가장 높은 Class 선택합니다.   
    
  + Stacking   
  <img width="550" alt="그림10" src="https://user-images.githubusercontent.com/59774709/153643333-01233638-4dd3-4c0a-9f27-1384a8ace07a.png">   
  
    + stacking은 서로 다른 모델들을 조합해서 최고의 성능을 내는 모델을 생성하는데, 매우 많은 연산량을 요구합니다.   
    
  + Model Select   
  ![그림11](https://user-images.githubusercontent.com/59774709/153643740-610480a2-3f8b-4d8b-aca6-8f5a11f5955b.png)   
  
    + 여러 Model들의 Ensembel Learning 진행했고   
    
    + CNN 포함 시 Accuracy가 낮아져 제외했습니다.   
    
    
  + Model Tuning   
  
    + Optuna를 이용해 모델의 Hyperparameter 수치 조정 및 교차 검증을 통한 Overfitting을 방지했습니다.   
       
       
    ![그림12](https://user-images.githubusercontent.com/59774709/153644145-f229995b-4dbc-4a54-aee5-73364def5635.png)   
    

## Result
- **Compare Using Model Accuracy**   

1. Boosting Model(XGBoost / LightGBM / CatBoost)   

2. RandomForest   

3. CNN   
    
    #
- **Compare Ensemble**   

1. Voting(+Boosting)   

2. Stacking(+Boosting)   

3. RandomForest(Bagging)   
    
    #
- **Compare Data Preprocessing**   

1. Use PCA > Except PCA   

  * 불분명한 Feature와 상관관계   
