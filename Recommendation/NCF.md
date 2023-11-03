NCF

## Neural Collaborative Filtering (NCF)
  * 개념
      * 선형 모델인 MF의 속성과, 비선형 모델인 MLP를 함께 고려하여 모델링
      * 협업 필터링 모델링에 뉴럴넷을 적용한 초기 모델의 대표격
      * GMF (Generalized Matrix Factorization)와 MLP를 결합함으로써 User-Item Interaction의 선형적 / 비선형적 패턴을 모두 잡아냄
  * 선형 모델의 한계점
      * Interaction Matrix에 대해 User와 Item의 Latent Factor 관점에서 내적을 취해 얻어지는 선형 변환 -> 선형 모델
      * <img width="583" alt="스크린샷 2023-11-03 오후 8 38 09" src="https://github.com/sally-yeom/TIL/assets/61625764/7c6c4dd2-1723-42e6-8272-34c0bb357c6d">
      * Implicit Feedback : 0이 비선호를 의미하고, 1이 선호를 의미하는게 아님 -> 모름
      * Implicit Matrix 상에서 선형 기반의 MF 모델은 표현에 더 큰 제약을 가짐 (if-else 와 같이 선형적인 패턴만 잡아낼 뿐 상대적으로 잘 동작하지 않는다)
      * K(latent factor)의 차원을 늘린다면 어느정도 대응이 가능하나, 과적합의 문제가 생길 수 있음
      * 복잡한 상호 관계 고려 필요! -> 딥러닝 도입 필요
  * NCF 구조
      * <img width="577" alt="스크린샷 2023-11-03 오후 8 50 34" src="https://github.com/sally-yeom/TIL/assets/61625764/63f231bb-9de4-469e-be53-722dda536a2d">
      * CF를 뉴럴렛으로 구현
      * 입력 형태 : User와 Item에 대한 one-hot vector -> K 차원으로 mapping하는 레이어 통과 (Embedding Layer)
      * Binary Cross-entropy Loss (Log-loss)가 사용되어 Implicit Feedback의 확률적인 특성 반영
        * Binary 한 특성을 잘 캐치하기 위함
        * Implicit Data는 Squared Loss 등이 가정하는 Gaussian 분포를 잘 따르지 않음
      * Latent Factor Mapping도 뉴럴렛으로 구현 -> 전달된 Latent Factor가 첫 번째 Layer에 concat
      * Point-wise 방식의 예측을 하고 있음
        * 모델링을 위한 negative sample은 uniform 분포에서 추출 (랜덤 추출)
        * 인기도 기반으로 추출하면 더 잘 작동한다고 함
  * NeuMF (MLP + GMF)
      * <img width="608" alt="스크린샷 2023-11-03 오후 9 09 00" src="https://github.com/sally-yeom/TIL/assets/61625764/fe10569a-1978-4219-b996-4b8e092e8892">
      * GMF : MF의 내적 부분을 element-wise 곱 연산과 비선형 활성함수 (sigmoid) 로 대체하여, 기존의 MF를 일반화 함
      * GMF는 비선형성을 잡아내기 어렵다는 한계가 있고, MLP는 선형적 상호작용을 잡아내는데 효율적이지 않을 수 있음
      * 두 모델을 조합하여 서로의 장단점을 상호 보완 (각각의 결과를 concatenation)
      * 활성함수 : ReLU
        * Sparse한 Activation의 형태를 띄고 있음 -> sparse한 추천 데이터에 적합 / overfiting 방지 가능



- 참고
  - https://arxiv.org/pdf/1708.05031.pdf
  - https://leehyejin91.github.io/post-ncf/
  - https://supkoon.tistory.com/28
  - https://lsjsj92.tistory.com/613
