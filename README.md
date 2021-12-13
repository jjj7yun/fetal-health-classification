# fetal-health-classification
Multi-class classification with imbalanced data
- 태아 건강상태 분류 예측

## description

### 분석개요
2020 년 영아 사망자 수(출생 후 1 년 이내 사망자 수)는 674 명이고,  영아 사망의 주요 원인으로는 ‘출생전/후기에 기원한 특정병태’가 48.5%로 가장 높았다. 영아
사망자 수는 감소하는 추세이지만, 영아 사망률을 줄이기 위한 노력은 계속해서 진행되어야 한다.  그 노력의 첫 단계는 출생 전 태아의 건강상태를 정확히 파악하는 것이라 생각한다. 이상신호를
조기에 감지한다면 적절한 처방을 통해 위험 요인을 제거할 수 있고, 이는 궁극적으로 태아의 사망률을 낮추는 결과를 가져오기 때문이다. 산모가 진행하는 산전 검사 중에는 Cardiotocogram 
검사(CTG)라는 것이 있다. 이는 분만 감시 장치를 통해 태아의 심박수, 태아의 움직임, 자궁 수축 등을 모니터링하는 것이다. 본 과제에서는 이 검사의 결과로 태아의 건강 상태를 예측할 수
있다고 가정하고, Kaggle 에 공유된 태아 CTG 검사 데이터를 활용하여 태아의 건강 상태를분류하는 모델을 만들어보고자 한다. 
해당 데이터셋에는 21 개의 설명변수와 태아의 건강상태를 3 가지로 분류한 타겟변수가 포함되어 있다. 타겟변수의 비율은 1(건강)이 78%, 2(의심)는 14%, 3(병리)은 8%로 불균형하다. 
때문에 모델을 생성하기에 앞서 Undersampling 기법인 ENN 과 Oversampling 기법인 SMOTE 를적용하여 불균형 데이터를 먼저 조정한 후에 분류 모델링을 진행한다. 이후 태아의 건강상태를
예측하기 위한 분류 모델을 생성해보고, 각 모델의 성능과 Feature importance 를 확인해볼것이다. 분류 모델은 Logistic Regression, SVM, Decision Tree Classifier, Random Forest Classifier
4 가지를 사용한다.

### 가정

1. CTG 검사 결과 데이터로 출생 전 태아의 건강 상태를 예측할 수 있다. 생성된 모델이 태아의 건강 상태를 예측하는 데 유효한 모델이라는 것이다. 
  모델의 성능을 검증하는 과정에서 roc_auc_score와 재현율로 확인할 것이다. 
2. 분석 전 태아의 건강 상태를 예측할 수 있는 주요한 변수는 prolongued_decelerations(장기 심장 박동 감속 비율)과 abnormal_short_term_variability(비정상적인 단기 변동성 비율)일 것이라 가정 한다. 
  사전 분석으로 시행한 상관분석에서 타겟변수인 fetal_health(태아의 건강상태)와의 상관계수 가 각각 0.48, 0.47로 가장 높게 나왔기 때문이다. 이는 태아의 건강상태가 좋지 않을수록 이 두
개의 변수 값이 높게 나오는 양의 상관관계가 있다고 해석할 수 있다. 
3. 불균형 데이터를 조정해주면 성능이 향상될 것이라 가정한다.

### Data
Kaggle에 공유된 ‘Fetal Health Classification’ 데이터로, 태아 CTG 검사 결과다. (https://www.kaggle.com/andrewmvd/fetal-health-classification) 데이터는 총 22개의 변
수와 2,126건의 데이터로 이루어져 있다. 
![image](https://user-images.githubusercontent.com/79688191/145770738-fd76e345-2cb2-4887-a039-9f0fffc59d16.png)

### 데이터 전처리
1. Target data 비율 확인
![image](https://user-images.githubusercontent.com/79688191/145770843-e411ecd3-5ac9-4a4a-8d21-a7b6b0daa262.png)

2. 상관관계 분석
![image](https://user-images.githubusercontent.com/79688191/145770867-a580f9d1-092e-4385-8f46-50ba0e147e99.png)



3. Train/Test Set 분리 
![image](https://user-images.githubusercontent.com/79688191/145771111-30689a94-9851-4f88-8f05-bfd802105545.png)


4. Feature / Label 분리
![image](https://user-images.githubusercontent.com/79688191/145771138-d6d78e37-2e06-4672-849c-3959e35ad662.png)

5. 표준화

![image](https://user-images.githubusercontent.com/79688191/145770936-c8e62f24-966d-4914-9e1a-7674508df32e.png)

### Result
1. 불균형 데이터 조정 - SMOTE , ENN 
- Undersampling 기법인 ENN과 Oversampling 기법인 SMOTE를 적용 
![image](https://user-images.githubusercontent.com/79688191/145771161-416ac740-90c3-4397-bff3-335797c14734.png)

- ENN과 SMOTE 복합 방식 적용
![image](https://user-images.githubusercontent.com/79688191/145771172-63ef11cb-8f07-4bac-9f46-8fc1122785a5.png)


2. Logistic Regression


3.SVC


4. Decision Tree classifier


5. Random forest classifier

![image](https://user-images.githubusercontent.com/79688191/145771585-436d77a9-4798-4e1a-a133-c031294e6ea5.png)


결론
1. CTG 검사 데이터의 21개 변수들을 통해 태아 건강상태를 예측할 수 있다.
태아의 심박수, 움직임, 심장박동, 단/장기 변동성, 단/장기의 비정상적인 변동성 비율, 산모의 자궁 수축 등의 변수들로 태아의 건강상태를 예측할 수 있다. 


![image](https://user-images.githubusercontent.com/79688191/145771326-884c2589-20bc-4c0f-b03c-b0ebce1323e1.png)


2. 태아 건강상태에 영향을 주는 주요한 변수는 mean_value_of_short_term_variability 
     (단기 변동성 평균), abnormal_long_term_variability(비정상적인 장기 변동성 비율) 이다![image](https://user-images.githubusercontent.com/79688191/145771416-002852be-4ee4-490b-b601-3a5666322ac0.png)


3. 불균형 데이터를 Oversampling, Undersampling 등의 방법으로 조정하여          
     모델의 성능을 개선할 수 있다. 
![image](https://user-images.githubusercontent.com/79688191/145771429-95a210f4-e47c-4872-99a4-7093da0e8de8.png)

![image](https://user-images.githubusercontent.com/79688191/145771346-c0809cd3-619b-474b-b375-ccafa1707bd0.png)











