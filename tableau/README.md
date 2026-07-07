# Tableau 대시보드 - Home Credit Default Risk

## 구성
- 단일 페이지 (1280 x 720)
- 상단 타이틀 + KPI 띠(전체 부도율 8.07% / 모델 AUC 0.766 / S1 고위험군 부도율 14.2%)
- 4개 차트 (2x2)

## 차트별 의도
| 차트 | 인사이트 |
|---|---|
| 1. 고객 위험군 분포 (도넛) | 도메인 룰 6개 세그먼트 비중. 어디에 고객이 몰려있는가 (S6 보통 45.1%, S1 고위험 1.3%) |
| 2. 세그먼트별 부도율 | 어떤 세그먼트가 평균(8.07%) 대비 위험한가. S1(14.2%) > S2(12.4%) > S6(11.0%) > S3(5.6%) > S5(5.0%) > S4(4.1%) |
| 3. Top 5 부도 예측 변수 (SHAP) | 모델이 의존하는 변수. 상위 5개는 모두 application 변수(EXT_SOURCE 1/2/3, AMT_GOODS_PRICE, ORGANIZATION_TYPE)이고 bureau 변수는 6순위 밖 |
| 4. 임계값 시뮬 | 승인 임계값에 따른 거절률 vs 승인 후 부도율 트레이드오프. 경영진 공격/보수 운영 모드 결정 지원 |

## 데이터 소스
- `outputs/tables/06_scored_data.csv`
- `outputs/tables/06_threshold_simulation.csv`
- `outputs/tables/07_shap_top_features.csv`

## 참고
- 전체 부도율(8.07%)은 세그먼트별 평균을 단순 평균한 값(8.72%)이 아니라 전체 307,511건 기준 실제 부도 비율. 세그먼트 뷰의 참조선은 FIXED LOD 계산(`전체평균_고정`)으로 고정.
- 최종 모델은 06번에서 선택한 LGB-B(+bureau), AUC 0.766.
