## Approximate Nearest Neighbor (ANN)
  * Nearest Neighbor : Vector Space Model 에서 내가 원하는 Query Vector 와 가장 유사한 Vector를 찾는 알고리즘
  * 모델 서빙 관점에서 보면 모델 학습을 통해 구한 User / Item (Query) Vector가 주어질 때 이에 인접한 이웃을 찾아주는 것
  * NN의 가장 기본적 방식
      * Brute Force KNN으로 유사도를 정확하게 구하기 위해 모든 Vector와 유사도 비교를 수행
      * 차원의 개수에 비례한 Cost가 듬 -> 서빙 불가능
  * 그렇기 때문에 정확한 근접 이웃이 아닌 근사적으로 근접 이웃을 구한다 (정확도는 조금 포기하되 빠른 속도를 취하는 방법)
      * 아마 제일 정확(근사)할 거야! 로 해석해야 함
  * 종류
      * ANNOY(Approximate Nearest Neighbors Oh Yeah)
        * Spotify에서 개발한 tree-based ANN 기법
        * Vector 공간을 잘게 나눈 후, 잘게 나누어진 공간을 binary tree로 구성
        * NN 연산 시, 해당 벡터가 포함되는 공간을 tree 검색으로 찾음 -> 찾은 공간(권역) 내에서 NN 수행
      * Hierarchical Navigable Small World Graphs (HNSW)
        * 벡터를 그래프의 Node로 표현하고 인접한 벡터를 Edge로 연결하는 방식
        * Layer를 여러 depth로 만들어 계층적으로 탐색 진행
        * Layer 0에 모든 노드가 존재하여 최상위 Layer로 갈 수록 개수가 적어짐
          * 최상위 Layer의 임의의 노드(최상단 빨간노드) 에서 시작
          * 현재 Layer에서 타겟노드(최하단 초록노드)와 가장 가까운 노드로 이동
          * 더 가까워 질 수 없다면 하위 Layer로 이동
          * 타겟노드에 도착할 때 까지 2~3 반복
          * 2~4에서 방문했던 노드들로 후보 NN을 탐색
        * 대표 라이브러리 :  nmslib, faiss
   


## Faiss
  * Facebook AI Research에서 개발한 오픈 소스 라이브러리
  * 고차원 벡터 검색을 위한 최적화된 인덱싱 및 검색 알고리즘을 제공
  * 규모 데이터셋에서 빠른 검색 속도와 높은 정확도를 달성할 수 있도록 설계


- 참고
  - ANN
    - https://velog.io/@minchoul2/RecSys-ANN-Approximate-Nearest-Neighbor-%EA%B8%B0%EB%B2%95
    - https://brunch.co.kr/@goodvc78/15
  - Faiss
    - https://velog.io/@acdongpgm/Faiss.-IVFPQ
