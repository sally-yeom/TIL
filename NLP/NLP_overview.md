## 자연어 처리(Natural Language Processing – NLP)
  * AI 모델을 활용하여 사람의 언어를 모방하는 모든 분야
  * 역사
      * ![스크린샷 2023-11-12 오후 8 55 15](https://github.com/sally-yeom/TIL/assets/61625764/a5fe7bcc-1fdc-48f1-a611-acb343907a54)
      * ![스크린샷 2023-11-12 오후 9 01 08](https://github.com/sally-yeom/TIL/assets/61625764/15f1994b-04de-441d-8598-02ccc7696748)



## Transformer
  * Attention Is All You Need (2017) 논문에서 제안
  * 그 중 핵심은? self-attention
      * Attention의 의미는 "강조" 이다
      * 어떤 말을 통해 의미를 전달하고자 할 때 핵심은 사실 한 두 문장, 혹은 한 두 단어에 압축 되어있음 (하나의 문장에서 단어 각각의 중요도가 다르다는 말)
      * 모델에게 언어를 가르칠 때 문장 내에서 단어 간 중요도에 차이가 있음을 알려주는 것
      * self-attention인 이유는 스스로가 스스로를 강조한다는 것
      * EX) ‘The man cross the river that is large with a small boat’ -> boat - small, river - large의 관계를 self-attention이 언어모델에게 알려줌
      * 한 단어가 어떤 단어를 좀 더 주위 깊게 살펴봐야 하는지 / 나열된 단어 간에 서로 어떤 연관성이 있는지 -> 자기 자신을 참조하고 강조하는 형태
  * Transformer에서 파생된 대표적인 두 개의 모델
      * Encoder : BERT(Bidrectional Encoder Representations from Transformers) / Google
      * Decoder : GPT(Generative Pretrained Transformer) / OpenAI
        * GPT-2, GPT-3은 GPT의 기본적인 구조를 그대로 사용하고 있으며, 모델의 사이즈의 차이가 있음 (더 거대해짐)
        * GPT3는 GPT1 대비 1400배, GPT2 대비 117배 증가
        * 모델 크기 증가는 언어모델 품질은 물론 각종 다운스트림 태스크의 성능 개선에 큰 도움이 되었음
      * 파생된 다른 언어 모델들
        * Transformer-XL : 좀 더 긴 문맥을 살피도록 확장
        * XLNet : auto-regressive (AR / GPT) 모델과 auto-encoder(AE / BERT) 모델의 장점을 합침
        * ALBERT : BERT의 한계점들을 개선시키기 위해 모델 크기는 줄이고, 성능은 높임
        * RoBERTa : BERT 추가 튜닝
        * XLM : 다국어를 목표로 사전 학습 시킨 BERT
        * Electra : GAN 방식 차용
        * ...
  * 모델 성능을 최대한 유지하면서 크기를 줄이려는 시도도 진행
      * 디스틸레이션 (Distillation)
      * 퀀타이제이션 (Quantization)
      * 프루닝 (Pruning)
      * 파라메터 공유 (Weight Sharing)
      * ...
  * ChatGPT
      * 대화형 인공지능 언어 모델
      * GPT 아키텍처를 기반 (GPT-3.5)
      * 사용자의 입력에 따라 일련의 대화를 형성
      * 질문에 대한 답변을 생성하거나 텍스트 요약, 글 작성 등 다양한 텍스트 생성 작업에 사용
      * 사용자가 원하는 내용을 정확하게 생성하기 위해서는 명확하고 구체적인 프롬프트를 제공하는 것이 중요
      * 프롬프트?
        * 사용자가 모델에게 입력하는 시작 문장, 모델이 이를 기반으로 텍스트를 생성
        * 프롬프트의 작성 방법과 내용에 따라 모델의 출력이 달라질 수 있기 때문에, 프롬프트 엔지니어링은 ChatGPT를 더 효과적으로 활용하기 위한 핵심적인 기술로 꼽힘
        * 다양한 방식으로 디자인 가능 (EX. 명확하고 구체적인 질문 형태 or 하는 텍스트의 스타일이나 톤을 명시)
  * Llama (Large Language Model Meta AI)
      * Meta AI에서 출시한 대규모 최신 언어 모델
      * Llama 2는 GPT-3.5 언어 모델보다 약간 더 높은 성능


## GPT와 BERT의 차이
  * ![스크린샷 2023-11-12 오후 8 28 42](https://github.com/sally-yeom/TIL/assets/61625764/234ff903-976d-4f3c-b5a5-131770a6c1b1)
  * GPT
    * 이전 단어들이 주어졌을 때 다음 단어가 무엇인지 맞추는 과정에서 프리트레인(pretrain)
    * 문장 시작부터 순차적으로 계산한다는 점에서 일방향(unidirectional)
    * 문장 생성에 강점을 가지고 있음
  * BERT
    * 마스크 언어모델(Masked Language Model)
    * 문장 중간에 빈칸을 만들고 해당 빈칸에 어떤 단어가 적절할지 맞추는 과정에서 프리트레인
    * 빈칸 앞뒤 문맥을 모두 살필 수 있다는 점에서 양방향(bidirectional)
    * 문장의 의미를 추출하는 데 강점을 가지고 있음




- 참고
  - https://blog.testworks.co.kr/natural-language-and-transformer-bert-gpt/
  - https://ratsgo.github.io/nlpbook/docs/language_model/bert_gpt/
  - https://modulabs.co.kr/blog/chatgpt-with-promptengineering/
  - https://www.samsungsds.com/kr/insights/chatgpt_whitepaper1.html
  - https://textcortex.com/ko/post/llama-2-vs-chatgpt
  - https://modulabs.co.kr/blog/llama-2-intro/
