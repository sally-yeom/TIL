## CatBoost
  * Gradient Boosting Decision Tree의 구현체 중 하나
  * 러시아 검색엔진 Yandex에서 오픈소스로 공개
  * Categorical Feature를 다루는데 특화
      * Numerical Feature가 더 많다면 XGBoost, LightGBM을 고려하는 것도 괜찮을 듯? 
  * 오픈 소스로 공개되어 있음
      * https://github.com/catboost/catboost
      * https://catboost.ai/en/docs/
  * 특징
      * Feature에 대한 전처리 불필요
      * 카테고리형 변수에 대한 자동 처리 기능 내장
          * Preprocessing 과정에서 one-hot으로 바꿀 필요 X
      * Feature Importance 제공
          * 설명력 Up
      * Spark 사용 가능
      * 빠른 속도
      * 우수한 성능
  * 구성
      * CatBoostClassifier
      * CatBoostRegressor
      * CatBoostRanker
          * Learning to Rank에 특화
          * pairwise, listwise loss 사용 가능
            * YetiRankPairwise
            * PairLogitPairwise
            * QueryCrossEntropy
          * Ranking 용 Meric 제공
