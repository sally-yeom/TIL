## Lightweight Techniques
  * Edge Device, Mobile 등에 탑재하기 위해 모델의 파라미터 수를 줄이는 방법


## Quantization (양자화)
  * 모델의 파라미터(가중치)를 32-bit float → 8-bit, 4-bit, 2-bit 등 더 작은 비트로 변환해 모델 크기와 연산량을 줄이는 방법
  * 계산 정확도 손실 가능 → 특히 softmax, layer norm, attention score 등 민감한 부분
  * 일부 연산은 정확도를 위해 FP32로 수행해야 하는 경우가 있음
  * 종류
      * Weight-only quantization: 가중치만 quantize
      * Activation quantization: 입력값도 quantize 하므로  hardware 가속 가능
      * GPTQ: 학습 없이 Hessian 정보를 기반으로 최소 손실 quantization
      * AWQ: Activation 범위를 기반으로 Weight 범위를 클러핑해 INT4화



## LoRA (Low-Rank Adaptation)
  * 기존 가중치 𝑊 ∈ 𝑅 𝑑 × 𝑘 W∈R d×k 를 동결(freeze)시키고, 학습 가능한 low-rank 행렬 𝐴 ∈ 𝑅 𝑑 × 𝑟 , 𝐵 ∈ 𝑅 𝑟 × 𝑘 A∈R d×r ,B∈R r×k 만 학습
  * W′ = W + ΔW = W + AB
  * 학습 중의 변경은 𝐴𝐵에만 적용되므로 원본 모델은 보호됨
  * 학습 파라미터 수가 대폭 감소되며 여러 task 별로 별도의 LoRA Adapter 저장이 가능
  * Adapter들을 병합하는 것도 가능함



## Pruning (가지치기)
  * 모델 내에서 중요도가 낮은 parameter 및 layer를 제거해 연산량을 줄이는(sparsity 증가) 방법
  * Pruned model은 sparse 연산 지원하는 runtime 필요함
  * Pruning을 진행하면 accuracy의 손실의 발생할 확률이 높으므로 Fine-tuning을 통해 accuracy 회복이 필요할 수 있음
  * 종류
      1. Unstructured Pruning
          * weight-level에서 작은 값들을 제거
          * 연산 최적화가 어렵지만 sparsity가 높음
      2. Structured Pruning
          * head, neuron, layer 단위 제거
          * GPU/TPU에서 최적화 용이
      3. Movement Pruning
          * weight의 gradient 움직임을 기반으로 중요도를 계산
          * Soft mask를 학습하여 pruning을 유도



## Knowledge Distillation (지식 증류)
  * 복잡한 모델(Teacher)의 출력을 활용하여 가벼운 모델(Student)을 학습시켜 성능을 보존하면서 경량화하는 방식
  * 학습 방식
      * Online Learning
          * Teacher 모델의 예측과 Student 모델이 학습이 동시에 진행됨
          * 두 모델을 올리고 학습할 수 있을 GPU/TPU 환경 필요
      * Offline Learning
          * Student 모델 독자적으로 학습하며 Teacher 모델의 예측값을 활용
      * Response-based Learning : soft target 사용
      * Feature-based Learning : 중간 layer의 hidden state도 학습
      * Relation-based Learning: token 간 관계를 학습



## Weight Sharing
  * Embedding layer와 decoder projection layer의 weight를 공유하는 방식
  * "W_embed = W_output" 이거나 여러 transformer block이 동일 weight를 공유하는 방식도 있음
  * 파라미터 수는 감소하게 되며 정규화 효과로 overfitting을 방지할 수 있음
​
