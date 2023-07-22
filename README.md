# 어몽어스 크루원 플레이 추천
## 1. 프로젝트 개요
  ### 1. 어몽어스 소개
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/c2452be7-4ee2-46b3-a537-72f660f56cdb)
  ### 2. 문제 정의
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/674ce296-d2a1-418e-b513-5531ba91e568) <br>
  step 1. 최근 유튜브로 ‘빅헤드’ 유튜버의 영상을 많이 보는데, 그중에서 어몽어스 플레이 영상을 재밌게 시청 <br>
  step 2. 어몽어스는 2020년 다양한 스트리머들이 플레이 하면서 대유행, 그 후 2년이 지났기 때문에 초심자에게 진입 장벽이 높아졌다고 생각 <br>
  step 3. 선정 확률이 적은 임포스터 대신 선정 확률이 높은 크루원을 주제로 선정 <br>
  step 4. 머신러닝을 활용하여 크루원의 2가지 승리 조건 중 어느 조건이 승리하기 쉬운지 확인 후 추천하기로 결정 <br>
  ### 3. 가설 설정
  1. 게임 시간이 길수록 크루원에게 유리할 것이다.
  2. 주어진 미션을 모두 끝냈을 경우가 끝내지 못했을 경우보다 승리 수가 더 많을 것이다.
  3. 게임 승패에 큰 영향을 끼치는 요인은 ‘임포스터에게 살해당했는지 여부’일 것이다.

## 2. 프로젝트 진행 과정
  |구분|기간|활동|비고|
  |:---:|:---:|---|---|
  |사전 기획|9/27(화)|- 프로젝트 기획 및 데이터 확인||
  |데이터 전처리 및 <br> 시각화|9/28(수)|데이터 전처리 후, 시각화||
  |머신러닝 및 성능 평가|9/28(수) ~ 9/29(목)|- baseline 모델 구현 <br> - 머신러닝 진행(XGBoost 모델) <br> - 성능 평가|하이퍼 파라미터 튜닝 진행|
  |모델 해석 및 정리|9/30(금)|모델 해석 및 정리||
  |총 개발기간|9/27(화) ~ 9/30(금)(총 4일)|||
  
## 3. 데이터셋 설명
  - 데이터 셋 : 2020년 11월 ~ 2021년 1월까지 게임 진행 데이터(승패 여부, 업무 완료 개수, 게임 시간 등) <br>
    → 총 29개로 나누어진 파일을 1개의 파일로 통합하여 진행 <br>
  - 데이터셋 주소 : https://www.kaggle.com/datasets/ruchi798/among-us-dataset
  - 특성 설명 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/3a6d6fc6-00f3-4801-a6a9-2296d1621d5b) <br>
    : 빨간 박스에 있는 특성만 사용

## 4. 프로젝트 진행 내용
  ### 1. 전처리
  - 사용하지 않는 데이터 및 특성 제거
    1. 특성 설명에서 하위 4개의 특성을 제거 <br>
    2. 소속 팀이 크루원인 데이터만 남기고 'Team' 특성 제거 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/7e5586df-6a69-494e-97f4-301155f95ed0)

  - 중복값 제거
    1. 중복값 제거 후 확인 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/0f49c68f-25ce-440f-b9da-887f0b3ced45)

  - 시간 관련 특성 단위 통일
    1. 분과 초가 나눠서 기록된 데이터와 분을 초로 환산하여 기록된 데이터가 혼재되어 있어, 분을 초로 환산하여 통일 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/5899fe18-b8b0-42d1-8561-391877863d75)

  ### 2. 시각화
  - 전체 데이터의 승/패 비율 <br>
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/ed2cd776-e1f8-4a0e-880c-f5429904e84d) <br>
  : 승/패 비율이 비슷하기 때문에 프로젝트를 신뢰할 수 있음 <br>

  - 게임 승/패에 따른 게임 시간 비교(가설1 검증) <br>
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/ca8906c7-9c73-4436-936d-3e9551ba757a) <br>
  : 승리한 게임이 패배한 게임에 비해 비교적으로 게임 시간이 길음 <br>
    따라서, 가설 1. 게임 시간이 길수록 크루원에게 유리할 것이다. → 진실 <br>

  - 주어진 업무 완료 여부 별 승/패 수(가설2 검증) <br>
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/65d10099-d2cd-4d9a-b548-fde7b024aa9f) <br>
  : 주어진 미션을 완료하지 못했을 때, 승리와 패배의 수가 모두 비교적 많음 <br>
    따라서, 가설 2. 주어진 미션을 모두 끝냈을 경우가 끝내지 못했을 경우보다 승리 수가 더 많을 것이다. → 거짓 <br>
    
  ### 3. 머신러닝
  - 훈련/검증/테스트 데이터 분리 <br>
  : 데이터를 학습 데이터와 테스트 데이터로 4:1의 비율로 분리 후, 학습 데이터를 다시 학습 데이터와 검증 데이터로 4:1의 비율로 분리 <br>
  → 하이퍼 파라미터 튜닝을 위해 검증 데이터가 필요 <br>
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/1c6c07f5-2256-4649-972e-e608e4ea8f0e) <br>
  
  - baseline 모델 <br>
  : 최빈값으로 타겟값 예측 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/bb149745-47c8-46e8-aa87-b82cc0a1c214) <br>
    
  - 머신러닝(XGBoost 모델)
    ① 특성 인코딩 <br>
    : 학습 진행을 위해 특성 인코딩 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/17e6dbbf-9771-47fb-ad35-744fd4f994d0) <br>
    
    ② 모델 생성 <br>
    : XGBoost 모델로 머신러닝 모델 생성 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/16f3d36a-a694-401e-8ee4-5a7e36514e9e) <br>
    
    ③ 하이퍼 파라미터 탐색 <br>
    : max_depth, min_child_weight, sub_sample 3가지 파라미터에 대하여 모델 성능이 가장 높은 값을 탐색 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/c370a5be-e097-42de-a078-c1a90ab2f2a3) <br>

    ④ 하이퍼 파라미터 튜닝 후 학습 진행 <br>
    : ③에서 찾은 최적의 파라미터로 튜닝 후 학습 진행 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/12fffec1-169f-4f58-b690-59138018c524) <br>
    
  ### 5. 성능 평가
  - 학습에서 활용하지 않은 테스트 데이터로 예측을 진행하여 일반화 성능을 확인
  - Confusion Matrix를 통해 예측 결과를 직관적으로 확인 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/07a9f004-e736-4212-af1c-b8178da2f06e) <br>
    - 실제로 승리한 샘플 중에서 모델이 승리했다고 예측한 샘플의 개수 : 141개
    - 실제로 승리한 샘플 중에서 모델이 패배했다고 예측한 샘플의 개수 : 45개
    - 실제로 패배한 샘플 중에서 모델이 승리했다고 예측한 샘플의 개수 : 76개
    - 실제로 패배한 샘플 중에서 모델이 패배했다고 예측한 샘플의 개수 : 70개
      
  - Classification Report를 통해 각 class에 대한 성능 평가 결과를 확인
    - precision : '예측값'을 기준으로 '정답인 예측값'의 비율
    - recall : '실제 값'을 기준으로 '정답인 예측값'의 비율
    - f1-score : precision과 recall의 가중 조화평균 
    - support : 각 라벨의 실제 샘플 개수
    - accuracy : 전체 샘플 중 맞게 예측한 샘플 수의 비율 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/f2ecd42e-2a03-4a89-9f65-e7521310adfa) <br>
    ex) precision의 Loss인 0.61은 '패배를 예측한 샘플 중에서 실제 패배인 샘플의 비율'로 115개(70개+45개) 중에서 70개의 샘플이 차지하는 비율
    
  ### 6. 모델 해석
  - Feature Importance(가설3 검증)
    : 모델이 중요하다고 생각한 특성의 순위 <br>
    ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/49b51a8a-a988-4a0f-bc9a-f3570482369c) <br>
    : ‘Murdered’, 'Ejected', 'Sabotages Fixed' 특성 순으로 모델의 성능에 가장 큰 영향을 미침 <br>
    따라서, 가설 3. 게임 승패에 큰 영향을 끼치는 요인은 ‘임포스터에게 살해당했는지 여부’일 것이다. → 진실 <br>
    
## 5. 프로젝트 결론
  - 가설 검증 결과
    - 게임 시간이 길수록 크루원에게 유리
    - 미션을 완료하지 않았을 경우의 승리 횟수가 미션을 완료할 경우보다 많음
    - 예측 모델에서 중요한 특성 : Murdered(임포스터에게 살해당했는지 여부), Ejected(투표로 퇴출되었는지 여부), Sabotages Fixed(사보타지 고친 횟수)
      
  - 결론 <br>
    : 크루원의 2가지 승리 조건인 '주어진 미션을 모두 완료'와 '모든 임포스터를 투표로 퇴출' 중에서 미션을 완료하기보다 임포스터에게 살해당하지 않게 주의하면서 '투표로 모든 임포스터를 퇴출' 을 목표로 하는 플레이 추천
## 6. 한계점 및 향후 계획
  - 한계점
    - 임포스터 승리 조건이 2가지이나 영상 시청 결과 임포스터가 사보타지로 아기기 어려워 임포스터의 플레이를 추천하기 어려움
    - 게임 업데이트에 따라 2년 전과 현재의 진행 방식, 특수 능력 존재 여부 등이 다를 수 있음
  - 향후 계획
    - 어몽어스 게임을 직접 플레이해 보고 2가지 조건 중에서 실제로 어느 조건을 충족시키는 승리가 많을지 확인
    - 해당 프로젝트에서는 XGBoost 모델을 활용하였지만 다른 모델로 학습을 진행하고 서로 비교
