---
name: software-fundamentals
description: Apply Matt Pocock's "Software Fundamentals Matter More Than Ever" principles together with Neo's metaphysical and theological framework. Use this skill whenever the user starts a new coding task, requests planning/architecture, asks for module design, wants to refactor existing code, or begins a new product/feature spec — even if they don't explicitly mention "fundamentals" or "principles". Triggers include phrases like "make a feature", "build X", "design Y", "plan Z", "refactor", "구현해줘", "기획", "설계", "어떻게 짜지", "모듈 만들어줘", "프로젝트 시작". Skip ONLY for trivial one-line fixes, pure factual lookups, or non-engineering tasks. When in doubt, trigger.
---

# Software Fundamentals (소프트웨어 펀더멘털)

> **Deep × Core × Interface — 깊음과 핵심 인터페이스**

> "Code is not cheap. Bad code is the most expensive it's ever been." — Matt Pocock
>
> "여호와를 경외하는 것이 지식의 근본이거늘" — 잠언 1:7

Fundamentals = 근본. 두 문장은 같은 진술의 두 층위다.

---

## 핵심 워크플로우

새 코딩/기획 주문 받으면 **무조건** 이 순서:

```
1. Grill Me        의도 추궁 (사용자 언어로)         (→ GRILL_ME_PROTOCOL.md)
       ↓
2. Spec Lock       명확한 명세 합의 + Ubiquitous Language
       ↓
3. Module Design   Deep Module 설계 + Vertical Slice 선택  (→ DEEP_MODULE_REVIEW.md, CORE_PRACTICES.md)
       ↓
4. Dependency Check  의존성 3가지 질문
       ↓
5. Build           TDD로 구현                          (→ CORE_PRACTICES.md)
       ↓
6. Review          의식적 코드 리뷰
       ↓
7. Daily Design    매일 시스템 설계에 투자 (Kent Beck)
```

**1~4단계가 5단계보다 길어야 정상이다.**

---

## 발동 조건

| 발동함 | 발동 안 함 |
|--------|------------|
| 새 기능/모듈 요청 | 오타 수정 |
| 신규 프로젝트 기획 | 한 줄 변경 |
| 리팩터링 요청 | 사실 검색 |
| 아키텍처 설계 | 번역/카피라이팅 |
| "어떻게 짜지?" 류 모호한 질문 | 엔지니어링 무관 작업 |

---

## 5대 참조 문서

세부는 아래 문서를 필요할 때 읽는다.

| 문서 | 결 | 언제 읽나 |
|------|-----|----------|
| `references/PHILOSOPHY.md` | 형이상학 | 작업 시작 전, 또는 "이거 왜 만들지?"라는 의문이 들 때. 기획자 형이상학(a~z → ㄱ~ㅎ)과 근본의 출처. |
| `references/SIX_PITFALLS.md` | 회피 (negative) | 모든 작업의 기준선. Pocock의 6가지 함정과 회피 원칙. |
| `references/CORE_PRACTICES.md` | 실천 (positive) | SIX_PITFALLS와 짝. Ubiquitous Language / Vertical Slices / TDD / Deep Modules — 지켜야 할 4가지 긍정 원칙. |
| `references/GRILL_ME_PROTOCOL.md` | 도구 | 1단계(Grill Me)에서 사용할 질문 템플릿. |
| `references/DEEP_MODULE_REVIEW.md` | 도구 | 3단계(Module Design)와 6단계(Review)에서 모듈 판별 체크리스트. |

**구조:** PHILOSOPHY가 뿌리, SIX_PITFALLS + CORE_PRACTICES가 양 날개(회피와 실천), GRILL_ME + DEEP_MODULE이 손에 들고 쓰는 도구.

---

## 빠른 자가 점검 (매일 30초)

1. 어제 짠 코드 중 Shallow Module이 있었나? (`DEEP_MODULE_REVIEW.md`)
2. 오늘 추가할 의존성 진짜 필요한가?
3. 이번 주 시스템 설계 시간이 코딩 시간의 10% 이상인가?
4. 마지막으로 "왜 이 제품을 만드는가" 물은 게 언제인가?
5. 코드/UI/문서가 같은 단어를 쓰고 있나? (Ubiquitous Language)
6. 이번 슬라이스가 끝에서 끝까지 동작하나? (Vertical Slice)
7. 이번 주 짠 코드에 테스트 없는 게 있나? (TDD)

---

## 안티 패턴 (이것의 정반대)

- 사용자 의도를 묻지 않고 가두는 화면 → Grill Me의 반대
- 일부러 모호한 약관/명세 → Spec Lock의 반대
- 일부러 Shallow하게 만들어 못 떠나게 함 → Deep Module의 반대
- 의존성 강제 결박 → 의존성 검토의 반대

이런 패턴은 본질적으로 "한정된 파이 빼앗기" 게임이다. 새 차원을 만들지 못한다. 자세한 이유는 `references/PHILOSOPHY.md` 참조.
