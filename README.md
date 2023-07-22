# 어몽어스 크루원 초심자 가이드
## 1. 프로젝트 개요
  ### 1. 어몽어스 소개
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/c2452be7-4ee2-46b3-a537-72f660f56cdb)
  ### 2. 문제 정의
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/aba04f65-5cc9-4273-8b5b-f56414b1410c)
  ### 3. 가설 설정
  1. 게임 시간이 길수록 크루원에게 유리할 것이다.
  2. 주어진 미션을 모두 끝냈을 경우가 모두 끝내지 못했을 경우보다 승리 수가 더 많을 것이다.
  3. 게임 승패에 큰 영향을 끼치는 요인은 ‘임포스터에게 살해당했는지 여부’일 것이다.

## 2. 프로젝트 진행 과정
  |구분|기간|활동|비고|
  |:---:|:---:|---|---|
  |사전 기획|9/27(화)|- 프로젝트 기획 및 데이터 확인||
  |데이터 전처리 및 <br> 시각화|9/28(수)|데이터 전처리 후, 시각화||
  |모델링 및 성능 평가|9/28(수) ~ 9/29(목)|- baseline 모델 구현 <br> - 모델 구현(XGBoost모델) <br> - 성능 평가|하이퍼 파라미터 튜닝 진행|
  |모델 해석 및 정리|9/30(금)|모델 해석 및 정리|프로젝트 내용을 ppt 파일로 정리|
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

  - 게임 승패에 따른 게임 시간 비교(가설1 검증) <br>
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/ca8906c7-9c73-4436-936d-3e9551ba757a) <br>
  : 승리한 게임의 시간이 패배한 게임에 비해 길음 <br>
  ![image](https://github.com/donghwi2022/ds-section2-project/assets/73475048/5dd24a98-d6d5-45ae-921a-5bcf193fa556) <br>

    - 사용 디바이스 종류 분석
    - 컬럼의 연도별 변화 분석(함수화하여 다양한 컬럼에 대해 분석할 수 있도록 작성)
    - 컬럼의 계절별 분석(함수화하여 다양한 컬럼에 대해 분석할 수 있도록 작성)
  ### 3. 추가 전처리
    - 불필요한 컬럼 drop
    - Category 컬럼 통합
    - 결측치 처리
    - 구매에 실패한 데이터 삭제
    - Parquet으로 파일 타입 변경(데이터 타입 변경시, 변경된 타입 저장)
  ### 4. 모델링
    - baseline 모델
      : 가장 빈도가 높은 상품 20개를 모든 고객에게 추천
    - 추천 모델
      - 상품의 정보를 바탕으로 CB모델을 통해 추천
      - OOM 문제를 해결하기 위해 코사인 유사도가 아닌 annoy 라이브러리를 사용
  ### 5. 성능평가
    - 20개의 상품을 추천
    - precision@k와 recall@k를 통해 성능평가
  ### 6. 모듈화
    1. 앞의 추천 모델을 python 파일로 작성 및 저장
    2. Colab에서 해당 python 파일을 불러와 추천 및 
## 5. 프로젝트 결과
  - 기준 모델의 성능(20개 추천 기준)
    - precision@k : 0.00013472549680026923
    - recall@k : 0.00036301053382020325
  - 추천 모델의 성능(20개 추천 기준)
    - precision@k : 0.0001613899180419891
    - recall@k : 0.0004927032935038315
  - 결과 요약
    : 2가지 성능평가 모두 기준모델보다 추천 모델이 점수가 높은 것을 확인할 수 있음
## 6. 한계점 및 향후 계획
  - 한계점
    - 시계열 정보를 활용하기 위해 함수를 작성해 보았으나 OOM 문제가 발생하여 시계열 정보를 활용하지 못함
    - 다양한 모델을 비교하고 싶었으나, 실력 부족으로 1가지 모델밖에 구현하지 못함
  - 향후 계획
    - 구현해보고 싶은 모델(링크) : https://jalynne-kim.medium.com/%EC%B6%94%EC%B2%9C%EB%AA%A8%EB%8D%B8-%EC%9D%B4%EC%BB%A4%EB%A8%B8%EC%8A%A4-%EC%B6%94%EC%B2%9C%EB%AA%A8%EB%8D%B8%EB%A7%81-%EB%94%A5%EB%9F%AC%EB%8B%9D%EB%AA%A8%EB%8D%B8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%ED%9A%8C%EA%B3%A0-d5017cb1335f
