---

title: "Rule induction"
excerpt: "Rule induction에 대한 이론과 rapid miner를 이용한 실습"
last_modified_at: 2020-08-15T10:27:01-05:00
categories:
  - data_mining_course
use_math : true

---
앞의 decision tree와는 다르게, 특정 class label에 부합하기 위한 attribute 선행 조건들을 and로 묶은 rule set을 정합니다.
그리고 예측하고자 하는 example의 class label을 rule set을 통해 label을 판별하는 모델입니다.
<br>
<br>
예를 들어, 롤 유저들의 티어를 예측하는 rule set을 만든다면,
<br>
<div style="border:2px solid; max-width: 500px;">
(맵을 보는가 = No) $\wedge$ (플레이시 비속어 횟수 > 20) = 브론즈
<br>
(와드 설치 유무 = Yes) $\wedge$ (분당 cs 횟수 > 8) = 플레티넘
</div>
<br>
처럼 표현 할 수 있습니다.

### Definition

Rule i : $(Condition)_{i} \rightarrow$ $ y$ $ _{i}$
<br>
<br>
위와 같은 if...then...else로 이루어진 rule이 집합의 형태로 이루어져 있으며 이를 rule set이라 합니다.
이 rule set에 의해 record의 label을 판별하게 되는데
여기서 해당 rule이 특정 record의 조건에 부합한다면 해당 rule은 그 record를 <strong>cover</strong>한다고 하며, 
반대로 record는 해당 rule을 <strong>trigger</strong> 한다고 말할수도 있습니다.


### 용어설명

Accuracy : $\frac{\|A\|}{\|D\|}$
<br>
전체 데이터 중에서 해당 rule을 trigger하는 record의 비율을 의미

Coverage : $\frac{\|A\cap y\|}{\|A\|}$
<br>
trigger하는 record 중에서 해당 rule set의 label과 같은 record의 비율을 의미

Example)
<table>
	<th>Id</th>
	<th>와드 여부</th>
	<th>맵 활용 여부</th>
	<th>비속어 사용 횟수</th>
	<th>티어</th>
	<tr>
		<td>1</td>
		<td>Yes</td>
		<td>Yes</td>
		<td>2</td>
		<td>플레티넘</td>
	</tr>
	<tr>
		<td>2</td>
		<td>Yes</td>
		<td>No</td>
		<td>5</td>
		<td>브론즈</td>
	</tr>
	<tr>
		<td>3</td>
		<td>Yes</td>
		<td>No</td>
		<td>8</td>
		<td>브론즈</td>
	</tr>
	<tr style="color:red;">
		<td>4</td>
		<td>No</td>
		<td>No</td>
		<td>55</td>
		<td>브론즈</td>
	</tr>
	<tr style="color:red;">
		<td>5</td>
		<td>No</td>
		<td>No</td>
		<td>32</td>
		<td>브론즈</td>
	</tr>
	<tr>
		<td>6</td>
		<td>Yes</td>
		<td>Yes</td>
		<td>12</td>
		<td>플레티넘</td>
	</tr>
	<tr style="color:red;">
		<td>7</td>
		<td>No</td>
		<td>No</td>
		<td>35</td>
		<td>플레티넘</td>
	</tr>
	<tr>
		<td>8</td>
		<td>Yes</td>
		<td>Yes</td>
		<td>10</td>
		<td>플레티넘</td>
	</tr>
	<tr>
		<td>9</td>
		<td>Yes</td>
		<td>Yes</td>
		<td>27</td>
		<td>플레티넘</td>
	</tr>
	<tr>
		<td>10</td>
		<td>No</td>
		<td>Yes</td>
		<td>29</td>
		<td>브론즈</td>
	</tr>
</table>
Rule set : (와드 여부 = No) $\wedge$ (맵 활용 여부 = No) $\wedge$ (비속어 사용 횟수 > 20) = 브론즈
<br>
<br>
Coverage = $\frac{3}{10} = 0.3$
<br>
이 중에서 class label이 브론즈인 record는 2개 이므로,
<br>
<br>
Accuracy = $\frac{2}{3} = 0.6667$
<br>
Mutually exclusive rule set
Exhaustive rule set