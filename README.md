# AI-based-Groundwater-Level-Fluctuation-Prediction
This project builds an AI-based model to predict long-term groundwater level changes using 10 years of multi-source environmental data.   Due to missing t-1 groundwater levels, extensive feature engineering and external hydrological datasets were incorporated to improve predictive accuracy.
<p align="center">
  <img src="./poster.png" alt="Competition Poster" width="600">
</p>
## 📑 목차
1. 개요
2. 배경
3. 데이터셋 설명
4. 방법 요약
5. 결과 요약
6. 프로젝트 구조
7. 노션 링크

---

## 🔍 1. 개요
10년간의 지하수 수위, 기상 자료, 하천 수위를 통합 분석하여  
지하수위의 장기 변동을 예측하기 위한 머신러닝 모델(LightGBM)을 개발하였습니다.  
누적 강수량, 주기성(time cycle), 외부 하천 수위 등 다양한 특징을 추가하여 예측 성능을 개선했습니다.

---

## 🏞️ 2. 배경
지하수 수위는 다음과 같은 특성으로 인해 예측이 까다롭습니다:
- t-1 시점 지하수 수위를 사용할 수 없음
- 계절성·비선형성 존재
- 긴 결측치 구간
- 지점별 패턴 차이(특히 7번·10번 지점)

이를 해결하기 위해:
- 하천 수위, 누적 강수량 등 대체 설명 변수를 설계
- 시계열 패턴을 보존하는 결측치 처리 전략 적용
- 지점별 모델 + Optuna 튜닝 수행

---

## 📊 3. 데이터셋 설명
### 사용 데이터(https://aida.kisti.re.kr/competition/main/problem/PROB_000000000002820/detail.do)
- **지하수 수위(시간 단위, 12개 관측지점)**
- **기상 자료(ASOS)**:  
  기온, 강수량, 풍속, 습도, 기압, 지면온도 등
- **하천 수위**: 위·경도 기반 가장 가까운 관측소에서 수집
- **추가 생성 변수**
  - 7일/30일 누적 강수량  
  - 가뭄지수, 침투율, 유출율  
  - 다항특성(변수 간 상호작용)  
  - 시간 주기성(sin/cos)

---

## ⚙️ 4. 방법 요약
- 모델: **LightGBM(최종 채택)**  
- 결측치 처리:
  - 단기 결측 → 선형보간  
  - 장기 결측 → LightGBM 예측 기반 보간  
  - 그 외 → 동일 시간대 평균  
- 피처 엔지니어링:
  - 누적 강수량 변환  
  - 하천 수위 외부데이터 추가  
  - 주기적 시간 인코딩  
  - 다항 특성 생성  
- 지점별 모델 구성 및 Optuna로 50회 파라미터 탐색

---

## 🏆 5. 결과 요약
리더보드 평가 기준(테스트 데이터):
- **NSE:** 0.593  
- **KGE:** 0.815  
- **평균:** 0.704  
LightGBM이 가장 안정적이고 높은 성능을 기록했습니다.

---

## 📝 7. 노션 링크
👉 **Notion 문서:** *https://www.notion.so/317a4a076c60807098d7fea3a6604586*
