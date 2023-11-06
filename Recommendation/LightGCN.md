## Collaborative Filtering 기반 추천 시스템의 패러다임
  * MF : latent embedding feature를 기반으로 예측 수행
  * SVD++ : 유저의 interaction history도 함께 참고
  * NAIS (Neural Attentive Item Similarity) : 유저의 interaction history 내에서 아이템 별 가중치를 다르게 학습
      * User-Item Interaction Graph 측면에서 봤을 때 위와 같은 연구 흐름은, 유저와 연결된 데이터들의 subgraph, 1-hop neighbor를 참고해서 embedding learning을 개선했던 시도들
  * NGCF (Neural Graph Collaborative Filtering)
      * subgraph 구조를 활용해서 high-hop neighbor 관계까지 포착하려 함
          * feature transformation
          * neighborhood aggregation
          * nonlinear activation
      * 다른 GCN (Graph Convolution Network) 와 동일하게 다음의 단계가 존재하지만, 성능 개선과는 별개로 각각의 '필요성 (성능에 기여하는 정도)'을 확인하지 않고 통상적으로 사용
      * 하지만 GCN 구조의 특성(다양한 attribute를 전파)과 다르게, 현실에서 마주하는 데이터셋은 user-item interaction 데이터 정도로, 굳이 여러 겹의 nonlinear activation을 진행할 필요가 없음


## LightGCN : Simplifying and Powering Graph Convolution Network for Recommendation
  * GCN (Graph Convolution Network) 기반의 추천 시스템
  * 협업 필터링 추천 시스템 (SOTA - 2023년 기준)
  * GCN 기반 모델이 추천 환경에 미치는 정확한 이해가 없기에 다음과 같은 문제 발생
      * Feature Transformation, Nonlinear Activation -> 퍼포먼스에 미치는 영향이 적음
      * Training 과정이 더 복잡해져서 성능이 저하되는 결과도 보임
  * GCN의 디자인을 단순하고 간결하게 만들어서 범용적으로 사용 가능하도록 디자인
      * GCN 모델의 주 요소는 유지하면서 모델을 크게 간소화
      * NGCF (Neural Graph Collaborative Filtering) 대비 평균 16% 성능 개선



- 참고
  - LightGCN : https://arxiv.org/pdf/2002.02126.pdf
  - NGCF : https://arxiv.org/pdf/1905.08108.pdf
