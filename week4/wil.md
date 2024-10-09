## 4주차 WIL   
3주차에서 배운 Weight matrix 값을 정하기 위해서 Loss Function을 활용할 수 있다.   
Loss Function을 통해 현재 Weight Matrix의 예측과 실제 정답 간의 차이(오차의 정도)를 수치화 한다.   
이 결과를 바탕으로 Weight Matrix 값을 업데이트하고 Loss를 최소화하여 분류 정확도를 최대화한다.   
   
이 때 문제의 특성과 데이터 유형에 따라 적합한 Loss Function을 선택하여야 한다.   
- 회귀 문제   
   - MSE : Mean Squared Error   
   
- 분류 문제   
    - SVM Loss : Support Vector Machine에서 사용하는 hinge loss
    - Cross-Entropy Loss


                     
SVM은 허용가능한 오류 범위 내에서 최대 margin을 만드는 것을 목표로 한다.


Cross-Entropy Loss는 네트워크 출력을 확률로 해석하고 싶을 때 사용하며 출력을 의미있는 확률 분포로 변환한다.   
이 때 잘한 예측에는 작은 페널티를, 잘못된 예측에는 큰 페널티를 부과한다.   
SVM보다 Cross-Entropy Loss가 확률 분포의 차이에 더 민감하게 반응한다.   


Regularization은 모델의 복잡도를 제어하고 과적합(Overfitting)을 방지하는 기법이다.   
Loss함수에 parameter에 대한 term을 추가하여 적용하며 가중치 w가 작아지도록 학습시켜 Local noise에 영향을 덜 받도록 한다.    

- L2 Regularization은 매끄러운 그래프를 원할 때 쓰는 정규화 기법이다.   
큰 가중치에 더 큰 페널티를 부과하고, 극단적인 가중치를 피하며, 모든 특성이 적당히 기여하도록 유도한다.   
- L1 Regularization은 분류기가 복잡하다고 느껴질 떄 쓰는 정규화로 가중치값에 0이 많도록 하여 보다 더 단순한 식을 만들어준다.   

Optimization(최적화)은 Loss Function이 줄어들도록 조정하는 방법이다.    
가장 빠르게 손실함수가 줄어드는 방향으로 최소지점으로 가는 것을 목표로 한다.   
Local minimum(Vanilla Gradient Descent)를 해결하기 위해 여러 방법을 도입하기도 한다.   
- Momentum(관성) : 이전 단계의 업데이트 방향을 고려하여 현재 업데이트에 반영한다.   
- Adative Learning rate : 과거의 그래디언트 정보를 할용하여 각 파라미터마다 서로 다른 학습률을 사용한다. 