# Engineering & AI Portfolio

**박찬웅 | 서울과학기술대학교 기계공학 전공**

기계공학의 설계·해석 경험을 바탕으로, **문제 정의 → 모델링/설계 → 결과 비교 → 한계 검토**의 흐름에 관심을 두고 프로젝트를 수행했습니다. KIST GROW Lab 현장실습 지원을 위해 관련 자료를 한곳에 정리했습니다.

## 먼저 볼 자료

| 자료 | 내용 | 열기 |
|---|---|---|
| **프로젝트 포트폴리오 (9쪽)** | CAD, CFD, AI 프로젝트 및 연구 관심을 한눈에 소개 | [PDF](portfolio/Portfolio_GROW_Lab.pdf) |
| **ANN–GA 성형공정 최적화** | 신경망 대리모델과 유전알고리즘을 이용한 금형 변수 탐색 | [프로젝트 설명](ann-ga-hat-forming/README.md) · [Colab 노트북](ann-ga-hat-forming/Hat_Forming_ANN_GA.ipynb) |
| **사출성형 품질 예측** | DecisionTree/RandomForest/ExtraTrees 모델 비교, 오류 분석 | [프로젝트 설명](injection-quality-tree-models/README.md) · [코드](injection-quality-tree-models/Tree_Models_Training.ipynb) · [결과 재확인](injection-quality-tree-models/Review_Results.ipynb) |

## 1. ANN–GA 기반 Hat 형상 성형공정 최적화

- **문제:** 목표 제품 형상에 가깝게 성형되도록 금형 치수를 탐색
- **방법:** 제공된 Abaqus 성형 사례 **891개**를 활용해 5개 입력에서 7개 성형 후 형상변수를 예측하는 ANN 구성, 4개 독립 금형 설계변수에 대한 GA 탐색
- **결과:** 독립 Test에서 높이 H의 R²는 약 **0.997**, 두 번째 반경 R₂의 R²는 약 **0.639**로 출력별 성능 차이가 존재. 스프링백 우선 대안의 **ANN 예측값**은 기준 0.5379°에서 0.1041°로 달라졌음
- **범위:** 생성형 AI의 도움을 받아 Colab 코드를 구성하고 분석·검토한 과제. **새 Abaqus 해석이나 실물 성형 검증은 수행하지 않음**

자세한 가정과 한계는 [상세 자료](ann-ga-hat-forming/README.md) 및 [검토 보고서](ann-ga-hat-forming/Source_Audit_Report.md)에 기재했습니다.

## 2. 사출성형 품질 예측 — 트리 기반 모델

- **문제:** 13개 공정변수로 사출성형 품질 등급 4개를 분류
- **담당:** 4인 팀 프로젝트 중 **트리 모델(Decision Tree, Random Forest, ExtraTrees) 구현·교차검증·튜닝·분석 및 최종 발표 담당**. 데이터 분할·전처리, 타 모델·종합 평가는 다른 팀원이 담당
- **방법:** 원본 1,451개 중 학습 1,160개/테스트 291개. 학습 내 5-Fold CV로 모델 설정 탐색, 확정 후 별도 Test 평가
- **결과:** 학습 CV Macro F1은 ExtraTrees **0.9502**가 가장 높고, 테스트 Accuracy는 RandomForest **0.9381**이 가장 높음
- **한계:** 모델별 Waste 누락이 남아 있으며, 새로운 생산 환경에 대한 일반화는 검증하지 않음

[저장된 예측값으로 지표 재확인하기](injection-quality-tree-models/Review_Results.ipynb) · [프로젝트 상세](injection-quality-tree-models/README.md)

## 3. 기계공학 기반 프로젝트와 연구 관심

기존 [포트폴리오 PDF](portfolio/Portfolio_GROW_Lab.pdf)에 DBD 플라즈마 액추에이터 CFD, 태양광 냉각 매니폴드 설계, 광학현미경 차광 커버의 CAD 설계·제작 과정을 정리했습니다. 또한 각 로터의 추력 방향을 두 축으로 독립 조절하는 **다자유도 틸트로터 회전익기**를 장기적으로 구상하고 있습니다. **현재 구상 단계이며 기체 제작이나 비행제어 실증 경험을 뜻하지 않습니다.**

이 관심을 바탕으로, 구조·환경이 달라졌을 때 행동을 어떻게 결정하고 검증하는지 로봇 시스템에서 배우고자 합니다. 이는 GROW Lab의 연구와의 **관심 및 방법론적 접점**이지, 본 저장소가 로봇 행동 정책이나 비행 제어를 구현했다는 의미는 아닙니다.

## 재현성 및 저작권 관련 안내

- 저장소에는 **직접 제공받은 수업 원본 데이터와 타 팀원의 분할 파일을 기본적으로 포함하지 않았습니다.** 공개 재배포 가능 여부가 확인되지 않았기 때문입니다.
- ANN–GA 코드의 학습 전체 재실행에는 원본 `input.csv`/`target.csv`와 모델 저장 경로 설정이 필요합니다. 기존 노트북의 일부 실행 결과가 저장되어 있지만, 나중에 추가된 점검 단계 중에는 미실행 셀도 있습니다.
- 트리 모델 학습 노트북은 공통 분할 ZIP이 필요한 팀 연계 실행 파일입니다. 반면 `Review_Results.ipynb`는 제공된 CSV 결과를 읽어 **저장된 테스트 점수를 재계산**할 수 있습니다.
- 생성형 AI 활용 여부, 개인 기여 및 검증하지 않은 부분을 각 프로젝트에 구분했습니다.
- 공정 원본 데이터 출처: [airtlab / machine-learning-for-quality-prediction-in-plastic-injection-molding](https://github.com/airtlab/machine-learning-for-quality-prediction-in-plastic-injection-molding). 원 논문과 수업 데이터의 차이는 ANN–GA [검토 보고서](ann-ga-hat-forming/Source_Audit_Report.md) 참고.

> 이 저장소는 대학·연구실 지원용 프로젝트 기록이며, 새롭게 구현·검증한 로봇 시스템을 주장하지 않습니다.
