# 주제
고등학생 성적 등급(GradeClass) 예측 및 성과 개선 인사이트 도출:
- 목표: GradeClass(0:A … 4:F)를 높은 정확도로 예측하고, 성적 개선에 가장 영향을 주는 요인과 개입 시나리오를 제시한다.

# 배경 및 데이터
- 출처: Kaggle “Students Performance Dataset”
- 표본: 2,392명
- 주요 변수: Age(15–18), Gender(0/1), Ethnicity(0–3), ParentalEducation(0–4), StudyTimeWeekly(0–20h), Absences(0–30), Tutoring(0/1), ParentalSupport(0–4), Extracurricular/Sports/Music/Volunteering(0/1), GPA(2.0–4.0), GradeClass(0–4)

# 연구 질문
1) 성적 등급 예측: 어떤 학생이 F(4) 또는 D(3)로 갈 확률이 높은가?
2) 개선 포인트: 주당 학습시간 증가, 결석 감소, 튜터링/부모지원 등 각 개입이 예측 확률에 어떤 변화를 주는가?
3) 공정성: 성별/민족 등 민감 특성이 예측 및 추천에 불합리한 영향을 주는가?

# 성공 지표(평가)
- 분류 성능: Macro F1, Balanced Accuracy, ROC-AUC(One-vs-Rest)
- 운영 지표: Recall@Risk(하위 등급(D/F) 탐지 재현율), Precision@Risk
- 해석 가능성: 글로벌/로컬 특성 기여(SHAP), 반사실 시나리오의 설득력
- 공정성: 그룹별 성능 차이(ΔF1, ΔTPR), Demographic Parity 간단 점검

# 방법론
1) EDA
- 분포/상관: GPA와 StudyTimeWeekly, Absences의 관계, ParentalSupport의 단계 효과
- 클래스 불균형 확인 및 리샘플링/가중치 전략 검토

2) 전처리
- 결측/이상치 처리
- 범주형 인코딩: One-Hot(민족, 부모교육 등)
- 스케일링: 수치형(학습시간, 결석)
- 데이터 분할: Train/Valid/Test = 70/15/15, 계층화(Stratified)

3) 베이스라인
- 로지스틱 회귀(클래스 가중치 포함)
- 트리 기반: Random Forest, XGBoost/LightGBM

4) 고도화
- 비용민감 학습: D/F 오분류 패널티 상향(클래스 가중치)
- 교차검증: Stratified K-Fold(5)
- 하이퍼파라미터 탐색: Optuna
- 캘리브레이션: Platt/Isotonic으로 확률 보정

5) 해석·인사이트
- 글로벌 중요도: SHAP feature importance
- 로컬 설명: 위험 학생별 SHAP waterfall
- 반사실(What-if): 학습시간 +2h, 결석 −3회, 튜터링=1, 부모지원 +1단계 적용 시 예측 변화
- 정책 시뮬레이션: 예산 제약 하에서 최대 성과 향상 조합(간단한 그리디/휴리스틱)

6) 공정성 점검
- 성별/민족 그룹별 성능 비교
- 필요한 경우 민감 변수 제외/제약 학습으로 영향 완화

# 산출물(Deliverables)
- 보고서: EDA → 모델링 → 성능 → 해석 → 반사실 시나리오 → 공정성
- 대시보드: 위험 학생 탐지, 추천 개입 포인트, What-if 슬라이더(학습시간/결석/튜터링/부모지원)
- 코드: 재현 가능한 파이프라인(전처리/학습/해석)
- 모형 카드(Model Card): 데이터/가정/한계/공정성/배포시 고려사항

# 일정(2주)
- 1주차
  - D1–D2: EDA/전처리 파이프라인
  - D3–D4: 베이스라인/교차검증
  - D5: 캘리브레이션/초기 SHAP/초기 보고서
- 2주차
  - D6–D7: 하이퍼튜닝/비용민감 최적화
  - D8: 반사실/정책 시뮬레이션/공정성 점검
  - D9–D10: 대시보드/최종 보고서/모형 카드

# 기술 스택
- Python: Pandas, scikit-learn, LightGBM/XGBoost
- 해석: SHAP
- 실험 관리: Optuna
- 시각화/대시보드: Plotly/Streamlit

# 위험·한계
- 합성 데이터: 실제 학교 적용 전, 외부 검증 필요
- 민감 변수: 성별/민족 사용의 윤리·법적 고려
- 인과 추론 한계: 반사실은 시뮬레이션일 뿐, 실제 개입 효과 검증 필요

# 기대 효과
- 운영 측면: D/F 위험 학생 조기 탐지로 개입 효율 극대화
- 정책 측면: 가장 영향력 있는 요인(예: 결석 감소, 부모지원 강화)을 근거 기반으로 추천





https://www.kaggle.com/datasets/rabieelkharoua/students-performance-dataset
