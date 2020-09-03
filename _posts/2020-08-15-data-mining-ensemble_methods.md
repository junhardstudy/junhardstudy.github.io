---

title: "Ensemble methods"
excerpt: "Ensemble methods에 대한 이론과 rapid miner를 이용한 실습"
last_modified_at: 2020-08-15T10:27:01-05:00
categories:
  - data_mining_course
use_math: true
---

여러 개의 weak base model들을 생성하고, 그 output들을 하나로 취합하여 하나의 output을 만드는 strong model 생성 방법 
![앙상블 매서드 사진]()
<br>
### Ensemble modeling에서 중요 요구 사항

1. base model들은 서로 서로에 대해 independent 해야 함.

2. 각각의 model들은 binary classification을 할 때, <strong>잘 못 분류하는 error rate가 50% 보다는 반드시 작아야 함</strong>.
<br>
<br>
<hr>

### Approaches for constructing ensemble modeling

1). 각각의 base model에 대해, training data set을 바꾸기.

  * original data로부터 resempling을 거쳐 여러 개의 training set을 생성.
  
  * bagging, boosting등이 있음.

2). 각각의 base model에 대해, input attribute들을 바꾸기.

  * 각각의 training set을 형성할 때, 서로 다른 input attribute set이 선택됨.
  
  * training data가 많은 수의 attribute를 가졌을 때, 사용하기 좋음.
  
  * random forest가 있음.

3). 각각의 base model을 생성할 때, 서로 다른 model algorithm을 적용.

  * 단, training data set은 똑같음.

4). 각각의 base model에 대해, 서로 다른 parameter를 사용.
<br>
<br>
<hr>

### Bagging

* Bootstrap aggregation이라고 함.

* original data set으로부터, 무작위 복원 추출(random sampling with replacement)을 반복 시행.

* 이렇게 생성된 subset data를 bootstrap sample이라함.

* 각각의 bootstrap sample에 의해 classifier 생성.

* class 예측을 위해 vote 방식 사용.