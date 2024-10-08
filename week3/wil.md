## 2주차 WIL   
이미지 분류란 컴퓨터가 주어진 이미지를 보고 이미지가 어떤 카테고리에 속하는지 판단하는 작업이다.   
이미지 분류는 다 지도학습일 거라는 오해를 할 수 있지만 앞서 배운 지도학습, 비지도학습, 반지도학습의 방법을 통해 이미지 분류라는 목표를 달성할 수 있다.   
디지털 이미지는 픽셀, 채널(RGB), 해상도 등의 구조로 이루어져 있다.   
컴퓨터는 이미지를 숫자의 배열 즉 행렬로 인식하기 때문에 우리는 컴퓨터에게 이미지를 행렬로 나타내서 제시해주어야 한다.   
이미지 분류 접근 방식에는 여러가지가 있다. 가장 원시적인 방법부터 발전된 방법으로 나아가보자.   
RAW-pixel 방식은 모든 이미지를 같은 크기로 맞추고 1차원 벡터로 펼친 후 벡터 간 거리를 계산하는 방식으로 가장 원시적인 방식이고 효율이 좋지 못하다. 이 방식으로는 픽셀간의 상대적인 위치 등의 정보를 반영하지 못한다.   
선형분류기 방식은 가중치와 편향값을 이용하는 방식이다. 훈련 데이터에 대한 지식을 요약해 가중치에 집어넣는다. 다만 이 방식을 하나만 이용하면 템플릿이 하나로만 요약되기에 다양한 블록을 쌓아야 한다.   
위의 2가지 기본적인 이미지 분류 방식은 육안으로는 명확히 구분되지만 픽셀값으로는 큰 차이가 나지 않는 이미지, 시점이 다른 이미지, 가려진 이미지 등을 잘 분류할 수 없다.    
이렇듯 입력 데이터를 1차원으로 펼쳐서 처리하는 방식을 FNN 방식이라고 한다. FNN방식에서는 인접 픽셀 간의 상관관계가 무시되어 정보손실이 발생한다.   
이러한 문제를 해결하기 위해 등장한 방식이 CNN(합성곱 신경망)이다.   
CNN은 Convolutional Layer, Pooling Layer, Fully Connected Layer로 구성된다.   
Convolutional Layer는 입력 이미지에 다양한 필터를 적용해 특징을 추출한다. 이 때 각 필터는 특정 패턴을 감지하도록 학습한다.   
Pooling Layer는 Feature map의 크기를 줄이면서도 특정 영역에서 가장 강한 특징이나 평균값 등을 선택하는 기법이다. 이 기법의 장점은 크기를 줄여 계산량을 줄이면서도 가장 강한 특징만을 선택하기에 약간의 위치 변화의 내성을 가지게 된다는 것이다.   
마지막으로 이전 층의 모든 뉴런과 연결되어 추출된 특징들을 종합하여 최종 분류를 수행하는 Fully Connected Layer기법이 있다. 다시 데이터를 flatten시키면 공간 정보를 유지한 소용이 없다고 생각할 수 있지만 이미 Feature map들이 이미지의 다양한 고수준 특징을 나타내고 있기 때문에 그러한 걱정을 하지 않아도 좋다.