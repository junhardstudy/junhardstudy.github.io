---

title: "K-NN"
excerpt: "K-NN에 대한 이론과 rapid miner를 이용한 실습"
last_modified_at: 2020-08-15T10:27:01-05:00
categories:
  - data_mining_course
use_math : true
---

예측하고자 하는 test record와 가장 가까운 k개의 training record들을 찾아 class label을 판별하는 분류 입니다.
<br>
따라서 record(instance)들을 기반으로 단순히 모델을 만드는 것이 아니므로 instance-Based classifiers 
또는 Lazy-Learner 라고도 합니다.
<br>
<br>

### Definition

K개의 <strong>가장 가까운(closest)</strong> training record들을 찾아 해당 k개의 training record들의 class label에 따라 
unseen data의 label을 분류, 예측.
<br>

![예시사진]()
<br>

<hr>
모든 record들은 n차원의 공간에서 하나의 점으로 표현할 수 있습니다. 여기서 n은 해당 data의 attribute의 개수를 뜻 합니다.
<br>
### K개 가지는 의미
<br>
고려되어지는 가장 가까운 training record의 <strong>개수</strong>
<br>
* k = 1일 때, 가장 가까운 하나의 training record의 class label을 채택. 하지만 그 training data가 outlier data여서 잘못 분류, 예측을 하게 될 수도 있음. 따라서 K를 2개 이상 선택
* K > 1일 때, voting에 의해 결정하며 보통 동점(tie)이 나오는 상황을 방지하고자 K는 홀 수를 사용.

### Measures of proximity

K-NN 알고리즘의 핵심은 test record와 가장 가까운 training record 사이에 <strong>거리를 측정하는 것</strong>

#### Matrics for measures of proximity
* Distance

* Correlation

* Similarity
  * Simple matching coefficient
  * Jaccard similarity
  * Cosine similarity
  
#### Distance

n차원에서 두 점 사이의 거리
<br>
각 attribute사이에서 단위가 다를 수 있으므로, 그런 경우 <strong>Normalization</strong>이 필요함

1. Range transformation : 값이 0 ~ 1 사이의 값을 가지도록 함.
$ X_{normalized} = {X-min(X)}/max(X)$

2. Z-transformation : 모든 attribute들이 평균이 0이고 표준 편차가 1인 값을 가지도록 rescale.
$ X_{normalized} = {X - mean(X)}/std(X)$

이 외에도 Manhatten/Chebyshev distance가 있음.
1. Manhatten : 각각의 attribute의 차의 절댓값을 더한 것.

2. Chebyshev : 각각의 attributed의 차이 중에서 최댓(max)값.

#### Correlation

#### Similarity

<hr>

### K-NN에서 class label 결정하기

K개의 개수에 따라 class label을 선택할 때 voting을 사용할 수 있음
<br>
voting은 다음과 같이 적용 됨.
<br>

1. Majority vote을 사용. 즉, K개의 가까운 것들 중에서 다수의 class labels를 채택

2. 거리에 따른 weighted vote을 사용. 즉, 먼 거리일수록 voting에 영향을 적게 받도록 함. 