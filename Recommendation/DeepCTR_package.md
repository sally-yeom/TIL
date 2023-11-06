## DeepCTR
  * 딥러닝 기반 랭킹 모델 오픈소스 라이브러리
  * 회사가 아닌 개인이 하고있지만, 다 유명한 엔지니어들이 참여
  * TF2, Pytorch 지원 (API 사용 가능)
  * https://github.com/shenweichen/DeepCTR
  * 장점
      * 많은 추천 모델이 구현되어 있음 (공부하기에 좋을 듯)
      * tf.keras.Model API 및 tf.keras.Layer API로 구현하여 기존 시스템과 Integration이 쉬움
      * Recommendation task에 맞게 Univariate Categorical, Multivariate Categorical, Continuous Feature를 설정할 수 있음
  * Feature Columns를 나눠놓았음 (자주 다루는 애들을 묶어놓음)
      * SparseFeat -> Univariate Categorical Feature
      * DenseFeat -> Continuous Feature
      * VarLenSpareFeat -> Multivariate Categorical Feature
