## PEFT (Parameter-Efficient Fine-Tuning)
  * LLM 및 DL 모델을 효율적으로 미세조정(fine-tune) 하기 위한 접근 방식
  * 전체 모델 파라미터를 모두 업데이트하지 않고 일부 파라미터만 수정
  * 학습 효율성 및 저장 비용 크게 절감 → 리소스 제한이 있는 환경 (GPU, 메모리, 저장 공간) 에서 유리
  * 기존 Fine-tuning vs PEFT
      * Fine-tuning
          * 사전학습된 모든 파라미터를 업데이트 → 계산 비용 큼 & 메모리 사용 많음
          * 작은 데이터셋에 대해 전체 모델을 재학습할 경우 과적합 가능성 상승
      * PEFT
          * 일부 파라미터만 학습 → 전체 파라미터의 수 %1 미만만 조정
          * 나머지 파라미터는 고정 (frozen) 상태로 유지
          * 다양한 태스크에 빠르게 적응할 때 유리한 편


## 주요 PEFT 기법들
  * Adapter
      * 기존 모델의 각 Transformer 블록 사이에 작은 병렬 모듈(MLP) 삽입
      * 원본 모델은 고정하고, Adapter만 학습
      * 매개변수 수를 매우 적게 유지하면서 태스크 적응 가능
  * LoRA (Low-Rank Adaptation)
      * 모델의 가중치 행렬을 rank-decomposition 형태(A×B)로 분해하고, 그 부분만 학습
      * 기존 W를 고정한 채, ΔW = A·B 형태로 저차원 업데이트 수행
      * 매우 적은 파라미터로 높은 성능 달성 가능
      * Hugging Face PEFT 라이브러리에서 가장 널리 사용됨
  * Prefix Tuning
      * Transformer의 각 layer에 학습 가능한 prefix(가상 토큰 시퀀스) 를 추가
      * 입력에 영향을 주는 형태로 작동하되, 원래 모델 파라미터는 고정
      * 언어 생성이나 요약 같은 seq2seq 작업에 적합
  * Prompt Tuning / P-Tuning
      * 입력 토큰 앞에 학습 가능한 임베딩(pseudo tokens)을 추가
      * Prompt를 통해 모델이 특정 태스크에 더 잘 반응하도록 유도
      * P-Tuning v2는 Transformer 구조에 맞춰 deep prompt를 사용하는 방식
  * BitFit
      * 가장 간단한 방식 중 하나로, 각 층의 bias만 학습
      * 대부분의 파라미터를 고정해두고, 적은 수의 bias만 조정
      * 효율성은 높으나 복잡한 태스크에는 성능 한계 있음


## 대표 라이브러리
  * Hugging Face [PEFT 라이브러리](https://huggingface.co/docs/peft/en/index)
  * LoRA, Prefix Tuning, Prompt Tuning 등을 손쉽게 적용 가능
'''
EX) from peft import get_peft_model, LoraConfig, TaskType
'''



## LoRA 적용 예제 (Hugging Face)
'''
from peft import get_peft_model, LoraConfig, TaskType

peft_config = LoraConfig(
    task_type=TaskType.CAUSAL_LM, 
    inference_mode=False,
    r=8,
    lora_alpha=32,
    lora_dropout=0.1,
)

peft_model = get_peft_model(base_model, peft_config)
peft_model.train()

'''





