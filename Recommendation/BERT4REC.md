## BERT4REC
  * 개념
      * <img width="477" alt="스크린샷 2023-11-03 오후 5 48 19" src="https://github.com/sally-yeom/TIL/assets/61625764/0a83d2a0-4aeb-4c19-91c8-e6a977e507e6">
      * 시퀀스 기반 딥러닝 모델(Bi-directional Encoding을 이용한 Pretrain 모델) Bert를 추천에 적용
      * Masked Language Model을 적용한 양방향 모델
        * Transformer의 인코더 및 디코더 파트의 구조를 활용
        * Pre-train : Encoder의 Masked Language Model 구조를 차용, 양방향의 정보를 활용해 학습
        * Fine-tuning : Decoder 파트로 예측 (Next  Token Prediction)
      * Multi Head Attention
        * Q, K, V를 각각의 Head 별로 쪼갬 -> 각각의 Attnetion을 구한 뒤 concat -> 최종 예측에 사용
      * SASREC은 BERT4REC의 특이 케이스라고 볼 수 있음
        * Single Head Attention + Last Item Masking
  * BERT란?
      *<img width="930" alt="스크린샷 2023-11-03 오후 5 52 17" src="https://github.com/sally-yeom/TIL/assets/61625764/78278d6a-8807-4aa0-9ede-ca67f789c9ff">
      * <img width="750" alt="스크린샷 2023-11-03 오후 5 52 25" src="https://github.com/sally-yeom/TIL/assets/61625764/ddb50fe1-064d-4a4a-b837-72ee2336c4fe">
      * Masked Language Model의 하나로 Bi-directional Transformer Encoder Block으로 구성됨
        * 다음 토큰을 예측하는 Autoregressive 한 모델이 아님!
      * 문장의 가운데를 뚫어 놓고, 이를 맞추는 방식으로 학습 (Randomly Masking)
        * 주변 토큰의 맥락을 활용
      * Bi-directional 학습
        * <img width="906" alt="스크린샷 2023-11-03 오후 5 25 41" src="https://github.com/sally-yeom/TIL/assets/61625764/eff45eb1-d4d1-4b3b-8fe3-3a873e00d31f">
        * Masked Token 주변의 단어로부터 양방향 정보를 활용해 예측, 학습
        * Test 과정에서는 마지막 Token만 Masking 함으로써 성능 측정
   



- 참고
  - BERT
      - https://arxiv.org/pdf/1810.04805.pdf
      - https://wikidocs.net/115055
      - https://happy-obok.tistory.com/23
  - BERT4REC
      - https://arxiv.org/pdf/1904.06690.pdf
      - https://wikidocs.net/177952
      - https://huidea.tistory.com/290
      - https://greeksharifa.github.io/machine_learning/2021/12/12/Bert4Rec/
  - https://dhgudxor.tistory.com/9
