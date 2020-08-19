---

title: "Decision Tree"
excerpt: "Data Mining에서 supervised learning인 classification에서 decision tree에 대한 이론과 rapid miner를 이용하여 버섯 데이터를 분류 해 봅니다."
last_modified_at: 2020-08-08T11:27:01-05:00
categories:
  - data_mining_course
  
use_math: true

---

데이터 마이닝에서 supervised learning중 classification인 decision tree model을 이용하여 버섯 데이터를 학습한 뒤 식용 버섯인지 독 버섯인지 예측하여 봅니다.

 


***
## Decision Tree

가령 독버섯에 대한 decision tree 모델에 대해 예시를 들면 아래와 같습니다.
![decision_tree_example_image1](/image/decision_tree_ex1.jpg)


* root node: decision tree의 가장 상단에 있는 노드로서, 들어오는 edge는 없고 0개 이상의 edge(s)를 포함하는 노드 입니다.

* internal node : 정확히 하나의 들어오는 edge와 2개 또는 그 이상의 나가는 edges를 가지고 있습니다. 또한 데이터들이 가지는 특정 attribute에 대해 조건(<strong>condition</strong>)에 따라 나누는(split) 역할을 합니다. 

* leaf or terminal node : 단 하나의 들어오는 edge만 있고 나가는 edge는 없는 노드로서 <strong>class label</strong>을 대표합니다.

최적의 split attribute condition을 찾기 위한 attribute test condition방법에서 impurity가 사용됩니다.
특정 노드 t의 impurity값은
1. [$GINI(t) = 1 - \sum_{j}[P(j\|t)]^{2}$](#gini)

2. [$Entropy(t) = -\sum_{j}P(j\|t)\log{_{2}P(j\|t)}$](#entropy)

3. [$Error(t) = 1 - max_{j}P(j\|t)$](#error)

위 impurity 값이 최소가 되는 방향으로, 
또는 GAIN값이 최대가 되는 방향으로 split condition을 정하게 됩니다.

---



<div id="gini"></div>
## GINI index
CART, SLIQ, SPRINT 알고리즘에서 사용되며, impurity와 k개의 분할에 대한 Gini index에 가중치가 적용된 Gini split은 각각 아래와 같습니다.

#### $GINI(t) = 1 - \sum_{j}[P(j\|t)]^{2}$

#### $GINI_{split} =  \sum_{i = 1}^{k}\frac{n_{i}}{n}GINI(i)$

Example)

![결정트리예시사진2](/image/decision_tree_ex2.jpg)


왼쪽 leaf node를 t1, 오른쪽 leaf node를 t2라 하면,

<div style="border:2px solid; max-width: 500px;">
$GINI(t1) = 1 - ( (\frac{9}{11})^2 + (\frac{2}{11})^2) = 0.297$
<br>
$GINI(t2) = 1 - ( (\frac{3}{9})^2 + (\frac{6}{9})^2) = 0.444$
<br>
<br>
$GINI_{split} = \frac{11}{20} \times 0.297 + \frac{9}{20} \times 0.444 = 0.363$
<br>
</div>
<br>

<div id="entropy"></div>

***

## Entropy
ID3, C4.5 알고리즘에서 사용되며, impurity와 Gain split 값은 아래와 같습니다. 

#### $Entropy(t) = -\sum_{j}P(j\|t)\log{_{2}P(j\|t)}$

#### $GAIN_{split} = Entropy(p) -(\sum_{i = 1}^{k}\frac{n_{i}}{n}Entropy(i))$
###### ( Entropy(p) : before split )

#### Entropy가 가지는 의미

Example)

![결정트리예시사진2](/image/decision_tree_ex2.jpg)


왼쪽 leaf node를 t1, 오른쪽 leaf node를 t2라 하면,

<div style="border:2px solid; max-width: 500px;">
$Entropy(t1) = - (\frac{9}{11}log_{2}\frac{9}{11} + \frac{2}{11}log_{2}\frac{2}{11} ) = 0.684$
<br>
$Entropy(t2) = - (\frac{3}{9}log_{2}\frac{3}{9} + \frac{6}{9}log_{2}\frac{6}{9}) = 0.918$
<br>
<br>
$Entropy(p) = - (\frac{12}{20}log_{2}\frac{12}{20} + \frac{8}{20}log_{2}\frac{8}{20} ) = 0.971$
$Gain_{split} = 0.971 - (\frac{11}{20} \times 0.684 + \frac{9}{20} \times 0.918) = 0.1817$
<br>
</div>
<br>


<div id="error"></div>

***

## Misclassification Error

#### $Error(t) = 1 - max_{j}P(j\|t)$

Example)

![결정트리예시사진2](/image/decision_tree_ex2.jpg)


왼쪽 leaf node를 t1, 오른쪽 leaf node를 t2라 하면,

<div style="border:2px solid; max-width: 700px;">
$Error(t1) = classification Error(t1) = 1 - max( \frac{9}{11}, \frac{2}{11}) = 1 - \frac{9}{11} = 0.1818$
<br>
$Error(t2) = classification Error(t1) = 1 - max( \frac{3}{9}, \frac{6}{9}) = 1 - \frac{6}{9} = 0.333$
<br>
<br>
$Error(Split) = \frac{11}{20} \times 0.182 + \frac{9}{20} \times 0.333 = 0.250$

</div>
<br>

***

문제는 이러한 impurity 값을 작게 하기 위해 최대한 split 가지수를 많이 늘릴수도 있습니다. 가령, 극단적인 예시의 경우 데이터에서 각각의 record가 고유한 id를 가질 때 
split condition으로 id에 대해 record개수 만큼 split을 하게 된다면 impurity값은 작아지겠지만 우리가 얻고자 하는 유의미한 모델은 아니게 됩니다. 따라서 이러한
split에 대해 제약을 주기 위해 SplitINFO가 사용 됩니다.

#### $SplitINFO = -\sum_{i = 1}^{k}\frac{n_{i}}{n}log\frac{n_{i}}{n}$

따라서 split에 대한 제약이 적용된 gain은

#### $GainRATIO_{split} = \frac{GAIN_{split}}{SplitINFO}$

Example)GINI index 예제에 splitINFO를 적용하면,

<div style="border:2px solid; max-width: 500px;">
$ SplitINFO = - ( \frac{11}{20}log_{2}\frac{11}{20} + \frac{9}{20}log_{2}\frac{9}{20} ) = $
<br>
$ GAIN_{split} = 1 - ()나누기전 $
<br>
$ GainRATIO_{split} = \frac{}{}$
</div>
<br>


![결정트리예시사진2](/image/test.jpg)
