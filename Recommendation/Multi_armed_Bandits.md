## A/B Test Recap
  * 목적
    * A, B 안 중 어떤게 가장 좋은 성과를 얻을 수 있을까?
  * A/B Test 컨셉
    * 특정 기간 동안, User마다 A, B (or C, D ...까지 N개) 안 중 랜덤하게 노출하여 가장 좋은 성과를 가지는 안 선택
  * 잔존하는 문제?
    * 탐색과 활용의 문제 (Exploration - Exploitation tradeoff)
      * 탐색 (Exploration)
        * 가장 나은 대안을 찾기 위해 테스트하는 과정
        * 테스트를 할 수록 기회비용 발생, A가 좋을 것으로 예상되었지만 실제 테스트 결과 A가 더 좋은것으로 나온다면?
        * B를 테스트(노출)하였던 기회비용 발생
      * 활용 (Exploitation)
        * 테스트를 중단하고 결정된 대안을 선택하는 것
        * 테스트 기간은 어느정도가 적정한 것인가? -> "적당히 길어야 함" -> 주관적
        * 테스트 기간이 짧으면 신뢰성을 보장하기가 어려움
        * 대체적으로 최소한의 비즈니스 사이클을 포함하도록 설정
          * 주말의 매출이 크기 때문에 최소한 주말은 포함해야 함
          * 계절성을 고려해 테스트 기간을 정해야 함 (그러나 기간 설정에 따라 결과는 달라질 수 있음)
      * 결국 테스트가 많을 수록 비용문제, 적게 할 수록 신뢰성의 문제가 발생하는 것

## MAB (Multi Armed Bandit)
  * 개념
    * 여러 대의 슬롯 머신이 존재하며 각 슬롯 당 돈을 따고 잃을 확률이 다른 경우, 어떻게 해야 가장 돈을 딸 확률이 높은 슬롯을 선택할 수 있을까?
    * Exploration - Exploitation tradeoff 가 이 상황에도 동일하게 적용
      * Exploration : 어느 슬롯이 수익률이 좋을지 확인하기 위해 모든 슬롯을 여러번 당겨봄 -> 그만큼 많은 돈이 필요
      * Exploitation : 한두 번씩만 당겨 가장 높은 수익을 보이는 슬롯을 택함 -> 가장 수익률이 높다고 단정하기 어려움
    * MAB는 Exploration과 Exploitation을 최적화하여, 매번 수익률이 높을 것으로 예상되는 슬롯을 선택해 수익률을 극대화
  * 용어
    * 행동 (Action) : MAB에서 선택된 대안
    * 보상 (Reward) : 대안 선택에 따른 수치화된 결과 (EX. 클릭, 구매)
    * 가치 (Value) : 행동으로 인한 기대 보상
    * MAB에서는 모든 행동은 순서대로 발생한다고 가정
    * t : 시점
    * <img width="503" alt="스크린샷 2023-07-23 오후 5 16 03" src="https://github.com/sally-yeom/TIL/assets/61625764/7a97c564-8c3b-480b-8208-0caf3a983980">
    * <img width="686" alt="스크린샷 2023-07-23 오후 5 22 54" src="https://github.com/sally-yeom/TIL/assets/61625764/1e28a503-b819-4329-b37a-8c47c06d1fbc">

## MAB의 알고리즘 (Policy)
  * 그리디 (Greedy)
    * 가장 간단한 Policy 
    * Q_t(a)를 구하기 위해 action에서 얻은 reward의 단순평균 사용 (현재까지 관측된 개별 슬롯 reward의 표본평균을 구함) -> 평균 reward가 최대인 action을 선택
    * <img width="684" alt="스크린샷 2023-07-23 오후 5 30 33" src="https://github.com/sally-yeom/TIL/assets/61625764/54b7853c-ff93-4eab-926a-49268c7215f6">
    * <img width="198" alt="스크린샷 2023-07-23 오후 5 32 49" src="https://github.com/sally-yeom/TIL/assets/61625764/9ab4366d-3262-4e3a-9f01-76c8c643122e">
    * Q_t(a)는 reward가 수집될 수록 계속 업데이트되며, reward가 최대인 action이 선택됨
    * 단점
        * 처음에 선택되는 슬롯이 본래 좋은 reward를 주는 슬롯이었지만, 하필 낮은 reward를 주었다면?
        * 해당 슬롯은 reward 평균이 낮기 때문에 다시 선택될 기회가 사라짐 (Exploration이 충분히 되지 않은 상태에서 Exploitation 진행)
  * 입실론-그리디 (Epsilon-Greedy)
    * Greedy에서 Exploration을 촉진하도록 보완된 Policy
    * Epsilon(ϵ)은 작은 숫자를 나타내는 그리스 문자
    * 일정한 확률로 greedy 하게 선택할지(1-ϵ) 랜덤하게 선택할지(ϵ)를 결정
    * <img width="480" alt="스크린샷 2023-07-23 오후 7 46 16" src="https://github.com/sally-yeom/TIL/assets/61625764/df2f2149-6f7a-4ca3-b760-d09422104070">
    * MAB 비교시 베이스로 많이 사용됨
    * 단점
        * 데이터가 많이 쌓여 최적의 값을 찾았더라도, 항상 ϵ의 확률로 무작위 탐색 (Exploration)을 하기 때문에 후반에는 최적 값과 멀어지는 결과가 나올 수 있음
        * Exploration을 과도하게 하는 문제
  * UCB (Upper Confidence Bound)
    * 시간이 지날수록 Exploitation을 증가시키는 방식
    * 추정된 가치 Q_t(a)에서 일종의 신뢰구간을 구하여, 그 구간의 위쪽 신뢰구간의 행동을 선택
        * <img width="707" alt="스크린샷 2023-07-23 오후 7 57 54" src="https://github.com/sally-yeom/TIL/assets/61625764/af44bb40-592f-4026-92ef-d09177c76e33">
        * t : 현재 시점
        * N_t(a) : 현재 시점까지 행동 a를 한 횟수
        * 위 식의 형태는 일반적인 신뢰구간을 구하는 식이 변형된 것
          * μ+c(σ^2/n)^(1/2)에서 μ -> Q_t(a) / σ^2 -> ln(t) 로 변경
        * 상수 c는 신뢰구간 폭을 제어하는 Parameter
          * c가 커지면 Exploration을 많이 하게되고, 작아지면 Exploitation을 많이 하게 됨
        * UCB 수식의 첫번째 항 Q_t(a)는 Exploitation에 중점을 둔 항이고, 두번째 항은 Explotation에 중점을 둔 항
  * 톰슨 샘플링 (Thompson Sampling)
    * 주어진 K개의 슬롯의 확률 분포를 구하는 문제
    * Action a에 해당하는 Reward 추정치인 Q_t(a)를 계산할 때 확률 분포를 따른다고 가정하고 그 추정치를 계속 업데이트하는 방법
    * 베이지안 추정
        * 관심있는 모수에 대한 사전 분포를 정의하고, 관측된 값으로부터 사후 분포를 이끌어냄 (모수값 분포 추정)
        * 사전확률 분포와 관측 데이터에 대한 가능도(likelihood)가 있다면, 베이즈 정리를 통해 사후확률 분포 추정 가능
          *<img width="777" alt="스크린샷 2023-07-23 오후 8 23 08" src="https://github.com/sally-yeom/TIL/assets/61625764/8fdb29ee-7df1-4d36-9a00-1d72f5baebc3">
          * 사전확률 분포 = 사전에 알고 있던 클릭률의 분포
          * 가능도 = 베르누이 시행 관측 데이터 (클릭 발생 or 미발생) -> 독립적인 베르누이 분포의 곱
          * 사후확률 분포 = 다음 시도 횟수 때 클릭률의 분포
        * 어떤 사전 확률 분포와 어떤 가능도 함수를 사용하냐에 따라 사후확률 분포의 모양이 달라짐
    * 주로 베타분포를 많이 사용
        * <img width="539" alt="스크린샷 2023-07-23 오후 8 25 32" src="https://github.com/sally-yeom/TIL/assets/61625764/2f870b10-283d-4a75-99be-9f10a102582e">
        * α, β에 따라 모양이 다양하게 구성될 수 있음
        * 켤레 사전 분포 (Conjugate prior) 만족
          * 베타분포가 사전확률 분포로써 베르누이 분포와 함께 베이지안 추정에 사용될 때, 사후확률 분포도 모수만 다를 뿐, 베타분포를 따름
          * <img width="390" alt="스크린샷 2023-07-23 오후 8 37 51" src="https://github.com/sally-yeom/TIL/assets/61625764/485600d4-0b9f-4d4e-876a-9411f3fdf8a8">
    * 시행 전 가정
        *  α : 노출이 되고 클릭한 횟수
        *  β : 노출이 되고 클릭하지 않은 횟수
        *  Beta(α+1,β+1) : 베타분포
        *  Beta(α+1,β+1)을 따른다고 가정했으므로 -> 베타분포에서 샘플링한 값이 최종적으로 Item을 클릭할 확률
    * Step 별 설명
        *  ...
        *  ...
    * Step 별 추세
        * <img width="714" alt="스크린샷 2023-07-23 오후 8 39 36" src="https://github.com/sally-yeom/TIL/assets/61625764/1f893e7b-47ba-4244-830f-94d7af64288a">
        * <img width="712" alt="스크린샷 2023-07-23 오후 8 39 47" src="https://github.com/sally-yeom/TIL/assets/61625764/68ed7983-e6d2-40c3-b0ea-446fcb633cf2">
        * <img width="705" alt="스크린샷 2023-07-23 오후 8 39 53" src="https://github.com/sally-yeom/TIL/assets/61625764/a87f281f-a4e2-4dbe-b99b-a11c699ddd10">
        * <img width="706" alt="스크린샷 2023-07-23 오후 8 40 03" src="https://github.com/sally-yeom/TIL/assets/61625764/ff12e647-b11d-4e19-9699-369eb1a17718">
    * 위와 같은 과정이 진행되면, Exploitation과 Exploration이 확률 분포를 따라 적절한 Trade-off가 유지되며 다양한 Item을 노출시키게 됨
    * 그리고 결국에는 가장 Reward가 높은 Item을 노출하는 것으로 수렴하는 결과를 얻을 수 있음
  * LinUCB
    * 각 User의 Context Vector에 따라서 어떤 Item이 더 높은 Reward를 줄지(클릭율이 높을지) 보고 추천하도록 학습
    * Context : ID 외의 Features (User의 demographic, Item categorhy, tags)
    * Context-free Bandit
        * 동일한 Action에 대한 User의 Context 정보에 관계없이 항상 동일한 Reward를 가진다고 가정하고 모델링하는 방법 (UCB, Epsilon Greedy)
    * Contextual Bandit
        * User의 Context 정보에 따라 동일한 Action이더라도 다른 Reward를 가진다고 가정
        * 개인화 추천과도 연관있음
    * 정의
        * <img width="687" alt="스크린샷 2023-07-23 오후 9 26 16" src="https://github.com/sally-yeom/TIL/assets/61625764/b2711848-e3f1-4c39-9289-b63d013a8aa0">
    * 예시
        * <img width="685" alt="스크린샷 2023-07-23 오후 9 30 33" src="https://github.com/sally-yeom/TIL/assets/61625764/c0ebf1cc-acde-4fb1-bc44-026883c1957b">
        * 위와 같이 서로 다른 Context를 가진 3명의 User가 존재하는 경우
          * x_t는 각 유저의 Context Vector로 4차원으로 각 차원은 다음의 특성을 갖는다고 가정 (male, female, young, old)
          * ([1,0,0,1]은 male과 old의 특성)
        * 각 User들이 어떤 Item을 선택하느냐에 따라 MAB 추천이 달라짐 -> 각 Item Action θ_a^∗에 대해 학습 필요
        * <img width="688" alt="스크린샷 2023-07-23 오후 9 34 55" src="https://github.com/sally-yeom/TIL/assets/61625764/30c1b886-f263-4948-bca1-54b98c0988ba">
        * 첫 번째 Action (θ_1^∗)은 2명에게 수집되었으므로 D_1 업데이트 (이하 동문)
        * 이렇게 진행하면 Context vector와 같은 차원의 θ_a^∗가 구해짐
          * θ_1^∗ : 2번째 차원이 가장 높은 weight / female 특성을 가진 User에게 줄 수 있는 Reward가 가장 큼
          * θ_2^∗ : 4번째 차원이 가장 높은 weight / old 특성을 가진 User에게 줄 수 있는 Reward가 가장 큼
          * θ_3^∗ : 3번째 차원이 가장 높은 weight / young 특성을 가진 User에게 줄 수 있는 Reward가 가장 큼


## MAB를 적용한 추천 시스템





- 참고
  - https://playinpap.github.io/mab/#%ED%86%B0%EC%8A%A8-%EC%83%98%ED%94%8C%EB%A7%81-thompson-sampling
  - https://velog.io/@minchoul2/RecSys-%EC%B6%94%EC%B2%9C%EC%9D%84-%EC%9C%84%ED%95%9C-MABMulti-Armed-Bandit-%EC%8B%AC%ED%99%94-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98Thompson-sampling-LinUCB
  - https://yjjo.tistory.com/21
  - https://github.com/conormm/bandit_algorithms/blob/master/bandits_post_code.py
  - http://www.kwangsiklee.com/2018/03/%ED%86%B0%EC%8A%A8-%EC%83%98%ED%94%8C%EB%A7%81thompson-sampling%EC%97%90-%EB%8C%80%ED%95%9C-%EC%A7%81%EA%B4%80%EC%A0%81%EC%9D%B8-%EC%9D%B4%ED%95%B4/

