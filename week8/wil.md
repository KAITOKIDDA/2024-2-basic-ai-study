# 강의 내용

## 1. Definition

### Object Detection이란?

- **목적**: 이미지 내 특정 객체의 **분류(Classification)**와 **위치(Localization)**를 파악하는 AI Task
- **결과물**:
  - **Object Label**: 객체의 종류
  - **BBox Info**: 객체 위치를 나타내는 경계 상자 정보 (중심 좌표 x, y와 크기 width, height)

---

## 2. Ideation

### Object Detection은 Image Classification의 확장

1. **기존 이미지 분류 모델의 한계**:
   - 이미지를 하나의 레이블로만 분류 (객체 위치 정보 제공 불가)
2. **목표**:
   - 이미지 분류 모델을 확장하여, 객체를 **BBox**(Bounding Box)로 잘라내고 레이블과 위치를 예측

### Object Detection 모델의 구성 요소

- **BBox Prediction Loss**: 객체 위치를 예측하는 손실 함수
- **Class Predict Loss**: 객체의 분류를 예측하는 손실 함수

---

## 3. Object Detection Model History

- 객체 탐지 모델의 발전 과정:
  1. Region Proposal 기반 모델 (Two-Stage Detectors)
  2. End-to-End 방식의 모델 (One-Stage Detectors)
  3. Feature Map 기반 네트워크 설계

---

## 4. Two-Stage Detector

### 주요 모델

1. **R-CNN (Region-based CNN)**:

   - **프로세스**:
     1. **Selective Search**를 통해 ROI(Region of Interest)를 뽑아냄
     2. ROI 크기를 고정된 크기로 변환 (Warping)
     3. CNN으로 특징 추출 후, SVM으로 분류와 BBox Regression 수행
   - **단점**:
     - ROI당 CNN 연산 수행 → 연산량 과다 (ROI 2000개당 CNN 2000번 실행)

2. **Fast R-CNN**:

   - **개선점**:
     1. ConvNet 연산 순서를 변경해 속도 개선
     2. SVM 대신 Linear Classification 사용
   - **ROI Pooling**:
     - Feature Map에서 ROI 크기를 고정하여 효율적으로 처리
     - Quantization에 의한 정보 손실 및 Misalignment 문제 발생 가능

3. **Faster R-CNN**:
   - Selective Search 제거, **RPN (Region Proposal Network)** 도입
   - **RPN 역할**:
     1. Anchor Box를 통해 객체 포함 여부 판단 (Binary Classification)
     2. 객체의 위치를 조정하고 크기를 조정 (BBox Regression)
     3. 결과를 NMS로 처리해 중복 제거 및 Top-N Proposal Region 생성
   - **장점**:
     - Region Proposal 단계부터 End-to-End 학습 가능

---

### Appendix: ROI Pooling

- **목적**: 다양한 크기의 ROI를 동일한 크기로 변환
- **과정**:
  1. ROI를 픽셀 단위로 분할
  2. 각 분할에서 최대값(Max Pooling) 추출
  3. 고정 크기의 Feature Map 생성
- **문제점**:
  - 픽셀 간 정렬(Misalignment) 문제가 발생할 수 있음
  - 원본 정보 손실 가능성 존재

### Appendix: NMS (Non-Max Suppression)

- **과정**:
  1. 가장 높은 Score를 가진 BBox 선택
  2. 나머지 BBox와의 IoU 비교
  3. IoU가 Threshold 이상인 박스 제거
  4. 반복
- **문제점**:
  - 겹쳐있는 객체들에 대해 좋은 BBox를 제거하는 경우 발생 가능

### Appendix: IoU (Intersection over Union)

- **정의**: 두 BBox의 교집합 면적과 합집합 면적 비율
- **평가 기준**:
  - IoU > 0.5: Decent
  - IoU > 0.7: Pretty Good
  - IoU > 0.9: Almost Perfect

---

## 5. One-Stage Detector

### YOLO (You Only Look Once)

- **특징**:
  1. 전체 이미지에서 한 번의 연산으로 객체를 탐지
  2. 속도가 빠르고 구현이 단순함
  3. 모델이 여러 위치에서 다른 클래스 예측 가능
- **YOLO v1 단점**:
  - Bounding Box Regression의 정확도가 낮고, 객체 크기가 다양할 때 탐지 성능이 저하됨
- **YOLO 발전**:
  - Pyramid Feature Map 등 다양한 해상도 정보 사용해 성능 개선

---

## 6. Feature Map Architecture

### Feature Pyramid Network (FPN)

- **구조**:
  - Convolutional Network에서 서로 다른 해상도의 Feature Map을 계층적으로 결합한 피라미드 형태
- **장점**:
  - 다양한 해상도에서 유용한 정보 결합 가능
  - 작은 객체부터 큰 객체까지 탐지가 용이

# 논문 리뷰

## 🚀 **Transformer - Attention is All You Need**

딥러닝 자연어 처리(NLP) 분야에서 획기적인 모델인 **Transformer**에 대한 내용을 다룬다.  
2017년 "Attention is All You Need" 논문에서 소개된 모델로, 기존 RNN 기반 모델들의 한계를 극복하며 NLP 기술 발전에 기여함

---

## 📘 **What I Learned**

## 1. **Transformer란?**

Transformer는 **순차적 처리의 한계를 극복**하기 위해 설계된 딥러닝 모델
기존 RNN(LSTM, GRU) 계열 모델은 시퀀스를 순차적으로 처리하기 때문에 병렬화가 어려웠으나, Transformer는 병렬 처리가 가능하여 학습 속도와 성능이 대폭 개선됨

---

## 2. **주요 구성 요소**

Transformer는 **인코더(Encoder)**와 **디코더(Decoder)**로 구성된 모델

## (1) **인코더**

- 입력 데이터를 처리하는 6개의 레이어로 구성
- 각 레이어는 다음의 두 가지 서브 레이어로 이루어짐:
  1. **멀티헤드 셀프 어텐션(Multi-Head Self-Attention)**
     - 입력 시퀀스의 모든 위치 간의 관계를 학습.
  2. **피드포워드 네트워크(Feedforward Network)**
     - 어텐션 결과를 더욱 정교하게 처리.
- **잔차 연결(Residual Connection)**과 **레이어 정규화(Layer Normalization)**로 학습 안정성 향상.

## (2) **디코더**

- 6개의 레이어로 구성.
- 인코더 출력 활용을 위한 **인코더-디코더 어텐션** 추가.
- **마스킹된 셀프 어텐션(Masked Self-Attention)**:
  - 디코더가 미래의 단어를 보지 못하도록 마스킹 처리.
  - 오토레그레시브(Autoregressive) 특성 유지.

---

## 3. **어텐션 메커니즘**

Transformer의 핵심은 **어텐션 메커니즘**

- 모든 입력 토큰 간의 상호작용을 모델링해 **전역 정보를 학습**.
- RNN처럼 순차적으로 처리하지 않아 **병렬 연산 가능**.

---

## 4. **Transformer의 영향**

Transformer는 NLP 분야의 다양한 응용에 혁신을 가져왔다

- 대표적인 모델:
  - **BERT**: 사전 학습을 통한 문맥 이해 강화.
  - **GPT**: 자연스러운 텍스트 생성.
- 활용 사례:
  - 기계 번역
  - 텍스트 요약
  - 질문 응답 시스템
  - 대화형 AI

---

## 💡 **Key**

- Transformer는 병렬 처리를 통해 학습 효율과 성능을 크게 개선.
- 어텐션 메커니즘은 NLP 모델의 성능을 혁신적으로 향상.
- 이 모델의 도입으로 NLP 응용 분야가 급격히 발전.

---
