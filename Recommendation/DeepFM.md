## CTR (Click-through rate) 예측
  * 클릭할 확률을 의미하며, 유저들이 어떤 상품 / 광고를 많이 클릭할지 예측할 수 있음
  * 1~5점 척도의 리뷰 평점 예측 태스크와 달리 CTR 예측 태스크는 '추천했을 때 클릭할지'를 기준으로 학습
  * 많은 추천 시스템의 목적 : Maximize the number of clicks
      * 온라인 광고의 경우?
          * 광고 매출 극대화가 목적
          * CTR (클릭 전환율) * Bid (광고 단가) 극대화
  * CTR 예측을 하기 위해서는 유저들의 Implicit Feature를 학습해야 함
      * low-order interaction
          * "식사시간에 음식 배달 앱을 많이 다운로드 받는다." (앱 카테고리 + 시간대) -> order-2 interaction -> low-order
          * "10대 남학생들이 RPG 게임과 shooting game을 좋아한다" (앱 카테고리 + 성별 + 연령대) -> order-3 interaction -> low-order
      * high-order interaction
          * 다양하고 복잡한 Feature 들의 관계는 사람의 도메인 지식만으로 연결하기 어려움
          * "기저귀 코너 옆에 맥주를 두면 매출이 올라간다."
          * "찜기를 구매하면 숯도 같이 구매한다."
          * 모델에 기반하여 자동으로 관계를 포착하도록 학습


## DeepFM 이전 CTR 예측 모델
  * FTRL - Ad Click Prediction : a View from the Trenches
      * 간단한 선형모델에서 좋은 성능을 보임
      * high-order interaction을 학습하기 어려움
  * FM - Factorization Machines
      * Latent Vector의 내적을 활용해서 Pairwise Feature Interaction 모델링 가능
      * 이론적 가정과 달리, 3-order 이상부터는 복잡도가 너무 높아져서 2-order 까지만 활용
  * DNN 계열
      * 복잡한 feature interaction을 포착하기에 용이
      * 단점
        * CNN 계열 : 이웃 피쳐에 편향된다는 특징이 있음
        * RNN 계열 : 순차적인 의존성이 있는 데이터에 더 적합 (문장, 영상 등)
  * FNN - Factorization-machine supported Neural Network
      * <img width="412" alt="스크린샷 2023-11-06 오후 5 33 31" src="https://github.com/sally-yeom/TIL/assets/61625764/a450ac2e-c759-49d9-91e8-1c199ce3b83e">
      * FM으로 사전학습을 한 후 DNN에 입력
      * 사전 학습된 FM 모델에 의존적인 한계
      * DNN 기반이므로 high-order interaction만 잡을 수 있음
  * PNN - Product-based Neural Network
      * <img width="391" alt="스크린샷 2023-11-06 오후 5 34 13" src="https://github.com/sally-yeom/TIL/assets/61625764/1abb0dc4-6165-4fc2-a6c0-732464079638">
      * Embedding Layer - Product Layer - FC Layer
      * low-order interaction을 거의 포착하지 못함
      * Inner Product(내적) 연산에서 나온 결과값이 첫번째 Hidden Layer의 모든 노드와 연결되어있어 계산량 큼
      * Outer Product(외적) 을 근사해서 사용하는데 많은 정보 손실 발생
  * Wide & Deep
      * <img width="667" alt="스크린샷 2023-11-06 오후 5 38 19" src="https://github.com/sally-yeom/TIL/assets/61625764/ddec043c-b61b-411c-a3fd-6f4ffb8ef5a5">
      * Hybrid Network Structure (linear wide model & deep model)
      * low, high-order interaction을 모두 포착하기에 좋은 구조
      * 다만, wide model은 여전히 feature engineering에 의존적인 결과를 냄
  * 기존 모델 특징 요약
      * low-order, high-order 중 하나에 치우쳐 있거나
      * feature engineering에 의존적


## DeepFM : A Factorization-Machine based Neural Network for CTR Prediction
  * Factorization Machines를 신경망으로 확장한 모델
  * 기존의 CTR 예측 모델의 한계를 보완
      * 특별한 feature engineering 없이 end-to-end 방식으로 low, high-order 모두에 대한 feature interaction을 학습할 수 있음
      * 사전학습 불필요
      * 해당 논문에서 GPU 학습은 지원되지 않는 상태라고 함
  * 특징
      * FM 아키텍쳐와 DNN 아키텍쳐를 통합한 Neural Network
          * low-order feature interaction은 FM 방식으로 학습
          * high-order feature interaction은 DNN 방식으로 학습
      * Wide part, Deep part 모두 같은 임베딩 벡터 공유
  * 구조
      * <img width="821" alt="스크린샷 2023-11-06 오후 4 49 44" src="https://github.com/sally-yeom/TIL/assets/61625764/e277c1eb-b8e3-4f4a-b2bb-411a0c773221">
      * 입력 형식
          * <img width="611" alt="스크린샷 2023-11-06 오후 5 28 43" src="https://github.com/sally-yeom/TIL/assets/61625764/a64e2f8b-9ea3-498f-abcc-c63b1940644c">
      * FM Component
          * <img width="728" alt="스크린샷 2023-11-06 오후 5 04 13" src="https://github.com/sally-yeom/TIL/assets/61625764/77d77671-b37e-4382-9f9e-54362fc6226f">
          * order-2 feature interaction 모델링
          * linear interaction & pairwise interaction 고려
          * feature latent vector 내적 진행
          - <img width="809" alt="스크린샷 2023-11-06 오후 4 59 45" src="https://github.com/sally-yeom/TIL/assets/61625764/22415f8a-2ae2-4043-9ede-0279e36499f6">
          - Addition Unit : order-1 feature 중요도 반영
          - Inner Product Unit : order-2 feature 중요도 반영
      * Deep Component
          * <img width="726" alt="스크린샷 2023-11-06 오후 5 05 04" src="https://github.com/sally-yeom/TIL/assets/61625764/61d2f0b0-5060-4a1e-9894-6daf452f0c14">
          * high-order feature interaction 모델링
          * Feed-Forward Neural Network
          * Deep Component를 어떻게 설계하냐에 따라 high-order feature interaction의 학습 성능이 달라질 것
          * Embedding Layer 상세
          * <img width="680" alt="스크린샷 2023-11-06 오후 5 18 43" src="https://github.com/sally-yeom/TIL/assets/61625764/16eec56e-2065-42a6-b0fb-9fc3546e10b4">
          - Sparse input features
             - categorical & continuous features
             - highly sparse, super high-dimensional
          - Dense Embeddings
             - low-dimensional, dense real-value vector
             - input field vector 크기가 필드마다 다르더라도 동일하게 크기 k의 임베딩 e_i로 변환
             - <img width="296" alt="스크린샷 2023-11-06 오후 5 23 32" src="https://github.com/sally-yeom/TIL/assets/61625764/51356217-db4c-40a6-a856-b63ae0567a7d">
             - <img width="375" alt="스크린샷 2023-11-06 오후 5 23 42" src="https://github.com/sally-yeom/TIL/assets/61625764/16e13698-9234-41e2-ab32-a4c6db56a19b">
             - <img width="490" alt="스크린샷 2023-11-06 오후 5 23 56" src="https://github.com/sally-yeom/TIL/assets/61625764/e5579e85-4f11-445d-993d-91fae56fbca6">
      * 최종 결과물은 클릭 여부
          * <img width="403" alt="스크린샷 2023-11-06 오후 4 55 13" src="https://github.com/sally-yeom/TIL/assets/61625764/b5d7d5c3-fb5a-44dc-9b99-02762e306aa4">
          * <img width="142" alt="스크린샷 2023-11-06 오후 4 55 00" src="https://github.com/sally-yeom/TIL/assets/61625764/5b1a15cd-eb52-48d7-a295-b09d02321fb2">
          * 각각 예측한 점수와 실제 점수 사이의 Error를 역전파 하는 형태로 FM Component, Deep Component를 한꺼번에 학습
      * FM Component와 Deep Component는 동일한 Feature Embedding을 공유해서 사용 (효율적)
          * Raw Data에서 low-order, high-order feature interaction을 함께 학습하기에 용이
          * 복잡한 feature engineering 필요 없음 (end-to-end)
  * 기존 모델과 비교
      * <img width="753" alt="스크린샷 2023-11-06 오후 5 40 02" src="https://github.com/sally-yeom/TIL/assets/61625764/391f93c4-2155-4380-9464-bda44a51c5c4">



- 참고
  - https://arxiv.org/pdf/1703.04247.pdf
