## 🙋🏻‍♀️ **OMO 전략을 위한 계열사 확장 예측 모델 및 상품 추천**

> OMO: Oline Merge with Offline
> 
<br>

## 🙋🏻‍♂️ **등장 배경**

> 기존 O2O 및 옴니채널은 온라인과 오프라인 간 경계 없이 이루어지는 고객의 복잡한 구매 행동 패턴을 이해하기 위한 ‘고객 행동 데이터’ 확보가 어려웠으며, 오프라인의 매장을 방문하는 고객 행동 데이터보다 온라인에 더 높은 비중을 두고 있어 통합적인 관리가 어려운 상황입니다.  
경쟁이 치열해짐에 따라 현재 커머스 시장은 실시간으로 고객의 다양한 니즈를 반영하고 더 불규칙해진 구매 패턴을 빨리 파악하고, 언제 어디서든 고객과의 상호작용을 통해 자사 서비스(상품, 브랜드)에 대한 새로운 고객 경험을 제공하는 것이 매우 중요해졌습니다. 온·오프라인 통합 데이터는 이런 시장 변화에 대응하기 위한 필수 요소이며, OMO 서비스가 O2O를 보완한 서비스 전략으로 주목받게 되었습니다.    
저희는 고객의 복잡한 구매 여정을 종합적으로 분석하고 그에 맞는 최상의 고객 경험을 제공하고자, OMO 전략을 위한 고객 유형별 확장 가능한 계열사 예측 및 상품 추천을 통해 계열사 확장을 유도하고자 합니다.
> 
<br>

## 😎 분석 목표

> (1) **클러스터링** - 고객 구매 데이터를 통한 고객 유형 분석  
(2) **예측 모델** - 확장 가능한 계열사 예측  
(3) **추천 시스템** - 예측 결과를 바탕으로 상품을 추천하여 계열사 확장 유도
> 
<br>

## 👩🏻‍💻 모델 구조
<img width="100%" src="https://user-images.githubusercontent.com/91619301/197831652-9842ea78-7626-4bfb-b4da-c24dcb4be522.png"/>
<br>

## 🙆🏻 클러스터링

> ☝ K-Means  
✌ HDBSCAN
> 
- 고객 구매 데이터를 기반으로 **고객 유형 세분화** 및 프로파일링
- 클러스터를 통해 **고객 분석** 및 새로운 데이터에 대해 유사 고객을 파악하여 **상품 추천** 시스템 고안
<br>

**[변수별 클러스터 분포 - 이용한 계열사 수, 고객생애가치]**
- x축: 이용한 계열사 수
- y축: 고객생애가치
- 이용한 계열사 수가 많을수록 고객생애가치가 증가 ➡ 계열사 확장의 필요성 재확인
![Untitled](https://user-images.githubusercontent.com/91619301/197833729-1e29f44c-16e3-4d5e-8ead-b7edccf140d2.png)
<br>
<br>

**[변수별 클러스터 분포 - 구매금액, 고객생애가치, 이용 계열사 수, 온라인 친화도, 성별]**
![image](https://user-images.githubusercontent.com/91619301/197835079-ff4f0d98-ad47-4929-a03d-3ebb12eb449c.png)
<br>
<br>

**[프로파일링(페르소나)]**
- 12개 클러스터의 관찰 변수 특징에 따라 **페르소나 확정** 후, 소비 특성에 따라 **4개 유형으로 분류**(충성/단골/입문/이탈위험)
![image](https://user-images.githubusercontent.com/91619301/197835429-2e7c08c8-5f55-43a0-967b-f81afb560d85.png)
![image](https://user-images.githubusercontent.com/91619301/197835499-760deb47-96eb-4bb3-89c1-c1d27ed750c9.png)
<br>





## 🙆🏻‍♂️ 예측 모델

> ☝ Xgboost
✌ Catboost
> 
- EDA와 클러스터링 결과에 따라 **고객이 이용하는 계열사 수**가 **유의미한 변수**임을 확인
- 고객의 첫 구매 데이터를 통해 **추후에 이용 가능성이 높은 계열사 예측**
- **다중 분류 예측 모델** 사용

➡️ 계열사 확장을 통해 통합된 고객 경험 제공 가능

### (1) 학습 데이터

- Custom encoding
    - 이용한 계열사의 고유값에 해당하는 컬럼에 계열사 이용 횟수를 표시하고, 나머지 컬럼에는 0을 표시
    - one-hot enocidng과 달리, 인코딩 값으로 1 대신 계열사 이용 횟수 사용
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fcebb39-d745-4884-8d67-ea20b12e41df/Untitled.png)
    
- Label encoding
    - 계열사를 제외한 범주형 변수에 적용

**[최종 학습 데이터]**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a9b5212e-269e-476e-adec-2adec4d2b5a6/Untitled.png)

- train, test 데이터 분리
    - 전체 중 5%(약 1000개)를 테스트 데이터로 분리

### (2) 모델 학습 및 성능 개선

- 하이퍼파라미터 튜닝
    - **Wandb(Weight & Biases)** 툴 이용
        - 모델 실험 결과를 효과적으로 추적 가능
        - 하이퍼파라미터 최적화 가능
        
        [하이퍼파라미터 튜닝 결과]
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/64e26abc-ab17-43f7-9c2f-bcccdb73c30e/Untitled.png)
        
- 데이터 증강
    - 확장 계열사 추가
    
    [계열사가 확장된 모든 경우 추가]
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/962dee89-854b-40ce-ae98-0fcf8d3f4051/Untitled.png)
    
- 불균형 데이터 처리
    - 확장이 많이 일어난 A01, A02를 제외한 예측 정확도가 낮음.
    - SMOTE 방법 실험, sample_weights 하이퍼파라미터 조정

### (3) 실험 결과

- 14개의 라벨을 가진 약 1000개의 텍스트 데이터의 420개 정도의 확장 계열사 예측
- 실험을 통해 베이스라인 모델 정확도 12%p 상승(0.3 ➡️0.42)
- 데이터 특성에 맞게 Custom Encoding 방식의 유효성 확인

<aside>
☝ XGBoost

- 하이퍼파라미터를 조정하는 과정에서 약 3%p 정도의 큰 상승
- 학습시마다 데이터와 독립변수의 양을 조절하는 subsample, colsample_bytree 파라미터를 조절하여 모델의 일반화 성능 향상
</aside>

<aside>
✌️ CatBoost

- K-fold Valdiation을 사용하여 일반화 성능 향상
</aside>

## 🙆‍♀️ 추천 시스템

> LightFM
> 

### (**1) 추천 시스템 문제**

**Cold start**

- 초기 고객이나 상품에 대한 정보가 부족하여 적절한 상품을 추천하지 못하는 문제
- 아이템이 많은 경우, 새로운 상품이 자주 등록되는 경우, 고객의 다수가 신규 고객인 경우 발생
- 첫 번째 계열사만을 이용한 고객의 적은 데이터를 기반으로 상품을 추천해야 하는 상황과 유사

### (**2) 추천 시스템 모델**

**LightFM**

- Content-Based와 Collaborative Filtering의 장점을 결합한 추천 시스템 모델
- 학습 과정에서 User-Item 특성과 Collaborative 데이터를 모두 사용
- LightFM학습을 위해 생성한 특징벡터는 변수에 대한 중요한 정보 포함

### (3) **추천 시스템 구현**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f581ea4b-3a73-4735-8fe9-12f64a911b8b/Untitled.png)

### (**4) 추천 시스템 결과 예시**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be7908db-7519-4d37-934a-b74838c7aa10/Untitled.png)

## 💁‍♂️ 고객 클러스터별 마케팅 전략

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/50f7fec4-8997-4117-bf04-912dadf3bae9/Untitled.png)
