# LOTTE_bigdata_competition

# 깃헙 정리

# 프로젝트 제목

OMO 전략을 위한 계열사 확장 예측모델 및 상품 추천
(OMO ? Online Merge with Offline!)

# OMO 전략을 위한 계열사 확장 예측모델 및 상품 추천

기존 O2O, 옴니채널은 고객의 구매행동 패턴이 디지털화되는 온라인에 집중되면서 온오프라인 간 경계없이 이루어지는 통합 고객 행동 데이터 확보가 어려워지는 한계를 갖고 있습니다.

실시간 고객 니즈 반영, 불규칙한 구매패턴 파악, 고객과의 상호작용 등 새로운 고객 경험 제공의 중요성이 커지는 요즘 국내 대형 유통기업의 온오프라인 통합하는 움직임에서 볼 수 있듯이 커머스 트렌드는 OMO로 변해가고 있습니다.

# 분석 목표

1. 고객 구매 데이터를 통한 고객 유형 분석(클러스터링)
2. 확장 가능한 게열사 예측(✅예측모델)
3. 예측 결과를 바탕으로 상품을 추천하여 계열사 확장 유도(✅추천시스템)

# 모델 구조
<img width="90%" src=https://user-images.githubusercontent.com/91619301/197762982-89194849-d914-459e-b1ae-1809e0218126.png>

# 클러스터링
- 고객 구매 데이터를 바탕으로 고객 유형을 분석하고 프로파일링
- 나아가 유저의 함축적인 정보를 담은 클러스터 기반의 추천시스템 고안
모델

1. K-Means
2. HDBSCAN

변수별 클러스터 분포
<img width="70%" src=https://user-images.githubusercontent.com/91619301/197761631-98a95247-d838-4c41-9081-99b9724d95e8.png>
클러스터별 시각화 자료
<img width="90%" src=https://user-images.githubusercontent.com/91619301/197763543-48a5c7ac-76b5-479b-bad8-1640a7cb2a50.png>
프로파일링(페르소나)
<img width="90%" src=https://user-images.githubusercontent.com/91619301/197763245-12512593-0cbf-4134-88cc-6a98c6cdbbe5.png>

# 예측 모델

개요

1. 1.
2. 학습 데이터 생성 방식

모델

1. Xgboost 
2. Catboost

# 추천시스템

모델

1. Ligh

# 결과

나경훈

박희진

하정현
