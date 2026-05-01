# E-Commerce Purchase Prediction

## 프로젝트 개요
Lin(2025) 논문 "Application of machine learning in predicting consumer behavior and precision marketing"을 재현하고 분석한 프로젝트.

이커머스 환경에서 소비자의 구매 여부를 예측하는 4가지 머신러닝 모델을 비교한다.

## 프로젝트 구조
ecommerce-purchase-prediction/
│
├── data/
├── notebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_modeling.ipynb
│   └── 04_visualization.ipynb
├── outputs/
└── README.md

##  데이터셋
- **출처**: UCI Machine Learning Repository
- **데이터**: Online Shoppers Purchasing Intention Dataset
- **크기**: 12,330개 세션, 18개 변수
- **타겟**: Revenue (구매 여부)

##  전처리
- LabelEncoder: 범주형 변수 인코딩 (Month, VisitorType)
- StandardScaler: 수치형 변수 정규화
- IsolationForest: 이상치 제거 (contamination=0.01)
- SMOTE: 클래스 불균형 처리 (0: 10329, 1: 10329)

##  모델 성능 비교

| Model | Precision | Recall | ROC AUC |
|---|---|---|---|
| SVM | 0.942 | 0.941 | 0.974 |
| XGBoost | 0.939 | 0.939 | 0.986 |
| CatBoost | 0.947 | 0.947 | 0.990 |
| BPANN | 0.938 | 0.936 | 0.969 |

## 주요 인사이트
- CatBoost가 ROC AUC 0.990으로 가장 우수한 성능을 보임.
- SMOTE 적용으로 인해 SVM Recall이 논문 대비 크게 개선됨 (0.886 -> 0.941)
- PageValues가 구매 예측에서 가장 중요한 특징
- 11월일 때의 구매율이 가장 높음 (블랙프라이데이 효과)
- 신규 방문자 구매율이 재방문자보다 11% 높음 (25% | 14%)
   ㄴ 구매자 수는 재방문자가 월등히 높기 때문에 재방문자 전환율 개선이 필요함

## 한계점
- SMOTE는 소수 데이터들 사이의 값으로 새 데이터를 "인위적"으로 만들어내는 기법임
=> 현실에 존재하지 않는 데이터가 생길 수 있고, 실제 분포 왜곡 및 노이즈 증폭이 될 수 있음
- 정적 데이터셋을 사용했기 때문에 실시간으로 변하는 소비자 행동 패턴을 반영하지 못함

##  사용 기술
- Python, Pandas, Numpy
- Scikit-learn, XGBoost, CatBoost
- Matplotlib, Seaborn

##  참고 논문
Lin, J. (2025). Application of machine learning in predicting consumer behavior and precision marketing. PLoS One, 20(5).