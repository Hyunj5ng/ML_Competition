# ML_Competition
ML in 2021-1 semester

각 file에 대한 설명
1) 컴피티션 당시 2등팀의 코드를 참고한 feature engineering 파일
2) 우리 팀이 직접 진행한 feature engineering 파일
3) SHAP 알고리즘을 활용한 feature selection 파일
4) 2등팀 + 우리가 수행한 modeling 파일
5) 교수님께서 제공해주신 PyCaret Modeling 파일
6) Scoring을 위한 산술평균 앙상블 파일

Machine Learning Competition은 총 2라운드로 진행하였고, 첫번째 라운드가 끝나고 상위 1-3등팀의 소스코드를 공개하여, 참고하도록 대회가 진행되었다.

1. 1라운드 2등팀의 feature engineering 코드리뷰
- 1라운드의 결과가 좋지 않았기 때문에, 단순히 우리팀의 힘으로만으로는 부족하다고 판단하여 상위팀 중 한 팀의 코드를 Line by line 으로 리뷰를 하기로 결정.
- 먼저 각 feature 별로 어떻게 column making을 해야 했는지 리뷰를 통해 학습했다.
- 예를 들면 goodcd 같은 경우 처음에 우리는 1만여개의 goodcd 종류를 모두 one-hot encoding을 시도했으나 메모리 문제가 발생하여 난항을 겪었다. 따라서 2등팀이 시도한 방법을 채택하였다.
  -> 랜덤하게 goodcd의 unique한 관측치를 선택하고, word2vec 알고리즘을 사용하여 가장 의미있는      goodcd가 무엇인지 찾아서 100개로 추려내는 작업을 했다.

2. PyCaret 이용
- PyCaret 소개. 작년 즈음에 출시된, 머신러닝의 workflow를 간단하게 조작할 수 있는 파이썬 라이브러리이다. 전체적인 메소드를 부르는 방식은 기존의 라이브러리와는 다르지만 큰 흐름으로 봤을 떄는 오히려 통일성있게 코딩을 할 수 있다. https://pycaret.org/ 
- 교수님께서 올려주신 코드를 그대로 제출했지만 안타깝게도 baseline을 넘지는 못했다. 왜? 1,2,3등팀의 feature들을 각각 모델링하고 따로 제출을 했기 때문이다.

3. SHAP 사용
- feature selection을 할때, SHAP 알고리즘 사용. 
- SHAP 에 대한 간략한 소개  https://github.com/slundberg/shap 
- 기존의 Ridge 회귀를 이용한 feature selection을 진행을 하고나서 다시 SHAP을 이용하여 selection을 진행하였다.
- 사용한 feature 데이터는 크게 3개였다.
	1) 1등팀 features
	2) 3등팀 features
	3) 2등팀 features + 우리 팀이 분석한 features
- 위 세개의 feature들을 기존의 Ridge 회귀로 selection을 진행하고 다시 SHAP으로 selection 했음.
- 각각을 모두 모델링 노트북 (LGBM + CatBoost + Ridge + DNN을 앙상블 한 모델을 작성한 파이썬노트북 파일)으로 돌려서 제출파일을 생성했다. 즉 제출파일 3개가 나오게 되었다.
- 결과로 나온 3개의 제출파일을 산술평균 앙상블 시도.

4. 마지막 scoring 시도
- PyCaret을 사용한 제출파일 3개 averaging
- 모델링 노트북을 사용한 제출파일 averaging
- 베이스라인 제출파일 averaging
- 위 3개를 averaging (최고점수)
