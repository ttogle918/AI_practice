# 경량화
[blog 설명 바로가기](https://velog.io/@ttogle918/ML-%EA%B2%BD%EB%9F%89%ED%99%94-%EB%B0%A9%EB%B2%95)
모델의 파라미터 수도 많고, 연산량이 많으면 특징 추출하기 용이하고 결과값도 좋을 것이다.
하지만 mobile 환경이나 IoT, Embedded환경과 같이 속도, 배터리, Memory 등이 중요한 환경이라면 파라미터 수가 적고 연산량이 적지만 성능은 비슷한 작은 모델을 원할 것이다.
그래서 최적화가 필요하다.

모델을 최적화해야하는 이유
1. 모델의 크기를 줄일 수 있다 -> 모델의 크기, RAM 사용량 감소
2. 추론 시간 감소 -> 계산을 단순화하여 잠재적 정확성을 떨어뜨리는 방식으로 줄임(특정 모델은 최적화 프로세스로 인해 오히려 정확성이 개선될 수도 있다.) -> 전력 소비 감소

모델 경량화 방법
1. quantization(양자화) 
2. pruning, 잘라내기
3. 클러스터링
4. Knowledge distillation (지식 증류)

## quantization, 양자화
[blog 설명 바로가기](https://velog.io/@ttogle918/Quantization-%EC%96%91%EC%9E%90%ED%99%94)

양자화는 float타입인 Tensor 가중치와 활성화 함수를 int형으로 변환하여 모델의 크기를 줄이고 추론(test) 속도를 높이는 방법이다.

- float -> int
- 모델의 크기 ↓, 속도 ↑(빠르게), 성능(loss)은 그대로
- Inference(추론) 시간을 줄이기 위한 것이다.

**모델별 양자화 기법 선정**
![image](https://user-images.githubusercontent.com/17754713/183678110-fe044cba-9122-49f7-9e31-792618421a0e.png)

- Post Training Quantization 방식 : Training된 모델(Post Training)을 Quantization
  - 장점 : parameter size가 큰 대형 모델에 대해서 정확도 하락의 폭이 작다
  - 단점 : parameter size가 작은 소형 모델에 대해서 정확도 하락의 폭이 크다. Edge device 등이 작은 소형 모델과 경량화를 주로 사용하여 PTQ를 이용하면 좋은 성능을 기대하기 어렵다.
  - [Dynamic Quantization (동적 양자화) 코드 보기](Dynamic_Quantization_PyTorch.ipynb)
  - Static Quantization
- 학습 중 Quantization 수행 : 모델이 실제로는 float 계산을 하지만, 이후 양자화될 것이라고 자각한 채로 훈련이 이루어진다. Fake Quantization node를 통해 양자화시 어떻게 동작할 지 시뮬레이션.
  - 장점 : 일반적으로 가장 높은 정확도를 가진다. 모델의 정확도 감소 폭을 최소화할 수 있다.(소형 모델에서 QAT가 필수적이다.)
  - 단점 : 모델 학습 이후 추가 연산(양자화)이 필요하다.
  - Quantization Aware Training
  
