## 1. Object Detection의 정의
- **Object Detection**은 특정 객체(Classification)가 이미지 내에서 어느 위치(Localization)에 있는지를 파악하는 작업이다.
- 모델은 **Object Label**과 **Bounding Box (BBox) 정보**를 제공한다.

## 2. 아이디어 발전
- **Image Classification** 모델을 기반으로 Object Detection 모델로 확장한다.
- **Bbox Prediction Loss**와 **Class Prediction Loss**를 통해 객체의 위치와 클래스를 예측한다.

## 3. Object Detection 모델의 역사
- **R-CNN** 시리즈부터 다양한 모델들이 개발되었다.
- **R-CNN**은 ROI(Region of Interest)를 선택하고 고정된 크기로 변환한 후, CNN 특징을 추출하고 SVM을 통해 분류 및 BBox 회귀를 수행한다.

## 4. Two-Stage Detector
- **Fast R-CNN**은 CNN과 이미지 크기 조정 순서를 변경하여 속도를 개선한다.
- **Faster R-CNN**은 Selective Search 대신 RPN(Region Proposal Network)을 도입하여 더욱 효율적인 객체 후보 영역을 생성한다.
- RPN은 앵커 박스를 사용해 객체가 포함된 영역을 판단하고 BBox 회귀 손실을 통해 중심을 조정 및 크기 변경을 수행한다.

## 5. One-Stage Detector
- **YOLO (You Only Look Once)** 시리즈는 단일 단계로 객체 탐지를 수행한다.
- YOLO v1은 단순하지만 상대적으로 정확도가 떨어지는 단점이 있다.
- **Feature Pyramid Network (FPN)**은 다양한 해상도의 feature map을 쌓아 올리는 구조로, 더 효과적인 다중 스케일 탐지를 가능하게 한다.

## 6. 부록
- **ROI Pooling**은 여러 사이즈의 ROI를 FC Layer에 넣기 위해 크기를 통일하는 역할을 한다. 하지만 Quantization으로 인한 데이터 유실과 Misalignment 문제가 발생할 수 있다.
- **Non-Max Suppression (NMS)**은 높은 점수를 가진 박스를 선택하고 겹치는 영역을 제거하는 방식으로 중복 탐지를 줄인다.
- **IoU (Intersection over Union)**는 두 객체의 박스가 얼마나 겹치는지를 수치로 나타내는 지표로, 0.5 이상의 IoU를 좋은 탐지로 간주한다.
