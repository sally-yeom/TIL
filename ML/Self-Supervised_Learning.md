## Representation Learning -> Embedding -> "압축"
  * representation learning은 한마디로 적절한 embedding을 배우는 것
      * Customer Embedding
      * Item Embedding
      * Category Embedding
      * ..

## Self-Supervised_Learning (SSL)
  * 레이블이 없거나 제한적으로 레이블이 있는 데이터를 사용하여 모델을 학습시키는 방법
  * SSL은 레이블이 없는 데이터를 활용하여 데이터의 표현을 학습하는 representation learning의 한 방법
  * SSL을 통한 embedding 학습 -> embedding을 이용한 downstream task
  * 결국, SSL은 Unlabeled 데이터로부터 좋은 Embedding을 배우고자 하는 것
  * Self-Supervised_Learning (SSL)이 중요한 이유?
      * 데이터를 유저로부터만 얻을 수 있기 때문에 서비스에서 추천 시스템을 위한 충분한 데이터를 가지기 어렵다
      * Unlabeled data로부터 좋은 representation을 배울 경우 다른 추천 모델에 도움이 된다
      * 실제로 NLP는 SSL로 엄청난 성과를 보았다 (EX. BERT, GPT ... )
