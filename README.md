# Section2-project

> 어몽어스 초심자에게 알려줄만한 내용에 무엇이 있을까<br>
  https://www.kaggle.com/datasets/ruchi798/among-us-dataset

## 사용 내역 요약
- 사용한 모델, 특성 등에 대해 이유와 함께 서술(추후 진행)


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
- 결측치가 존재하는 특성은 '주어진 업무 완료까지 걸린 시간'에 해당하는 특성 뿐인데, 해당 특성에서 결측치는 의미가 있다고 판단<br>
  **→ Imputer로 결측치를 채우지 않기로 결정 → XGBoost를 사용하되, SimpleImputer 미사용**
- 하이퍼 파라미터 튜닝은 Grid Search로 진행
  - 튜닝 파라미터 : max_depth, min_child_weight, sub_sample
  - 튜닝하지 않은 파라미터
    - n_estimators : 확인결과 영향이 적어서 고정
    - scale_pos_weight : 내가 가진 데이터셋의 타겟 불균형이 심하지 않아 미지정
    - **gamma : 최적값은 0이나, 모델의 과적합이 심해 2로 고정**
- 평가지표 : 타겟값이 비교적 불균형이 아니기 때문에 accuracy를 사용
- 모델 해석
  - 특성 중요도
    - 시간과 관련된 특성은 high cardinality특성 → Feature Importance 사용 불가
    - 서로 연관이 있는 특성이 존재(ex. '모든 업무를 완료했는지 여부'특성과 '모든 업무 완료까지 걸린 시간'특성) → Permutation Importance 사용 불가
    - 특성 개수가 비교적 많지 않으므로, Drop-Column Importance 사용
  - ICE Plot → 우리가 보고자 하는 것은 전체적인 데이터를 통한 분석이기 때문에 생략
  - PDP
    - 특성 중요도에서 해당 특성을 drop했을 때, 성능이 감소하는 특성에 대해 진행


## 4일차 진행 내용
- 작성중인 colab 파일 확인 및 수정
  - 오타 수정
  - 내용에 맞지 않은 내용 제거 및 보완
- 결론 도출
- ppt 제작
- 발표 영상 제작
- 코드 파일, ppt, 발표 영상 최종 확인 및 제출

---

## 회고
- 질문
  - XGBClassifier(eval_metric='error', gamma=2, n_estimators=200, n_jobs=-1,
              random_state=42, xgbclassifier__max_depth=2,
              xgbclassifier__min_child_weight=1, xgbclassifier__sub_sample=0.2)
  - model_sample = XGBClassifier(
        eval_metric = "error",  
        n_estimators = 200,
        random_state = 42,
        gamma = 2,
        n_jobs = -1,
        max_depth=2, 
        min_child_weight=1, 
        sub_sample=0.2
    )
    : 위의 2개의 모델에 대해서 xgbclassifier__가 붙는지 여부로 정확도 점수가 다르게 나옴

## 피드백

---
깃헙 작성요령
: https://lsh424.tistory.com/37
