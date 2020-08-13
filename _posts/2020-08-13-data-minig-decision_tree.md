---

title: "Decision Tree"
excerpt: "Data Mining에서 supervised learning인 classification에서 decision tree에 대한 이론과 rapid miner를 이용하여 버섯 데이터를 분류 해 봅니다."
last_modified_at: 2020-08-08T11:27:01-05:00
categories:
  - data_mining_course

---

데이터 마이닝에서 supervised learning중 classification인 decision tree model을 이용하여 버섯 데이터를 학습한 뒤 식용 버섯인지 독 버섯인지 예측하여 봅니다.

 


***
## Decision Tree
가령 독버섯에 대한 decision tree 모델에 대해 시각화를 하면 위와 같습니다.


* root node: decision tree의 가장 상단에 있는 노드로서, 들어오는 edge는 없고 0개 이상의 edge(s)를 포함하는 노드 입니다.

* internal node : 정확히 하나의 들어오는 edge와 2개 또는 그 이상의 나가는 edges를 가지고 있습니다. 또한 데이터들이 가지는 특정 attribute에 대해 조건(<strong>condition</strong>)에 따라 나누는(split) 역할을 합니다. 

* leaf or terminal node : 단 하나의 들어오는 edge만 있고 나가는 edge는 없는 노드로서 <strong>class label</strong>을 대표합니다.
