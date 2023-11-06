## Collaborative Filtering 기반 추천 시스템의 패러다임
  * MF : latent embedding feature를 기반으로 예측 수행
  * SVD++ : 유저의 interaction history도 함께 참고
  * NAIS (Neural Attentive Item Similarity) : 유저의 interaction history 내에서 아이템 별 가중치를 다르게 학습
      * User-Item Interaction Graph 측면에서 봤을 때 위와 같은 연구 흐름은, 유저와 연결된 데이터들의 subgraph, 1-hop neighbor를 참고해서 embedding learning을 개선했던 시도들
  * NGCF (Neural Graph Collaborative Filtering)
      * subgraph 구조를 활용해서 high-hop neighbor 관계까지 포착하려 함
      * <img width="566" alt="스크린샷 2023-11-06 오후 10 47 53" src="https://github.com/sally-yeom/TIL/assets/61625764/fbd22d14-32d0-4e39-906f-87069f2c959e">
      * <img width="581" alt="스크린샷 2023-11-06 오후 10 48 37" src="https://github.com/sally-yeom/TIL/assets/61625764/a32012a0-a44a-4f18-b9a6-3428c3250ff9">
      * <img width="563" alt="스크린샷 2023-11-06 오후 10 50 01" src="https://github.com/sally-yeom/TIL/assets/61625764/230619cb-c108-474d-a2a0-91d8117b6c03">
      * GCN 계열 모델의 핵심 로직은 Propagation을 통해 Embedding을 업데이트 시키는 것
      * 다른 GCN (Graph Convolution Network) 와 동일하게 다음의 단계가 존재하지만, 성능 개선과는 별개로 각각의 '필요성 (성능에 기여하는 정도)'을 확인하지 않고 통상적으로 사용
          * feature transformation -> 차원 수 조정
          * neighborhood aggregation
          * nonlinear activation -> 비선형적인 경향들까지 잡아냄
      * 하지만 GCN 구조의 특성(다양한 attribute를 전파)과 다르게, 현실에서 마주하는 데이터셋은 user-item interaction 데이터 정도로, 굳이 여러 겹의 nonlinear activation을 진행할 필요가 없음
          * 굉장히 많은 데이터셋이 존재하는 경우라면 효과적일 수도 있겠음
      * Ablation studies
          * <img width="1105" alt="스크린샷 2023-11-06 오후 10 59 37" src="https://github.com/sally-yeom/TIL/assets/61625764/c55de47a-89cf-4f7c-bbd4-0bdab2a1bec2">
            * NGCF-f : feature transformation W1, W2 제거
            * NGCF-n : nonlinear activation 쎄타 제거
            * NGCF-fn : 둘 다 제거
            * 각 임베딩 값을 기존의 모델에서 concat 해주던 방식에서 sum으로 변경하여 차이를 극명히 볼 수 있도록 함
          * feature transformation은 부정적 영향을 미침
          * nonlinear activation은 feature transformation이 포함되어 있을 때 긍정적인 영향을 끼치지만, feature transformation이 포함되어 있지 않을 때는 부정적 영향을 미침
          * 전체적으로 봤을 때 제거한 버전이 가장 좋은 성능을 보임


## LightGCN : Simplifying and Powering Graph Convolution Network for Recommendation
  * GCN (Graph Convolution Network) 기반의 추천 시스템
  * 협업 필터링 추천 시스템 (SOTA - 2023년 기준)
  * GCN 기반 모델이 추천 환경에 미치는 정확한 이해가 없기에 다음과 같은 문제 발생
      * Feature Transformation, Nonlinear Activation -> 퍼포먼스에 미치는 영향이 적음
      * Training 과정이 더 복잡해져서 성능이 저하되는 결과도 보임
  * GCN의 디자인을 단순하고 간결하게 만들어서 범용적으로 사용 가능하도록 디자인
      * GCN 모델의 주 요소는 유지하면서 모델을 크게 간소화
      * NGCF (Neural Graph Collaborative Filtering) 대비 평균 16% 성능 개선
  * 특징
      * more interpretable
      * practially easy to train and maintain
      * technically easy to analyze model behavior and revise
  * GCN의 기본적인 Idea
      * <img width="315" alt="스크린샷 2023-11-06 오후 11 09 22" src="https://github.com/sally-yeom/TIL/assets/61625764/cdd9cd77-f1a3-418d-bed3-8e539b8820c2">
      * 노드에 대한 representation을 그래프 상에서 계속 aggregation하며 update 하는 것 (주변 노드들의 정보를 모아 타겟 노드의 정보를 갱신)
      * AGG (Aggregation Function)
        * GIN : weighted sum aggregator
        * GraphSAGE : LSTM aggregator
        * BGNN : bilinear interaction aggregator
        * 위 방식들은 feature transformation과 nonlinear activation을 함께 사용하고 있음
      * LightGCN은 weighted sum aggregator-fn을 사용
  * Light Graph Convolution (LGC) 수식
      * <img width="563" alt="스크린샷 2023-11-06 오후 10 50 01" src="https://github.com/sally-yeom/TIL/assets/61625764/0175aef6-c3c0-4d02-93ef-cc655881ad77">  
      * <img width="288" alt="스크린샷 2023-11-06 오후 11 31 23" src="https://github.com/sally-yeom/TIL/assets/61625764/e9034d15-651c-4f13-aa76-495bbe9f8ba1">
      * nonlinear activation / feature transformation / self-connection 제거
      * self-connection이 가능하도록 layer combination 형태로 구성
      * embedding scale이 너무 커지는 것을 방지하기 위해 normalization term 활용
      * 각 타겟들의 이웃 노드를 활용해서 업데이트하는 방식만 남기고 나머지 세부적인 & 복잡한 내용들은 제거
      * 결국, 학습 가능한 parameter는 초기 임베딩 레이어 (0번째 레이어) 값
        * 다른 레이어들은 propagation rule에 의해 전파될 뿐
  * Matrix Form
      * <img width="572" alt="스크린샷 2023-11-06 오후 11 41 45" src="https://github.com/sally-yeom/TIL/assets/61625764/b6f2ce47-50f5-4063-8ae0-c81aac90b180">
      * <img width="642" alt="스크린샷 2023-11-06 오후 11 42 29" src="https://github.com/sally-yeom/TIL/assets/61625764/c8c67298-5e30-4538-a1e6-5473291aa7a4">
      * <img width="568" alt="스크린샷 2023-11-06 오후 11 44 41" src="https://github.com/sally-yeom/TIL/assets/61625764/b46837c6-b62b-49e7-93be-f1788e4970e3">
  * Layer Combination
      * <img width="563" alt="스크린샷 2023-11-06 오후 11 46 06" src="https://github.com/sally-yeom/TIL/assets/61625764/933ba0b4-f9fa-411a-932f-6cfc5c67ead4">
      * <img width="303" alt="스크린샷 2023-11-06 오후 11 46 19" src="https://github.com/sally-yeom/TIL/assets/61625764/8e9dcc74-b7f4-44c1-8847-2efa5a9e63d2">
      * 각각 user embedding / item embedding의 가중합 진행
        * a_k는 k번째 임베딩의 가중치
        * 학습 가능한 파라미터 or 어텐션 스코어 or 직접 설정 가능
        * <img width="221" alt="스크린샷 2023-11-06 오후 11 46 28" src="https://github.com/sally-yeom/TIL/assets/61625764/0ec68989-27d3-46ea-b57c-2e11b5e5a67d">
      * 초기 임베딩 값이 더해져 들어가는 부분 -> self-connection
      * 왜 각 레이어의 임베딩 값을 가중합 한 것인지?
        * layer의 수가 늘어나면, 최종 단계의 값이 over-smooth 됨
          * 주변 노드들을 여러번 propagation을 거치다 보면, 주변의 노드들과 특징이 비슷해지는 경향이 있음
          * 레이어가 깊어질 수록 최종 레이어들만 사용한다면 유저와 아이템의 고유한 값이 남아있지 않고 주변 노드들의 영향을 많이 받은 (일반화 된) 임베딩 값만 얻게 됨
          * 모든 레이어를 가중합 한다면 low-level의 임베딩 값도 사용하므로써 smoothing이 덜 된 값을 얻을 수 있음
        * 각각의 embedding layer들은 different proximity를 담아냄
          * 레이어가 깊어질 수록 더 멀리 있는 이웃 (high-hop) 유저와 아이템들의 특징까지 포함하는 임베딩 값을 얻을 수 있음
        * 서로 다른 layer의 임베딩을 가중합으로 결합하면 self-connection의 효과 가능
  * 최종 예측
      * <img width="119" alt="스크린샷 2023-11-07 오전 12 02 38" src="https://github.com/sally-yeom/TIL/assets/61625764/5c31dd31-0ec3-4792-9b89-2e9a8c6bd61e">
      * Adam Optimizer 사용
      * negative sampling, adversarial sampling 사용 X
      * dropout mechanism 사용 X
      * <img width="434" alt="스크린샷 2023-11-07 오전 12 03 48" src="https://github.com/sally-yeom/TIL/assets/61625764/8943a16a-383e-4b15-9f7d-a3fa81aa18af">
      * BPR Loss : 관측값(이웃 노드가 있는 경우)이 비관측값(이웃 노드가 없는 경우) 보다 스코어가 높도록 학습 (위 수식에서는 L2-norm 사용)


- 참고
  - LightGCN : https://arxiv.org/pdf/2002.02126.pdf
  - NGCF : https://arxiv.org/pdf/1905.08108.pdf
