## BERT4REC
  * 개념
      * Bert의 Masked Token Prediction에서 단어 Token을 상품으로 변경
        * 한 User의 Sequence에 담긴 상품/콘텐츠 List의 일부를 Masking 한 뒤 Prediction 하면서 학습 진행
        * Test 시에는 맨 마지막 상품/콘텐츠를 예측하도록 설계
      * <img width="477" alt="스크린샷 2023-11-03 오후 5 48 19" src="https://github.com/sally-yeom/TIL/assets/61625764/0a83d2a0-4aeb-4c19-91c8-e6a977e507e6">
      * 시퀀스 기반 딥러닝 모델(Bi-directional Encoding을 이용한 Pretrain 모델) Bert를 추천에 적용
      * Masked Language Model을 적용한 "양방향 모델" -> 논문에서는 양방향 모델의 학습 방법의 효과 입증에 초점
        * Transformer의 인코더 및 디코더 파트의 구조를 활용
        * Pre-train : Encoder의 Masked Language Model 구조를 차용, 양방향의 정보를 활용해 학습
        * Downstream Task Fine-tuning : Decoder 파트로 예측 (Next  Token Prediction)
      * Multi Head Attention
        * Q, K, V를 각각의 Head 별로 쪼갬 -> 각각의 Attnetion을 구한 뒤 concat -> 최종 예측에 사용
      * SASREC은 BERT4REC의 특이 케이스라고 볼 수 있음
        * Single Head Attention + Last Item Masking

## BERT
  * 개념
      * 단어 임베딩을 위해 사용된 Word2Vec, Glove, Fasttext 방식 외에도 MLM인 BERT를 사용해 임베딩을 표현할 수 있음
      * <img width="930" alt="스크린샷 2023-11-03 오후 5 52 17" src="https://github.com/sally-yeom/TIL/assets/61625764/78278d6a-8807-4aa0-9ede-ca67f789c9ff">
      * Masked Language Model의 하나로 Bi-directional Transformer Encoder Block으로 구성됨
        * 다음 토큰을 예측하는 Autoregressive 한 모델이 아님!
      * 문장의 가운데를 뚫어 놓고, 이를 맞추는 방식으로 학습 (Randomly Masking)
        * 주변 토큰의 맥락을 활용
      * Bi-directional 학습
        * <img width="906" alt="스크린샷 2023-11-03 오후 5 25 41" src="https://github.com/sally-yeom/TIL/assets/61625764/eff45eb1-d4d1-4b3b-8fe3-3a873e00d31f">
        * Masked Token 주변의 단어로부터 양방향 정보를 활용해 예측, 학습
        * Test 과정에서는 마지막 Token만 Masking 함으로써 성능 측정
      * input representation
        * <img width="750" alt="스크린샷 2023-11-03 오후 5 52 25" src="https://github.com/sally-yeom/TIL/assets/61625764/ddb50fe1-064d-4a4a-b837-72ee2336c4fe">
        * <img width="573" alt="스크린샷 2023-11-03 오후 7 29 56" src="https://github.com/sally-yeom/TIL/assets/61625764/2419ed30-4373-4aa7-97ec-f23c165facd6">
        * Token Embeddings
         * 실질적인 입력이 되는 워드 임베딩. 임베딩 벡터의 종류는 단어 집합의 크기
         * Word Piece 임베딩 방식 (토크나이저) 사용
         * 단어보다 더 작은 단위로 쪼개는 서브워드 토크나이저
         * 바이트 페어 인코딩(Byte Pair Encoding, BPE)의 유사 알고리즘
         * 과정 : 토큰이 단어 집합에 등장한다면 그대로 사용 or 토큰이 단어 집합에 등장하지 않는다면, 해당 토큰을 서브워드로 분리하고 첫번째 서브워드를 제외한 나머지는 "##"를 붙여 단어 집합에 추가
        * Position Embeddings
         * 위치 정보를 학습하기 위한 임베딩. 임베딩 벡터의 종류는 문장의 최대 길이
         * 학습을 통해서 얻는 임베딩
         * WordPiece Embedding과 더해줌 (위치 정보를 더함)
         * 문장의 길이만큼 임베딩 존재 (MAX 512개)
        * Segment Embeddings
         * 두 개의 문장을 구분하기 위한 임베딩. 임베딩 벡터의 종류는 문장의 최대 개수 (2개)
        * (+) Attention Mask
         * 불필요한 패딩 토큰에 어텐션을 주지 않도록, 실제 단어와 패딩 토큰을 구분하는 입력 (0 : 마스킹 O, 1 : 마스킹 X)
      * Pre-train 상세
        * 아래 두 가지 과정을 loss를 줄이면서 동시에 학습
        * Masked Language Model (MLM)
         * 학습에 들어가는 입력 텍스트의 15%를 랜덤으로 마스킹 (Masking) -> 가려진 단어를 예측하도록 함
         * 더 정확히는 마스킹 대상 중, 80% -> [MASK] / 10% -> 랜덤으로 단어 변경 / 10% -> 동일하게 둠
         * 모델은 위 대상을 예측 (나누는 이유는 파인 튜닝 단계에서는 [MASK]가 없기 때문에 데이터 불일치가 발생하기 때문)
         * <img width="475" alt="스크린샷 2023-11-03 오후 7 34 33" src="https://github.com/sally-yeom/TIL/assets/61625764/3ea40a79-1a88-45f4-bcc8-b5fc28981c0c">
        * Next Sentence Prediction (NSP)
         * <img width="526" alt="스크린샷 2023-11-03 오후 7 30 16" src="https://github.com/sally-yeom/TIL/assets/61625764/48d47fb9-6032-46eb-95d1-ff592442cf05">
         * 두 개의 문장을 준 후에 이 문장이 이어지는 문장인지 아닌지를 맞추는 방식으로 훈련
         * 50:50 비율로 실제 이어지는 두 개의 문장과 랜덤으로 이어붙인 두 개의 문장을 주고 훈련
        * Token 설명
         * [CLS] : 분류 문제를 풀기 위해 추가된 특별 토큰 (문장이 실제 이어지는 문장인지, 아닌지 등)
         * [SEP] : 문장의 끝에 추가하는 토큰
         * [PAD] : 문장이 끝났으나, 학습을 위해 채워주는 빈 값
      * Fine-tuning 상세
        * Bert의 각 Token의 output에 Dense Layer(Fully-connected Layer)를 추가하여 예측 진행
        * 종류
         * 하나의 텍스트에 대한 텍스트 분류 유형(Single Text Classification)
         * 하나의 텍스트에 대한 품사 / 개체명 태깅 작업(Tagging)
         * 텍스트의 쌍에 대한 분류 또는 회귀 문제(Text Pair Classification or Regression)
         * 질의 응답(Question Answering)

   



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
