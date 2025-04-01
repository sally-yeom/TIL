## Prompt Engineering
  * LLM 모델에서 원하는 력 결과를 얻기 위해 입력 프롬프트를 설계 / 조정하는 기술


## 지시형 프롬프트 (Instruction Prompting)
  * 명확하고 구체적인 지시를 포함시켜 모델이 무엇을 해야 하는지 분명히 전달
  * EX) 다음 텍스트를 한 문장으로 요약해줘.


## 샷 프롬프트 (Few-shot, One-shot, Zero-shot)
  * Zero-shot
      * 예시 없이 바로 작업을 지시 (Description)
  * One-shot / Few-shot
      * 1개 또는 몇 개의 예시를 제공해 모델이 패턴을 학습하도록 유도
  * “질문: … 답: …” 형태의 예시 제공


## Chain-of-Thought (CoT) Prompting
  * 모델이 단계별로 추론하도록 설명으로 유도
  * 복잡한 문제 해결 능력을 향상시키고자 할 때 씀
  * EX) "생각을 단계별로 설명해줘."
  * 단일 프롬포트 뿐만이 아닌, 여러번의 LLM 모델 Call 을 통해 Chain을 형성하는 것도 가능 (반복 및 후속 프롬프트 / Refinement Prompting)
      * 이전 응답을 바탕으로 수정/보완을 요청하여 품질을 개선하는 방식


## Role-based Prompting
  * 모델에게 역할을 부여해 특정 관점이나 톤을 유도
  * EX) 너는 역사 선생님이야. 학생에게 설명하듯 말해줘.


## 컨텍스트 확장 (Context Priming)
  * 필요한 배경 정보나 용어 정의를 사전에 제공하여 더 정확한 응답 유도
  * LLM Fine-tuning 시에는 모델을 해당 단어에 대한 Token에 더 많이 노출시켜, 더 유관한 단어를 생성하도록 하는 특징이 있음
​

## Output Format Control
  * 원하는 출력 포맷(JSON, 표, 목록 등)을 명시해 결과를 구조화
  * EX) 결과를 JSON 형식으로 출력해줘.
