# Higher Education Student Retention Prediction

Predicting Dropout Risk & Academic Success Using Machine Learning

학생 중도 탈락 여부 예측

⸻

1. 프로젝트 개요 (Project Overview)

학생의 중도 탈락(dropout) 은 대학 교육 품질·재정 안정성·학생 복지와 직결되는 핵심 문제다.
본 프로젝트는 Kaggle의 Predict students' dropout and academic success 데이터를 활용하여

	•	어떤 학생이 졸업(Graduate) 할지

	•	어떤 학생이 재학 유지(Enrolled) 할지

	•	어떤 학생이 중도탈락(Dropout) 할지

이를 머신러닝으로 예측하는 모델을 개발하는 것이다.

더불어 주요 요인(feature)이 학생의 학업 지속성에 어떤 영향을 미치는지 분석하여

교육정책 및 학생 지원 프로그램 설계에 시사점을 제공하는 것이 목적이다.

⸻

2. 문제 정의 (Problem Statement)

교육기관이 직면한 주요 질문은 다음과 같다:

	•	“어떤 학생이 중도탈락할까?”

	•	“어떤 요인이 학업 지속 여부에 가장 큰 영향을 줄까?”

	•	“위험 학생을 조기에 식별할 수 있을까?”

이를 해결하기 위해 본 프로젝트는 다음을 수행한다:

	1.	학생의 상태(Target) 예측

	•	Dropout / Graduate / Enrolled

	•	→ 다중 분류(Multi-class Classification) 문제

	2.	모델링을 통해 위험 예측 정확도 개선

	3.	Feature Importance & SHAP 분석을 통한 주요 영향 요인 도출

⸻

3. 데이터셋 정보 (Dataset Description)

	•	데이터셋: Higher Education Predictors of Student Retention

	•	출처: Kaggle

	•	행 개수: 약 4,424명

	•	컬럼 수: 35개

⸻

4. Target 변수 정의

데이터의 주요 타깃(Target)은 단일 변수를 통해 정의되며,
학생 상태를 3개의 카테고리로 분류한다:

값	의미
Graduate	졸업
Enrolled	재학 중
Dropout	중도 탈락

→ 따라서 Softmax 기반 다중 분류(Multi-class Classification) 문제로 접근한다.

⸻

5. 주요 변수 목록 (Feature List Summary)

변수들은 크게 5가지 그룹으로 구성된다:

✔ 학생 개인 정보 (Student Information)
	•	Gender
	•	Age at enrollment
	•	Marital_status
	•	Nationality

✔ 가정 경제적 변수(Socioeconomic)
	•	Father_qualification
	•	Mother_qualification
	•	Father_occupation
	•	Mother_occupation
	•	Debtor (등록금 미납 여부)
	•	Scholarship_holder
	•	Tuition_fees_up_to_date

✔ 학업 관련 변수(Academic Performance)
	•	Curricular_units_1st_sem_approved
	•	Curricular_units_1st_sem_grade
	•	Curricular_units_2nd_sem_approved
	•	Curricular_units_2nd_sem_grade
	•	Admission_grade

✔ 생활/상황 변수(Attendance, Lifestyle)
	•	Daytime/evening attendance
	•	Displaced
	•	Educational_special_needs
	•	International

✔ 경제/사회 환경 변수 (Regional Socioeconomic Indicators)
	•	Unemployment_rate
	•	Inflation_rate
	•	GDP

⸻

6. 데이터 전처리 계획 (Data Preprocessing Plan)
	1.	결측치 확인 → 기본적으로 없음
	2.	이상치 탐지 및 제거 (IQR 사용)
	3.	범주형 변수 인코딩 (LabelEncoder / One-Hot Encoding)
	4.	Feature Selection (Chi-square 또는 ANOVA)
	5.	클래스 불균형 해결 (SMOTE Oversampling)
	6.	데이터 표준화/정규화(필요 시)

⸻

7. 모델링 계획 (Modeling Plan)

✔ 적용할 모델

Baseline:
	•	Logistic Regression
	•	Decision Tree

Ensemble Models:
	•	Random Forest
	•	Gradient Boosting
	•	XGBoost
	•	LightGBM
	•	CatBoost (범주형 변수 강점 → 예상 Best Model)

✔ 평가 지표
	•	Accuracy
	•	Precision, Recall, F1-score
	•	Confusion Matrix
	•	ROC-AUC (One-vs-Rest 방식)

⸻

8. 결과 분석 (Interpretation)
	•	Feature Importance
	•	SHAP Value로 개인/전체 수준에서의 요인 영향력 분석
	•	Dropout 고위험군 특성 정의

⸻

9. 기대 효과 (Impact & Insights)
	•	위험 학생 조기 식별 → 개입 정책 수립 가능
	•	장학금·학습 지원 정책의 효과 분석 가능
	•	떨어질 가능성 높은 요소 파악 → 실질적 교육 데이터 기반 의사결정 지원
	•	머신러닝 모델을 통한 교육행정 효율화

⸻

10. 프로젝트 구성 (Repository Structure)

├── README.md  
├── data/  
│   ├── raw/  
│   ├── processed/  
├── notebooks/  
│   ├── 01_EDA.ipynb  
│   ├── 02_Preprocessing.ipynb  
│   ├── 03_Modeling.ipynb  
│   ├── 04_Evaluation.ipynb  
├── models/  
│   ├── best_model.pkl  
├── reports/  
│   ├── EDA_report.md  
│   ├── modeling_summary.md  
├── src/  
│   ├── preprocess.py  
│   ├── train.py  
│   ├── evaluate.py  


⸻