# pj-data-analysis
SeSAC LLM DA pjt 1st

# 브라질 이커머스 데이터 분석 보고서 (3개 과제)

## 과제 1) 고객 세분화 & RFM 분석

### 목표
- Recency / Frequency / Monetary 기준으로 고객 세분화
- VIP, Loyal, Potential, At Risk, New Customers 그룹 정의 및 전략 제시

### 핵심 인사이트
- **VIP** : 프리미엄 멤버십, 한정판 리워드, 전담 상담
- **Loyal** : 적립금·정기배송, 연관 카테고리 쿠폰, 브랜드 알림
- **Potential** : 계단식 쿠폰, 개인화 추천, 구독 체험
- **At Risk** : 복귀 인센티브, CS/배송 경험 점검
- **New Customers** : 온보딩, 리뷰 리워드, 재구매 유도

---

## 과제 2) 배송 성과 분석 & 지역별 물류 최적화

### 목표
- 리드타임/지연 현황 파악 및 지역별 성과 비교
- 배송 지연이 리뷰에 미치는 영향
- 배송비 정책 효과 분석

### 주요 결과
- 전체 평균 **리드타임 12.40일**, **정시율 91.8%**
- 리드타임 가장 긴 권역: **North**, 정시율 최저 주: **AL**
- 배송 지연이 길수록 리뷰 점수 급락 (정시 vs 7일 이상 지연 구간 비교 시 큰 하락)
- **무료배송** 주문은 유료배송 대비 평균 리뷰 점수 **+0.23p** 높음
- 배송비와 주문수 간 **음의 상관관계** → 배송비 인하 시 주문 증가 가능성

### 실행 전략
- 리드타임 길고 정시율 낮은 지역에 **배송비 10% 차등 할인**
- 무료배송 확대 및 정시 배송 품질 관리 강화

---

## 과제 3) 카테고리별 수요 예측 & 재고 관리

### 목표
- 월별 수요 추이 및 계절성 분석
- 간단 예측과 안전재고(SS)·ROP 산출
- 재고 부족/과잉 위험 구간 식별

### 주요 결과
- 상위 카테고리 월별 수요 예측 및 **95% 신뢰구간** 제시
- **안전재고(SS)** = z × σ × √L (z=1.645, 95%)
- **ROP** = 평균일수요 × 리드타임 + 안전재고
- 월별 ROP 여유율로 **재고 부족/과잉 위험** 시각화 가능

### 운용 체크리스트
- 성수기 사전 발주
- 전진배치 가능 시 ROP 하향
- 비수기엔 ROP 축소 및 재고 소진 전략 적용

---

# 전체 코드 (Python)

## 0) 공통 설정

```python
import os, math, warnings
warnings.filterwarnings("ignore")

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

DATA_DIR = "./"

def read_csv(name):
    return pd.read_csv(os.path.join(DATA_DIR, name))

