## Two-Tower_architecture
  * ![스크린샷 2023-11-12 오후 7 01 14](https://github.com/sally-yeom/TIL/assets/61625764/87a0c89d-df6a-4770-98eb-260510524977)
  * Dot Product를 유지
  * Query, User 및 Item의 Side Information 사용 가능
  * Two-Tower 아키텍쳐의 장점
      * 자유도 높은 구조로 비즈니스에 맞는 다양한 정보를 담은 임베딩을 생성할 수 있다
          * Only Item id, User id VS Meta data, Context data, Feature Interaction
      * User 타워와 Item 타워의 추론이 분리되어 있다
          * 서빙 시에는 User 타워만 추론에 사용된다
  * Two-Tower 아키텍쳐의 한계
      * User 타워는 온라인 추론이 가능하지만, Item 타워는 오프라인 추론만 가능하다
          * 즉, Item 타워의 피쳐에는 Context 피쳐가 포함될 수 없다




- 참고
  - https://blog.reachsumit.com/posts/2023/03/two-tower-model/
