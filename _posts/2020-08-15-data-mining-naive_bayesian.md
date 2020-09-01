---

title: "Naive Bayesian"
excerpt: "Naive Bayesian에 대한 이론과 rapid miner를 이용한 실습"
last_modified_at: 2020-08-15T10:27:01-05:00
categories:
  - data_mining_course
use_math : true

---

* 통계와 확률에 기반

* 많은 적용 사례에서, attribute set과 class variable사이의 상관 관계는 <strong>non-deterministic</strong>함.
<br>
&nbsp;&nbsp;->why?) noise data나 data set에는 포함되지 않지만 분류하는데 영향을 주는 다른 요소에 의해, 어떤 test example의 attribute set이
	training example의 attribute set과 동일하다고 해서 확정저긍로 똑같은 class labelss로 분류가 안될 수 있음.
	
<br>
결론적으로, <strong>attribute set과 class variable사이의 modeling probablistic relationship를 ananlysis하기 위한 적근 방법</strong>

> 예를 들어, 경대 캠퍼스를 지나가다 아무나 조사했을 때, it대 소속 학부생일 확률이 20%라고 가정. 여기서 '손에 선형 대수책을 들고 있다' 거나, '돌아다니는 경로가 정문쪽이다' 와 
> 같은 추가적인 정보는 이 학생이 it대 소속일 확률을 점점 높여줌. 즉, 결과에 영향을 주는 통계 확률이론에 기반해 결과를 추측하는 것.

<br>
<hr>
### Notations and terminologies

X : the evidence, factors, or attribute set.
<br> 
주의)Not individual attribute.
<br>
<br>
Y : the outcome, taget, or class label.
<br>
<br>
P(Y) : prior probability.
<br>
 * 주어진 data set에서 해당 outcome의  발생빈도.
 * data set으로부터 구할 수 있음.
<br>
<br>

P(Y\|X) : the conditional probability.
 * 조건부 확률로서, evidence X가 일어났을 때 outcome Y일 확률.
 * posterior probability라고도 불림.
<br>
<br>
<hr>
### Conditional probability 

->Bayes Theorem을 이용하여 계산

