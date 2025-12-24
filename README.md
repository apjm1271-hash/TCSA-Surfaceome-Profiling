# TCSA-Surfaceome-Profiling
 **TCSA(The Cancer Surfaceome Atlas) 데이터를 활용한 세포 표면 단백질체 구조 프로파일링**

(https://colab.research.google.com/drive/1zPgB9lDUtWOtxLuFzUf1r8S9UBywiaFC#scrollTo=70uHqZ4lpbH5)

## 1. 프로젝트 개요 (Introduction)

본 프로젝트는 TCSA(The Cancer Surfaceome Atlas) 데이터를 활용하여,암세포 Surfaceome 내 단백질 간의 구조적 유사성을 정량화하고 기능적 핵심인 Common Core영역을 자동으로 추출하여 암에 범용적으로 적용될 수 있는 항원을 추출하는 것이 목표입니다.

## 2. 주요 분석 워크플로우 (Workflow)

* **Clustering**:foldseek algorithm을 이용한 surfaceome clustering
* **Superimposing**:가장 많이 clustering된 분자에 대해 TM-align 바이너리를 활용하여 대량의 PDB 데이터셋에 대해 TM-score 및 RMSD를 산출
* **Common Core Extraction**: TM-align 결과에서 거리 5.0Å 이내로 정렬된 잔기(Matched residues)만을 Biopython의 PDB.Select 기능을 통해 새로운 PDB 파일로 자동 추출
* **데이터 필터링 및 랭킹**: matched_df를 생성하여 TM-score 기준 상위 5개 타겟을 자동으로 선별
* **다중 그리드 시각화 (3D Visualization)**: py3Dmol 라이브러리를 통해 선별된 상위 구조들의 중첩 상태를 그리드 형태로 시각화하여 구조적 일치도를 시각화

## 3. 주요 분석 결과 (Key Results)
* **데이터 통계**: SEMA4G 등을 기준으로 다수의 Surfaceome 단백질에 대한 구조 비교를 수행하였으며, 특정 단백질 쌍에서 높은 구조적 보존성(TM-score > 0.7)이 있음을 확인
  <img width="784" height="1243" alt="Screenshot 2025-12-24 at 14 28 48" src="https://github.com/user-attachments/assets/c8534012-3c1f-4b51-9b87-5280905ab936" />

* **시각화 결과**: 
  <img width="500" height="484" alt="Screenshot 2025-12-24 at 14 28 58" src="https://github.com/user-attachments/assets/9493789d-7e55-4836-b4d3-92e5ad816ab4" />

  <img width="1636" height="953" alt="Screenshot 2025-12-24 at 14 29 06" src="https://github.com/user-attachments/assets/d693ea36-4e72-4c09-9205-8212960b67bb" />


## 4. 향후 연구 및 발전 가능성 (Future Directions)

### **1) Surfaceome 구조적 프로파일링 고도화**
* 표면 노출도(SASA) 분석: Shrake-Rupley 알고리즘을 적용하여 공통 구조 중 실제 세포 외부에 노출되는 면적을 계산함으로써, 항체나 약물 접근이 용이한 타겟 부위를 선별
* 서열 보존성(Conservation) 분석: MSA(Multiple Sequence Alignment) 데이터를 매핑하여, 변이가 적으면서도 입체 구조가 안정적으로 유지되는 영역을 도출

### **2) 데이터 스케일업 및 데이터베이스화**
* 수천 개의 표면 단백질 구조 데이터에 대한 **All-to-all structural comparison**을 수행하여 미지의 구조적 유사성을 발굴하는 대규모 스캐닝으로 확장 가능

## 5. 기술 스택 (Tech Stack)
* **Language**: Python
* **Bioinformatics Tools**: TM-align, Biopython
* **Visualization**: py3Dmo
* **Data Analysis**: Pandas
* **Environment**: Google Colab
