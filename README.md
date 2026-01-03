# 🧠 NLP Review Analysis Project  
### Sentiment Classification · Multi-label Classification · ABSA

본 프로젝트는 리뷰 텍스트를 대상으로  
**① 감성 분류 → ② 다중 속성 분류 → ③ 속성 기반 감성 분류(ABSA)** 를  
단계적으로 수행하며, **문제 유형·입력 구조·모델 선택에 따른 성능 차이**를 분석한 NLP 프로젝트입니다.

---

## 📌 Project Overview

### 🎯 목표
- 리뷰 데이터에서 감정과 속성을 **정확히 분리·해석**
- 단계별 NLP 문제 정의 차이에 따른 **모델링 전략 비교**
- 입력 텍스트 구조가 성능에 미치는 영향 분석

---

## 🧩 Project Steps

### Step 1. Sentiment Classification
- **문제 유형**: Binary Classification
- **입력**: 리뷰 텍스트
- **출력**: 긍정 / 부정
- **역할**: 전체 프로젝트의 baseline

---

### Step 2. Multi-label Attribute Classification
- **문제 유형**: Multi-label Classification
- **입력**: 리뷰 텍스트
- **출력**: 11개 속성에 대한 존재 여부 (0 / 1)
- **특징**
  - 하나의 리뷰에 여러 속성이 동시에 존재 가능
  - `Sigmoid + BCEWithLogitsLoss` 사용
  - **LoRA(PEFT)** 기반 파인튜닝 실험

---

### Step 3. Aspect-Based Sentiment Analysis (ABSA)
- **문제 유형**: Attribute-level Sentiment Classification
- **입력**: (속성 + 리뷰 문장)
- **출력**: 해당 속성에 대한 긍/부정
- **핵심 포인트**
  - 하나의 리뷰 → 속성 수만큼 학습 샘플 확장
  - 입력 텍스트 구조에 따른 성능 비교

---

## 🛠 Tech Stack

- Python  
- PyTorch  
- Hugging Face Transformers  
- Datasets  
- PEFT (LoRA)  
- Scikit-learn  

---

## 📂 Project Structure
├── Step1_sentiment.ipynb
├── Step2_multilabel.ipynb
├── Step3_absa.ipynb
├── data/
│ └── reviews.csv
└── README.md


---

## ⚙️ Data Processing

- 텍스트 정제 및 토큰화
- Multi-label 라벨 벡터 구성
- ABSA를 위한 `(속성, 문장)` 단위 샘플 생성
- Train / Validation 분리

---

## 🤖 Modeling Strategy

### Base Models
- BERT
- RoBERTa

### Training
- HuggingFace `Trainer` 활용
- Step2에서 **LoRA 적용**
- Early Stopping 적용

---

## 📊 Evaluation Metrics

- Accuracy
- Precision / Recall
- **Macro F1-score**
  - 클래스 불균형을 고려한 공정한 평가를 위해 사용

---

## 🔍 Key Insights

- Multi-label 분류에서는 **Sigmoid + BCE**가 필수
- ABSA에서는 **모델보다 입력 텍스트 구조가 성능에 더 큰 영향**
- 스페셜 토큰 구조보다 **단순 문자열 구조가 동등하거나 더 좋은 성능**을 보임
- 데이터 규모가 작을 경우, 대형 모델 간 성능 차이는 크지 않음

---

## 🚀 Limitations & Future Work

- 데이터 규모 한계로 대형 모델의 잠재력 제한
- 속성 간 관계를 명시적으로 모델링하지 않음

### 향후 개선 방향
- Threshold 최적화
- 속성 간 관계 모델링
- Prompt 기반 Zero-shot 분류 비교
- 실제 서비스 적용 실험

---

## ✍️ One-line Summary
> 리뷰 텍스트를 대상으로 감성·속성·속성별 감성을 단계적으로 분석하며,  
> 입력 구조와 문제 정의가 모델 성능에 미치는 영향을 실험적으로 검증한 NLP 프로젝트

