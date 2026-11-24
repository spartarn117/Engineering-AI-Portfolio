# 사출성형 품질 예측 — 트리 기반 AI 모델 비교

**구분:** AI응용제조 4인 팀 프로젝트 (2026)

## 연구 문제

사출성형 공정에서 측정한 수치형 변수 13개로 품질을 4개 등급(Waste, Acceptable, Target, Inefficient)으로 예측합니다.

## 담당 범위

- **본인 담당:** DecisionTree, RandomForest, ExtraTrees 구현과 5-Fold CV, 하이퍼파라미터 탐색, 모델별 예측 및 오분류 분석, 최종 발표
- **협업:** 공통 데이터 분할·전처리 담당자의 결과를 재사용했으며, SVM/MLP 및 전체 분석은 별도 팀원의 역할
- Colab 코드 작성·수정 과정에서 생성형 AI 도움을 받았음. 개인적으로 수행·검토한 범위를 코드의 전체 독자 작성과 동일시하지 않음

## 사용 방법

**바로 재현 가능한 분석:** [Review_Results.ipynb](Review_Results.ipynb)를 이 폴더에서 실행하면 `results/metrics.csv` 및 `results/tree_predictions.csv`를 사용해 저장된 291개 테스트 결과를 다시 집계합니다. 학습은 새로 수행하지 않습니다.

**모델 학습 코드:** [Tree_Models_Training.ipynb](Tree_Models_Training.ipynb)는 1번 담당자의 `01_공통분할_즉시공유.zip`과 [원본 공개 데이터](https://github.com/airtlab/machine-learning-for-quality-prediction-in-plastic-injection-molding/blob/master/dataset/data.csv)가 있어야 원래의 실험 구성을 재실행할 수 있습니다. 이 저장소에는 해당 팀 공통 분할 파일을 포함하지 않았습니다.

## 검증 결과

| 모델 | 5-Fold CV Macro F1 | 최종 Test Accuracy | Test Macro F1 | 실제 Waste 누락 |
|---|---:|---:|---:|---:|
| DecisionTree | 0.9241 | 0.9072 | 0.9063 | 4 |
| RandomForest | 0.9469 | **0.9381** | **0.9365** | 5 |
| ExtraTrees | **0.9502** | 0.9313 | 0.9300 | 7 |

- 전체 1,451개, 학습 1,160개, 테스트 291개(모델별 동일 샘플)
- 대표 트리 모델은 **학습 교차검증 Macro F1**으로 ExtraTrees를 선정
- **최종 Test Accuracy는 RandomForest**가 더 높았지만, 테스트 점수로 모델을 다시 선택하거나 튜닝하지 않음
- 트리별 변수 중요도는 예측에 사용된 정보량을 나타내며 인과관계를 뜻하지 않음

## 결과 자료

- [성능 원표](results/metrics.csv)
- [테스트 예측값](results/tree_predictions.csv)
- [튜닝 요약](results/cv_tuning_summary.csv)
- [RF 변수 중요도](results/feature_importance.csv)
- [CV 튜닝 전후 F1](results/figures/cv_before_after_f1.png)
- [최종 Test Accuracy](results/figures/final_test_accuracy.png)
- [RF 변수 중요도 이미지](results/figures/feature_importance_rf.png)

## 한계

새로운 생산일자·설비·제품에 대한 외부 검증이 이루어지지 않았으며, 실제 생산라인에 투입한 결과가 아닙니다. 저장된 결과를 재집계하는 것은 원본 코드 및 전처리 전체를 재현하는 검사와 다릅니다.
