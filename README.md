# AI_practice


### [QA Task](https://github.com/ttogle918/AI_practice/tree/main/QA%20task)

KorSQuAd를 사용하여 QA task 풀기(BertModel fine-tuning)

1. [01_BERT_QA_workflow.ipynb](https://github.com/ttogle918/AI_practice/blob/main/QA%20task/01_BERT_QA_workflow.ipynb)
  - 기존에 pre-training된 모델을 가져와서 결과값을 도출하는 과정
  - fine-tuning하지 않았다.  
2. [02_BERT_QA_squad_BertForQuestionAnswering.ipynb](02_BERT_QA_squad_BertForQuestionAnswering.ipynb) : 미완성
  - BertForQuestionAnswering(transformers 패키지에 구현된 클래스)로 해당 데이터셋을 추가하여 fine-tuning   
3. [03_BERT_QA_korsquad_BertModel로구현.ipynb](https://github.com/ttogle918/AI_practice/blob/main/QA%20task/03_BERT_QA_korsquad_BertModel%EB%A1%9C%EA%B5%AC%ED%98%84.ipynb)
  - BertModel로 결과값 도출 1 layer를 쌓아 미세조정
  - context에서 정답인 부분을 1로 하여 정답 위치 찾기
  - (question + context) token이 512 이하가 되도록 context를 전처리하여 사용
  - 전처리 시 'UNK'부분을 삭제할 것인가?
    - 삭제 x : answer text에도 'UNK'가 있었다. 만약 삭제한다면 answer text도 삭제해야한다.(answer start_idx도 조정 필요)
  - 평가지표 : F1, exact match(EM), accuracy(KorQuAD 1.0에서 요구하는 평가지표 : EM, F1)
   

### [음성분류](https://github.com/ttogle918/AI_practice/tree/main/dacon_%EC%9D%8C%EC%84%B1_%EB%B6%84%EB%A5%98_%EA%B2%BD%EC%A7%84%EB%8C%80%ED%9A%8C)

목적 : 음성 데이터를 다루는 방법 알아보기

0-1. [샘플코드 : data 분석](https://github.com/ttogle918/AI_practice/blob/main/dacon_%EC%9D%8C%EC%84%B1_%EB%B6%84%EB%A5%98_%EA%B2%BD%EC%A7%84%EB%8C%80%ED%9A%8C/data_%EB%B6%84%EC%84%9D.ipynb)
  - 퓨리에 변환
  - Mel Spectrogram
  
0-2. [샘플코드 : baseline - randomforest](https://github.com/ttogle918/AI_practice/blob/main/dacon_%EC%9D%8C%EC%84%B1_%EB%B6%84%EB%A5%98_%EA%B2%BD%EC%A7%84%EB%8C%80%ED%9A%8C/baseline_randomforest.ipynb)
  - 0부터 9까지 음성 분류
  - dacon의 샘플 코드

1. [모델 : cnn2d](https://github.com/ttogle918/AI_practice/blob/main/dacon_%EC%9D%8C%EC%84%B1_%EB%B6%84%EB%A5%98_%EA%B2%BD%EC%A7%84%EB%8C%80%ED%9A%8C/cnn2d.ipynb)
  - dacon의 샘플 코드를 바탕으로 모델을 변형하여 적용
  - test 정확도 : 0.98 
