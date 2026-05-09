# 입원환자 진료 도구
**Inpatient Clinical Toolkit · 의료진용 단일 페이지 임상 보조 도구**

> 입원환자 진료 의료진을 위한 단일 HTML 임상 도구. 다빈도 입원상병 101개 ICD-10 데이터베이스, 사망확률 평가 (CURB-65 · qSOFA · Charlson · CFS · NEWS2), 점수 해석 가이드를 통합했습니다.

---

## 개요

본 도구는 입원환자 진료 시 의료진이 침상에서 빠르게 활용할 수 있도록 설계된 단일 HTML 페이지입니다. 빌드 도구·서버 설치 없이 브라우저로 바로 열어 사용합니다.

세 가지 통합 기능:

1. **다빈도 입원상병 101개** — HIRA 입원 청구 패턴 기반 ICD-10 진단 데이터베이스, 검색·카테고리 필터·임상 정보 제공
2. **사망확률 평가** — CURB-65, qSOFA, Charlson Comorbidity Index, Clinical Frailty Scale, NEWS2 통합 평가 + 자동 사망률 추정
3. **점수 가이드** — 5개 임상 도구의 점수 해석 표·사망률 데이터·한국 적용 주의사항

---

## 빠른 시작

```bash
git clone https://github.com/<your-org>/inpatient-clinical-toolkit
cd inpatient-clinical-toolkit
# 더블클릭 또는
open index.html      # macOS
xdg-open index.html  # Linux
start index.html     # Windows
```

별도 빌드 도구·Node.js·서버 설치 불필요. 모든 React·CSS·데이터가 단일 HTML 파일에 인라인으로 포함되어 있습니다.

**시스템 요구**: 모던 브라우저 (Chrome 90+, Safari 14+, Firefox 90+, Edge 90+).

---

## 화면 구성

### 1️⃣ 다빈도 입원상병

ICD-10 코드 101개의 검색·열람 화면. 각 진단별 임상 정보:

- 주요 임상 소견 (증상·징후)
- 응급·악화 지표 (red flags)
- 진단 접근 (병력·진찰·검사실·영상·중증도 평가)
- 감별진단
- 표준 치료
- 입원 중 모니터링
- 주의 합병증
- 퇴원 기준·교육
- 예후
- 참고 가이드라인
- 환자·가족 설명용 쉬운 표현 (접이식)

### 2️⃣ 사망확률 평가

| 도구 | 영역 | 출처 |
|---|---|---|
| **CURB-65** | 폐렴 중증도 (5점) | Lim WS et al. Thorax 2003;58:377–82 |
| **qSOFA** | 패혈증 선별 (3점) | Sepsis-3 · Seymour CW et al. JAMA 2016;315:762–74 |
| **Charlson** | 동반질환 지수 + 연령보정 | Charlson ME et al. J Chronic Dis 1987;40:373–83 |
| **CFS** | Rockwood 임상 노쇠 척도 (1–9) | Rockwood K et al. CMAJ 2005;173:489–95 |
| **NEWS2** | 활력징후 추적 모니터링 | Royal College of Physicians (RCP) 2017 |

추가 평가 항목: CAM(섬망 감별), MDR 위험인자, 추가 노쇠·예후 인자.

자동 산출:
- 점수별 30일/입원 사망률 (CURB-65, qSOFA)
- 1년 사망률 (CFS)
- 10년 생존율 (Charlson)
- 종합 위험계층 (저위험 / 중등도 / 매우 고위험)
- 위험계층별 권장 조치 (sepsis bundle, ICU 전과 기준, DNR 논의 등)

### 3️⃣ 점수 가이드

5개 임상 도구의 점수표·해석·사망률 데이터를 한 화면에 정리. 한국 적용 시 ±10–15%p 오차 안내 포함.

---

## 진행 상태

| 항목 | 상태 |
|---|---|
| 다빈도 입원상병 ICD-10 데이터 | ✅ 101/101 |
| 사망확률 평가 도구 (5개 통합) | ✅ 완료 |
| 점수 해석 가이드 | ✅ 완료 |
| 임상 콘텐츠 (진단·치료·모니터링·예후) | 🔄 5/101 진행 중 |

### 임상 콘텐츠 작성 완료
| 코드 | 진단 | 항목 수 |
|---|---|---|
| J18 | 폐렴 | 38 + 예후 + 가이드라인 |
| N39 | 요로감염 | 37 + 예후 + 가이드라인 |
| I50 | 심부전 | 41 + 예후 + 가이드라인 |
| I63 | 뇌경색증 | 40 + 예후 + 가이드라인 |
| J44 | COPD | 38 + 예후 + 가이드라인 |

### 작성 예정 (RISK_RELEVANT_CODES 우선)
J20 급성 기관지염, J45 천식, J42 만성 기관지염, N18 만성 신장병, I10 본태성 고혈압, I20 협심증, I21 급성 심근경색, I25 만성 허혈성 심장병, E11 2형 당뇨병, F03 치매

---

## 기술 스택

- **React 18** (인라인 번들, CDN/빌드 도구 불필요)
- **단일 HTML 파일** (~250 KB)
- **CSS-in-JS** (인라인 스타일, 외부 CSS 없음)
- **Noto Sans KR / Noto Serif KR** (Google Fonts)
- **외부 의존성 0개** (오프라인 사용 가능, Google Fonts만 온라인 시 로드)

---

## 데이터 출처

### 진단 분류
- **ICD-10** / **KCD-8** (한국표준질병사인분류)
- **HIRA 다빈도질병 통계** (건강보험심사평가원, 2023–2024 입원 청구 기준 패턴)

### 사망확률 산출 근거
- CURB-65 점수별 30일 사망률 — Lim 2003 검증 코호트 (영국·뉴질랜드·네덜란드)
- qSOFA 입원 사망률 — Seymour 2016 (Sepsis-3 발표 시 검증)
- Charlson 10년 생존율 공식 — `0.983^exp(0.9 × CCI)` (Charlson 1987 원공식)
- Charlson 1년 사망률 — 검증 연구 평균값 단순화
- CFS 1년 사망률 — Rockwood/Mitnitski 등 검증연구 평균값
- NEWS2 합산 점수 권장 모니터링 — RCP 2017

---

## ⚠️ 의료법적 고지

본 도구는 **의료진의 임상 판단을 보조**하기 위한 참고 자료이며, 표준 진료지침이나 의료진 자문을 대체하지 않습니다.

표시되는 사망확률 수치는 각 도구의 원논문 검증 코호트의 **통계적 평균값**으로:

- 개별 환자의 실제 사망 확률을 정확히 예측하지 않습니다
- 한국인 환자 적용 시 **±10–15%p**의 오차가 있을 수 있습니다
- 인종·의료체계·기저질환 분포에 따라 결과가 달라집니다

**최종 진단·치료 결정은 환자 개별 상황에 따른 임상의의 종합적 판단을 따라야 합니다.** 환자·가족 설명 시 본인 상황은 더 좋을/나쁠 수 있다는 점을 함께 전달하세요.

본 도구의 사용으로 인한 결과에 대해 개발자는 어떠한 책임도 지지 않습니다 (MIT License `AS IS` 조항).

---

## 임상 데이터 검수 필요 항목

기여 시 다음 영역의 의료진 검수가 우선 필요합니다.

- **약제 용량·기간** — 가이드라인 간 미세 차이 통일
- **한국 의료 환경 반영** — 예: tPA 적응증 시간 창, 한국 ESBL 유병률 반영 항생제 선택
- **MDR 정의 범위** — IDSA vs 한국 기준 차이
- **사망률 한국 코호트 데이터** — 한국인 검증 연구 반영

---

## 기여 / Contributing

의료진의 임상 검수와 데이터 보강을 환영합니다.

```bash
# 1. Fork 후 clone
# 2. 새 브랜치 생성
git checkout -b clinical-content/<진단코드>

# 3. index.html의 DISEASES 배열에서 해당 코드 entry 수정
# 4. 임상 콘텐츠 추가 (clinicalDiagnosis, treatment, monitoring 등)

# 5. PR 생성 (가능하면 검수 의료진 정보 포함)
```

기여 가이드라인:
- 모든 임상 권고는 **공인 가이드라인 출처** 명시
- 약제는 **일반명(generic name)** 사용
- 한국 진료지침이 있는 경우 **한국 학회 지침을 우선** 참조
- 새 진단 추가 시 **HIRA 입원 빈도 근거** 함께 제출

---

## 로드맵

- [x] **v1.0** 단일 앱 통합 (다빈도 + 평가 + 가이드)
- [x] **v1.1** 5개 우선 진단 임상 콘텐츠
- [ ] **v1.2** RISK_RELEVANT_CODES 14개 진단 임상 콘텐츠 완료
- [ ] **v1.3** 빈도 상위 30개 진단 임상 콘텐츠
- [ ] **v1.4** 한국인 코호트 사망률 데이터 보정
- [ ] **v2.0** 진단별 환자 점수 시계열 저장 (localStorage), 입·퇴원 시점 추적
- [ ] **v2.1** EMR 연동 (FHIR 표준 검토)

---

## 라이선스

MIT License — 자세한 내용은 [LICENSE](./LICENSE) 참고.

```
Copyright (c) 2024-2026 [JuneYoung/biofit-research]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND...
```

---

## 참고문헌

1. Lim WS, van der Eerden MM, Laing R, et al. *Defining community-acquired pneumonia severity on presentation to hospital: an international derivation and validation study.* **Thorax** 2003;58:377–82.
2. Seymour CW, Liu VX, Iwashyna TJ, et al. *Assessment of Clinical Criteria for Sepsis: For the Third International Consensus Definitions for Sepsis and Septic Shock (Sepsis-3).* **JAMA** 2016;315:762–74.
3. Charlson ME, Pompei P, Ales KL, MacKenzie CR. *A new method of classifying prognostic comorbidity in longitudinal studies: development and validation.* **J Chronic Dis** 1987;40:373–83.
4. Rockwood K, Song X, MacKnight C, et al. *A global clinical measure of fitness and frailty in elderly people.* **CMAJ** 2005;173:489–95.
5. Royal College of Physicians. *National Early Warning Score (NEWS) 2: Standardising the assessment of acute-illness severity in the NHS.* London: RCP, 2017.
6. 건강보험심사평가원. *다빈도질병 통계.* opendata.hira.or.kr (2023–2024).

---

## 연락처

- Issues: [GitHub Issues](https://github.com/biofit-research/inpatient-care
- 임상 검수 기여: PR 또는 [Discussions](https://github.com/biofit-research/inpatient-care)
