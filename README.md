# Section2-project

> 어몽어스 초심자에게 알려줄만한 내용에 무엇이 있을까
  https://www.kaggle.com/datasets/ruchi798/among-us-dataset

## 과제 진행시 주의사항(과제로서 가이드라인)


## 진행 계획
### 날짜별 계획
- 1일차 : 세부 주제 선정, 데이터 전처리 및 EDA
- 2일차 : 머신러닝 모델 작성 및 하이퍼 파라미터 튜닝
- 3일차 : 해석 및 결론 도출
- 4일차 : ppt 자료 작성 후 발표영상 촬영
### 내용 계획
- 코드 작성
  - 데이터셋 분할 후에 scaling 등의 전처리를 진행할 것(정보 누수 우려)
  - 다양한 모델을 활용해보고 최종 결정한 모델에 대해서 왜 그 모델을 썼는지 설명
  - 모든 작업 완료했는지 여부를 확인하는 특성은 drop하기(승패와 직접적 관련)
  - scale_pos_weight는 꼭 튜닝하기 -> 점수차이 많이 남
  - 기본 모델 설정
- 발표자료 제작
  - 내가 이 주제를 왜 선택했는지, 비즈니스적 가치에 대한 설명 -> 내가 한 프로젝트를 하면 이런 효과가 있을 것이다~
    - 어몽어스 초심자에게 어느 부분에 집중하는 것이 좋은지
  - 내가 하기로 한 게임에 대한 간략한 설명
  - 가설 설정
    1. 게임 시간이 길어질수록 패배할 확률이 높을 것이다.
    2. 게임 승패에 영향을 미치는 요인

## 1일차 진행 내용
- 특성 선택
- 결측값 및 중복값 처리
- 전처리 진행

## 2일차 진행 내용 
- 시각화 참고자료 : https://wikidocs.net/book/5011
- 다중 막대그래프 참고자료 : https://jimmy-ai.tistory.com/40


## 3일차 진행 내용
- 분류 모델은 Tree based model, RandomForestClassifier, XGBoost 를 사용해보고 가장 점수가 높은 모델을 채택(max_depth 파라미터만 조절)
  - DecisionTreeClassifier
    - SimpleImputer로 결측치를 채워줄 필요가 있음
    - 최고 점수(훈련 : 65 / 검증 : 60)
  - RandomForestClassifier
    - SimpleImputer로 결측치를 채워줄 필요가 있음
    - 최고 점수(훈련 : 64 / 검증 : 60)
  - XGBoost
    - SimpleImputer로 결측치를 채워주지 않을 경우
      - 최고 점수(훈련 : 76 / 검증 : 61)
    - SimpleImputer로 결측치를 채워줄 경우
      - 최고 점수(훈련 : 75 / 검증 : 62)
- 'max_depth' 파라미터만 조절하긴 했지만 Classifier 종류의 모델이 XGBoost 모델보다 과적합이 적게 발생
- 결측치가 존재하는 특성은 '주어진 업무 완료까지 걸린 시간'에 해당하는 특성 뿐인데, 해당 특성에서 결측치는 의미가 있다고 판단
  **→ Imputer로 결측치를 채우지 않기로 결정 → XGBoost를 사용하되, SimpleImputer 미사용**
- 하이퍼 파라미터 튜닝은 Grid Search, Bayesian Search 중에서 선택


## 4일차 진행 내용


---

## 회고


## 피드백

---
깃헙 작성요령
: https://lsh424.tistory.com/37
